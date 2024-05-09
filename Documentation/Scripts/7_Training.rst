Training
====================================

7.1 Création de dataSet sur HuggingFace
----------------------------------------------

pour la suite on va  prendre comme exemple les deux images suivantes:

.. figure:: /Documentation/Images/Exemple_Images.png
   :width: 100%
   :align: center
   :alt: Alternative text for the image
   :name: Exemple_Images

Aprés labelisation de vos images et obtenir le fichier json,de cette `forme <https://github.com/MasrourTawfik/Textra/blob/main/Codes/Exemple/Exemple_Training.json#L2>`_.

.. hint::
   - Le json est de forme d'une liste contenait deux dictionnaires, chacun pour une image on a pris que deux images à titre d'exemple, mais vous allez utiliser plusieurs.
   - La suite de code est elaboré sur Google Colab.
   
7.1.1 Preparation de fichier json
+++++++++++++++++++++++++++++++++++

Le fichier obtenu jusqu'à maintenant n'est pas encore compatible avec la forme qui accepte la famille des modèles LayoutLM
parmi ses non compatibilités :

- bbox (les coordonnées des rectangles de chaque labelisation **[xmin,ymin,xmax,ymax]** ) ne sont pas normalisés entre **[100,1000]**.

- Dans la nouvelle forme, on a une liste contient les informations des images, chacune est représentée par un  dictionnaire dont les clés sont **['id', 'image', 'bboxes', 'ner_tags', 'tokens']**

.. code-block:: python

   # Import some Libraries
   import json # v2.0.9
   import os
   from PIL import Image # v9.4.0
   import io

.. note:: 
   - Prends garde aux versions des bibliothèques mentionnées dans les commentaires ci-dessus.

.. code-block:: python

   def Get_Image(Image_name):
    filename = Image_name
    image_path = os.path.join("PATH_YOUR_TRAINING_IMAGES",filename)
    print(image_path)
    with open(image_path, 'rb') as file:
        binary_image_data = file.read()
    image = Image.open(io.BytesIO(binary_image_data))
    return image

Cette fonction renvoie une image ce format Pillow, prenant en paramètre le nom de l'image **Image_name**.

**PATH_YOUR_TRAINING_IMAGES** est le chemin de votre dossier contenant les images de Training les même que vous allez labelliser sur Labet-Studio.
par exemple **/content/drive/MyDrive/Exemple/Data**.

.. code-block:: python

   def Get_Annoutaions(Annoutaion):
    bboxes = []
    ner_tags = []
    tokens = []
    Number_annotaions = len(Annoutaion)
    for j in range(Number_annotaions):
        box = Annoutaion[j]["box"]
        text = Annoutaion[j]["text"]
        tag = Annoutaion[j]["label"]
        #Transform box data :
        box = [int(x * 10) for x in box]
        # Append
        bboxes.append(box)
        tokens.append(text)
        ner_tags.append(tag)

    return bboxes,tokens,ner_tags

**Get_Annoutaions** renvoie 3 listes : **bboxes**, **tokens** et **ner_tags**, chacune contenant les informations des annotations de l'image.
il corrige aussi le probleme de la bbox qui n'est pas normalisée entre **[100,1000]** en multipiant par 10.

.. code-block:: python

   def Prepare_Data(Json_path):
    dataSet = []
    # Read the JSON file
    with open(Json_path, 'r') as file:
        data = json.load(file)
    n = len(data) # n : Number_Images
    for i in range(n):
          ###########################################
          image = Get_Image(data[i]["file_name"])
          ########################################
          bboxes,tokens,ner_tags=Get_Annoutaions(data[i]["annotations"])
          #print(ner_tags)
          ############################################
          document_dict = {
              'id': i,
              'image': image,
              'bboxes': bboxes,
              'ner_tags': ner_tags,
              'tokens': tokens
          }
          dataSet.append(document_dict)
    return dataSet

**Prepare_Data** renvoie une liste de dictionnaires dont les clés sont **['id', 'image', 'bboxes', 'ner_tags', 'tokens']**,prenant en paramètre le chemin de fichier json **Json_path**.

.. code-block:: python

   Json_path = "PATH_YOUR_TRAINING_JSON_FILE"
   dataSet = Prepare_Data(Json_path)
   print("Number of Images : ",len(dataSet))

Cette cellule renvoie un dictionnaire **dataSet** contient l'ensemble des informations de chaque image.

**PATH_YOUR_TRAINING_JSON_FILE** est le chemin de votre fichier json, par exemple **/content/drive/MyDrive/Exemple/Exemple_Training.json**.

7.1.1 Compte HuggingFace
+++++++++++++++++++++++++

Vous connaissez pas HuggingFace ?,c'est qui est une grande plateforme d'IA avec une large communauté, contient les modèles préétablis, des datasets, des espaces..., on vous laisse la main pour découvrir `plus <https://huggingface.co/>`_.

On besoin d'abord de créer un compte sur HuggingFace, si vous l'avez pas encore.

.. figure:: /Documentation/Images/Hugging_Face_Account.png
   :width: 100%
   :align: center
   :alt: Alternative text for the image
   :name: Compte HuggingFace

Il faut installer ces bibliothèques pour pouvoir utiliser HuggingFace

.. code-block:: bash

   !pip install huggingface_hub
   !pip install -q datasets seqeval

Pour pouvoir hoster votre data sur HuggingFace, vous devez avoir une **token key**. Cela se trouve dans votre compte HuggingFace. `Comment <https://github.com/MasrourTawfik/Textra/tree/main/Documentation/Videos>`_.


.. code-block:: python

   from huggingface_hub import notebook_login
   # hf_XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX , this the token to put , Get Yours
   notebook_login()

.. figure:: /Documentation/Images/Login_token.png
   :width: 60%
   :align: center
   :alt: Alternative text for the image
   :name: LogIn

7.1.1 Création de le DataSet
++++++++++++++++++++++++++++++

.. code-block:: python

   from sklearn.model_selection import train_test_split
   from datasets import Dataset, Features, Sequence, ClassLabel, Value, Image

.. code-block:: python

   dataset_features = Features({
    'id': Value('string'),
    'image': Image(decode=True),
    'bboxes': Sequence(Sequence(Value('int64'))),
    'ner_tags': Sequence(ClassLabel(names=['InvNum','InvDate', 'Fourni' ,'TTC','TVA','TT' ,'Autre'])),
    'tokens': Sequence(Value('string')),
    })

Les colonnes de dataset sont définies ici : id, images, box,ner_tags,tokens avec le type de données de chacune.

.. note:: 
   - Pour **names** de *ner_tags* colonne , il faut remplacer avec vos propres classes en respectant l'ordre.
   c-à-d l'ordre avec le quelle on a encodé les classes, par exemple si on désigne 0 pour InvNum , il faut le mettre le premier dans names.

   - Le type Sequence comme une liste en python.

.. code-block:: python

   # Convert the final_dataset into a dictionary of lists
   data_dict = {
      'id': [item['id'] for item in dataSet],
      'image': [item['image'] for item in dataSet],
      'bboxes': [item['bboxes'] for item in dataSet],
      'ner_tags': [item['ner_tags'] for item in dataSet],
      'tokens': [item['tokens'] for item in dataSet],
   }

.. code-block:: python

   # Convert the dictionary of lists into a HuggingFace Dataset
   hf_dataset = Dataset.from_dict(data_dict, features=dataset_features)
   ds = hf_dataset.train_test_split(test_size=0.07,shuffle=True,seed =10) 

Ici on split le dataset en 2 parties : 93% pour l'entrainement et 7% pour le test, vous pouvez choisir un autre pourcentage.

.. code-block:: python
   
   ds.push_to_hub("ID_YOUR_DATASET_NAME")

On push aprés le dataSet a notre compte HuggingFace. **ID_YOUR_DATASET_NAME** est par exemple  *Textra/Textra_Data*

.. figure:: /Documentation/Images/ID_Data.png
   :width: 100%
   :align: center
   :alt: Alternative text for the image
   :name: Compte HuggingFace


.. hint::
   - le DataSet sur HuggingFace pour Exemple des deux images `ici <https://huggingface.co/datasets/Textra/Textra_Data?row=0>`_.




.. video:: _static/Create_Token.mp4
