Inference
==========
C'est le temps maintenant de tester notre modèle en utilisant les images que nous avons prises pour le test à partir de HuggingFace ou d'autres images.

.. attention:: 
   - Pour l'inference, on travaille avec **Python 3.10.12**.

.. code-block:: bash

    !pip install -q transformers==4.39.2
    # CUDA 11.8
    !pip install torch==2.2.1 torchvision==0.17.1 torchaudio==2.2.1 --index-url https://download.pytorch.org/whl/cu118
    # CPU only
    #pip install torch==2.2.1 torchvision==0.17.1 torchaudio==2.2.1 --index-url https://download.pytorch.org/whl/cpu

Attention au-dessus pour la deuxième installation, il y a deux cas selon la machine utilisée **(GPU, CPU)**.


.. code-block:: bash

    ## CPU :
    #!pip install paddlepaddle -i https://pypi.tuna.tsinghua.edu.cn/simple
    ## GPU :
    !pip install paddlepaddle-gpu -i https://pypi.tuna.tsinghua.edu.cn/simple

La même remarque ici.

.. code-block:: bash

     !pip install "paddleocr>=2.0.1" # Recommend to use version 2.0.1+
    
.. code-block:: python

    from paddleocr import PaddleOCR
    from PIL import Image, ImageDraw, ImageFont

    ocr = PaddleOCR(use_angle_cls=False,
                lang='fr',
                  rec=False,
                ) # need to run only once to download and load model into memory


ici on Initialise notre OCR, on choisisins la langue francaise avec le parametre **lang**,on vous recommende de découvrir d'autres parametres 
dans la documentation.

.. raw:: html

    <a href="https://pypi.org/project/paddleocr/" target="_blank">
    <img src="https://miro.medium.com/v2/resize:fit:1200/1*qklqV9yl7bw8tzkyhCALNw.png" alt="PaddleOCR" width="200" height="100"/>
    </a>

.. code-block:: python

    labels = ['labl1', 'labe2','...']
    id2label = {v: k for v, k in enumerate(labels)}
    label2id = {k: v for v, k in enumerate(labels)}

Ici on définit la liste **label** contenant nos labels par exemple ['InvNum', 'InvDate', 'Fourni', 'TTC', 'TVA', 'TT', 'autres'], ainsi les deux dictionnaires **id2label** et **label2id**
qu'on aura besoin ultérieurement.

.. code-block:: python

    def processbbox(BBOX, width, height):
        bbox = []
        bbox.append(BBOX[0][0])
        bbox.append(BBOX[0][1])
        bbox.append(BBOX[2][0])
        bbox.append(BBOX[2][1])
        #Scaling
        bbox[0]= 1000*bbox[0]/width # X1
        bbox[1]= 1000*bbox[1]/height # Y1
        bbox[2]= 1000*bbox[2]/width # X2
        bbox[3]= 1000*bbox[3]/height # Y2
        for i in range(4):
            bbox[i] = int(bbox[i])
        return bbox

La fonction **processbbox** fait un traitement sur les BBOX qui va retourner l'OCR, par normalisation et transformation en des entières.

.. code-block:: python

    def Preprocess(Image_path):
        image = Image.open(Image_path)
        image = image.convert("RGB")
        width, height = image.size
        results = ocr.ocr(Image_path, cls=True)
        results = results[0]
        test_dict = {'image': image ,'tokens':[], "bboxes":[]}
        for item in results :
        bbox = processbbox(item[0], width, height)
        test_dict['tokens'].append(item[1][0])
        test_dict['bboxes'].append(bbox)

        print(test_dict['bboxes'])
        print(test_dict['tokens'])
        return test_dict

    
**Preprocess** Prends en paramètre le chemin de l'image, elle commence par lire cette image avec **Image** de la bibliothèque
PIL, l'a transformé en RGB car paddle exige des images RGB, puis exécuté l'OCR sur cette image, extrait les mots détectés avec leurs BBOX ajustées à la taille réelle de l'image, 
puis renvoie un dictionnaire avec les informations suivantes : image, boxes, tokens.


.. code-block:: python

    from transformers import AutoModelForTokenClassification
    from transformers import AutoProcessor
    model_Hugging_path = "MODEL_REPO_ID"
    model = AutoModelForTokenClassification.from_pretrained(model_Hugging_path)

Vous chargez votre modèle identifié par **MODEL_REPO_ID** par exemple **Textra/LayoutLM**. après en exécuter le modèle tout simplement, plus de détails et dans le notebook en bas.

.. code-block:: python

    def unnormalize_box(bbox, width, height):
     return [
         width * (bbox[0] / 1000),
         height * (bbox[1] / 1000),
         width * (bbox[2] / 1000),
         height * (bbox[3] / 1000),
     ]


pour labeliser l'image avec les resultats obtenus , en doit dénormaliser les BBOX

- `predictions = outputs.logits.argmax(-1).squeeze().tolist()`: Cette ligne extrait les prédictions du modèle. Elle applique la fonction `argmax()` pour obtenir l'indice de la classe prédite avec la probabilité la plus élevée, puis utilise `squeeze()` pour éliminer les dimensions inutiles, et enfin, `tolist()` pour convertir les résultats en une liste Python.

.. raw:: html

   <a href="https://colab.research.google.com/github/MasrourTawfik/Textra/blob/main/Notebooks/Inference.ipynb" target="_blank"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>


































