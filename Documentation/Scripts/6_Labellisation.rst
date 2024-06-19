Labellisation 
================
Avant de commencer la labelisation, nous avons classé nos données en 2 catégories : 
- les données d'apprentissage 
- les données pour le test 
 Après il faut installer label-studio pour démarrer la labellisation 

.. figure:: /Documentation/Images/labelstudio.png
   :width: 60%
   :align: center
   :alt: Alternative text for the image
   :name: Prétraitement


1.Les classes de labellisation 
----------------------------------
Pour notre cas, nous avons 7 classes 

.. figure:: /Documentation/Images/classes.jpg
   :width: 70%
   :align: center
   :alt: Alternative text for the image
   :name: Prétraitement

.. note:: 
   - l'entrée de label-studio est json-file
   - c'est pour cela il faut convertir les images ou bien les données d'apprentissage en OCR fichier json pour avoir la possibilité de labeliser

2.Step1 : Setup
---------------------------------------------------

On doit d'abord installer les bibliothèques nécessaires. Sur votre PC,  vous créez une nouvel environnement anaconda
avec python **v3.9.18** avec la commande suivante :

- **Name** : dans le commande est le nom de votre environnement.

.. code-block:: bash

   conda create -n Name python=3.9.18

Aprés vous activez votre environnement :

.. code-block:: bash

   conda activate Name

Installation de paddleOcr, label-Studio sur l'environnement creé

.. code-block:: bash

    #CPU :
    pip install paddlepaddle -i https://pypi.tuna.tsinghua.edu.cn/simple
    ## GPU :
    #!pip install paddlepaddle-gpu -i https://pypi.tuna.tsinghua.edu.cn/simple

.. code-block:: bash

    pip install "paddleocr>=2.0.1"

.. code-block:: bash

    pip install label-studio==1.11.0


3.Step2: Images to OCR json file  
--------------------------------

pour transformer les images en OCR json file, nous avons utiliser le code suivant : 

.. code-block:: python

    # Specify here the path to your training images
    images_folder_path  = "PATH_TRAINING_IMAGES"

.. code-block:: python

    def create_image_url(filename):
       return f'http://localhost:8080/{filename}'

    def convert_bounding_box(bounding_box):
        x1, y1, x2, y2 = bounding_box
        x = min(x1, x2)
        y = min(y1, y2)
        width = x2 - x1
        height = y2 - y1

        return [x, y, width, height]


.. code-block:: python

    def extracted_tables_to_label_studio_json_file_with_paddleOCR(images_folder_path):
        label_studio_task_list = []
        for images in os.listdir(images_folder_path):
                output_json = {}
                annotation_result = []

                print(images)

                output_json['data'] =  {"ocr":create_image_url(images)}

                img = Image.open(os.path.join(images_folder_path,images))

                img = np.asarray(img)
                image_height, image_width = img.shape[:2]

                result = ocr.ocr(img,cls=False)

                #print(result)

                for output in result:

                    for item in output:
                        co_ord = item[0]
                        text = item[1][0]

                        four_co_ord = [co_ord[0][0],co_ord[1][1],co_ord[2][0]-co_ord[0][0],co_ord[2][1]-co_ord[1][1]]

                        #print(four_co_ord)
                        #print(text)

                        bbox = {
                        'x': 100 * four_co_ord[0] / image_width,
                        'y': 100 * four_co_ord[1] / image_height,
                        'width': 100 * four_co_ord[2] / image_width,
                        'height': 100 * four_co_ord[3] / image_height,
                        'rotation': 0
                                }


                        if not text:
                            continue
                        region_id = str(uuid4())[:10]
                        score = 0.5
                        bbox_result = {
                            'id': region_id, 'from_name': 'bbox', 'to_name': 'image', 'type': 'rectangle',
                            'value': bbox}
                        transcription_result = {
                            'id': region_id, 'from_name': 'transcription', 'to_name': 'image', 'type': 'textarea',
                            'value': dict(text=[text], **bbox), 'score': score}
                        annotation_result.extend([bbox_result, transcription_result])
                        #print('annotation_result :\n',annotation_result)
                output_json['predictions'] = [ {"result": annotation_result,  "score":0.97}]

                label_studio_task_list.append(output_json)


        # saving label_stdui_task_list as json file to import in label_studio
        with open("Paddle_Exemple.json", 'w') as f:
            json.dump(label_studio_task_list, f, indent=4)
        f.close()

Exécuter la fonction en haut

.. code-block:: python

    extracted_tables_to_label_studio_json_file_with_paddleOCR(images_folder_path)

3.Step3: Labéliser en label-Studio 
-----------------------------------






l'interface affichée après lancement de label-studio est la suivante : 

.. figure:: /Documentation/Images/Capturelabelstudio.PNG
   :width: 100%
   :align: center
   :alt: Alternative text for the image
   :name: Prétraitement


.. note:: 
   - Vous trouvez ci-joint une video qui montre la procédure de labélisation et de téléchargement de fichier json : 


.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
        <iframe src="https://www.youtube.com/embed/HePK6l6ArNg" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
