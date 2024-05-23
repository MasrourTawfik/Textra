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
1.L'installation de label-studio en utilisant pip
---------------------------------------------------
.. code-block:: bash

   !pip install label-studio

2.Les classes de labellisation 
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

3.Images to OCR json file : 
----------------------------

pour transformer les images en OCR json file, nous avons utiliser le code suivant : 

.. code-block:: python

 import os
 from paddleocr import PaddleOCR
 from PIL import Image, ImageDraw, ImageFont
 import json
 from uuid import uuid4
 import numpy as np


 #loading the engine
 #OCR enginer
 ocr = PaddleOCR(use_angle_cls=False, 
                lang='fr',
                  rec=False,
                ) # need to run only once to download and load model into memory 


 images_folder_path  = r"C:\Users\hp\Desktop\Textra_Code\preprocess\DataTraining\Noureddine" 

.. code-block:: python

 def create_image_url(filename):
    return f'http://localhost:8080/{filename}'

.. code-block:: python    

 def convert_bounding_box(bounding_box):
    x1, y1, x2, y2 = bounding_box
    x = min(x1, x2)
    y = min(y1, y2)
    width = x2 - x1
    height = y2 - y1

    return [x, y, width, height]

.. code-block:: python

 def create_image_url(filename):
    return f'http://localhost:8080/{filename}'

.. code-block:: python

 def extracted_tables_to_label_studio_json_file_with_paddleOCR(images_folder_path):
    label_studio_task_list = []
    for images in os.listdir(images_folder_path):
        if images.endswith('.jpg'):
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
    with open("Paddle_Noureddine.json", 'w') as f:
        json.dump(label_studio_task_list, f, indent=4)
    f.close()

 extracted_tables_to_label_studio_json_file_with_paddleOCR(images_folder_path)


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
        <iframe src="https://youtu.be/HePK6l6ArNg" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
