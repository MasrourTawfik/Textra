OCR
=================
3.1 C'est quoi OCR ?
--------------------
OCR signifie Reconnaissance Optique de Caractères. C'est la technologie qui permet aux logiciels de reconnaître du texte dans des images ou des documents numérisés, 
et de le convertir en données modifiables et recherchables

3.2 Comment ca fonctionne ?
---------------------------
.. figure:: /Documentation/Images/OCR.jpg
   :width: 100%
   :align: center
   :alt: Alternative text for the image
   :name: OCR
La reconnaissance optique de caractères (OCR) implique plusieurs étapes pour convertir des images de texte en texte éditable:

- **Prétraitement de l'image:** L'image est nettoyée pour améliorer la qualité et la lisibilité du texte. Cela peut inclure des opérations telles que la normalisation des couleurs, la suppression du bruit et l'amélioration du contraste.
- **Détection des régions d'intérêt:** Les zones de l'image contenant du texte sont identifiées à l'aide de techniques de détection d'objets ou de segmentation d'image.
- **Reconnaissance des caractères:** Les caractères individuels dans les régions d'intérêt sont identifiés à l'aide de modèles de reconnaissance de forme ou de réseaux de neurones convolutifs (CNN) pour reconnaître les formes des lettres et des chiffres.
- **Post-traitement:** Une fois les caractères reconnus, des techniques de traitement du langage naturel peuvent être utilisées pour améliorer la précision de la reconnaissance en tenant compte du contexte et de la grammaire.

3.3 OCR Bechmarking:
---------------------
3.3.1 EasyOCR
~~~~~~~~~~~~~~~
est un logiciel de reconnaissance optique de caractères (OCR) open-source développé
en Python. Il permet de convertir des images ou des fichiers PDF contenant du texte en texte
éditable et recherchable. EasyOCR est conçu pour être facile à utiliser et offre une bonne
précision de reconnaissance pour plusieurs langues, y compris des langues asiatiques comme le
chinois, le japonais et le coréen. Il prend en charge plusieurs plates-formes, notamment Windows,
macOS et Linux, et peut être intégré dans des applications grâce à une interface simple et des
fonctionnalités avancées telles que la détection de langage automatique, la segmentation de texte
et la reconnaissance de mise en page.

.. code-block:: python

 import pandas as pd
 import matplotlib.pyplot as plt
 import cv2
 from PIL import Image, ImageDraw, ImageFont
 import numpy as np

.. code-block:: python

 def Plot_EsyOCR(image_path, results, Threshold,Time,text_size=20):
    img = cv2.imread(image_path)
    font = cv2.FONT_HERSHEY_SIMPLEX
    for detection in results:
      if detection[2] >= Threshold:
          bbox = detection[0]
          text = detection[1]
          conf = detection[2]
          x1, y1 = bbox[0]
          x2, y2 = bbox[1]
          #cv2.rectangle(img, (int(x1), int(y1)), (int(x2), int(y2)), (0, 0, 150), 2)
          cv2.putText(img, f"{text}", (int(x1), int(y1) - 10), font,0.7, (0, 0, 255), 2)
          cv2.putText(img, f"{conf:.2f}", (int(x1), int(y1)-30), font, 0.7, (255, 0, 0), 2)

    # Display the image using matplotlib
    img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    plt.figure(figsize=(16, 16))
    plt.imshow(img_rgb)
    plt.axis('off')
    plt.title(f"EasyOCR : {Time} seconds")
    plt.show()
.. code-block:: python
    import easyocr
    import time
    from PIL import Image, ImageDraw, ImageFont
    reader = easyocr.Reader(['fr'],gpu = False)
.. code-block:: python
 start_time = time.time()

 results = reader.readtext(Image_path)

 end_time = time.time()

 Time = end_time - start_time
 Plot_EsyOCR(Image_path,results,0.9,round(Time))
 #df = pd.DataFrame(results,columns=['bbox','text','conf'])
























