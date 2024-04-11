Prétraitement des images 
=========================

4.1 Qu'est-ce que le prétraitement des images ?
-------------------------------------------
Avant d'être utilisées pour l'entraînement et l'inférence de modèles, les images doivent d'abord subir un prétraitement. Cela inclut, mais n'est pas limité à, des ajustements de la taille, de l'orientation et de la couleur. L'objectif du prétraitement est d'améliorer la qualité de l'image afin de pouvoir l'analyser plus efficacement. Le prétraitement nous permet d'éliminer les distorsions indésirables et d'améliorer des qualités spécifiques qui sont essentielles pour l'application sur laquelle nous travaillons. Ces caractéristiques peuvent changer en fonction de l'application. Une image doit être prétraitée pour que le logiciel puisse fonctionner correctement et produire les résultats souhaités.

.. figure:: /Documentation/Images/prétraitement.png
   :width: 80%
   :align: center
   :alt: Alternative text for the image
   :name: Prétraitement

4.2 Pourquoi est-ce important ?
-------------------------------
Pour préparer les données d'image à l'entrée du modèle, un prétraitement est nécessaire. Par exemple, les couches entièrement connectées des réseaux neuronaux convolutifs exigent que toutes les images soient dans des tableaux de la même taille.

En outre, le prétraitement du modèle peut réduire le temps d'apprentissage du modèle et accélérer l'inférence du modèle. Si les images d'entrée sont très volumineuses, le fait de réduire la taille de ces images diminuera considérablement le temps nécessaire à l'entraînement du modèle sans affecter de manière significative les performances du modèle. 

Même si les transformations géométriques des images (comme la rotation, la mise à l'échelle et la translation) sont classées parmi les techniques de prétraitement, l'objectif du prétraitement est d'améliorer les données de l'image en supprimant les distorsions involontaires ou en améliorant certaines caractéristiques de l'image cruciales pour le traitement ultérieur.

4.3 les caractéristiques à corriger 
-----------------------------------

4.3.1 Le Contraste
~~~~~~~~~~~~~~~~~~~~
.. figure:: /Documentation/Images/contrast.jpg
   :width: 80%
   :align: center
   :alt: Alternative text for the image
   :name: Prétraitement

Le contraste est une caractéristique d'image définissant la différence entre les parties claires et foncées.

.. code-block:: python

 import cv2
 import matplotlib.pyplot as plt

.. code-block:: python

 def enhance_contrast(image, factor):
    lab = cv2.cvtColor(image, cv2.COLOR_BGR2LAB)
    l, a, b = cv2.split(lab)
    clahe = cv2.createCLAHE(clipLimit=factor, tileGridSize=(8, 8))
    l = clahe.apply(l)
    lab = cv2.merge((l, a, b))
    enhanced = cv2.cvtColor(lab, cv2.COLOR_LAB2RGB)
    return enhanced

4.3.2 La luminosité
~~~~~~~~~~~~~~~~~~~~~~
.. figure:: /Documentation/Images/brightness.jpg
   :width: 80%
   :align: center
   :alt: Alternative text for the image
   :name: Prétraitement

.. code-block:: python

 import cv2
 import matplotlib.pyplot as plt

.. code-block:: python

 def enhance_brightness(image, factor):
    enhanced = cv2.convertScaleAbs(image, alpha=factor, beta=0)
    enhanced = cv2.cvtColor(enhanced, cv2.COLOR_BGR2RGB)
    return enhanced
4.3.3 Image inversée
~~~~~~~~~~~~~~~~~~~~~~
.. figure:: /Documentation/Images/inversée.png
   :width: 80%
   :align: center
   :alt: Alternative text for the image
   :name: Prétraitement

.. code-block:: python

 inverted_image = cv2.bitwise_not(img)
 cv2.imwrite("temp/inverted.jpg", inverted_image)

.. code-block:: python

 display("temp/inverted.jpg")

4.3.4 Binarisation
~~~~~~~~~~~~~~~~~~~~~~
.. figure:: /Documentation/Images/outputb.png
   :width: 80%
   :align: center
   :alt: Alternative text for the image
   :name: Prétraitement

.. code-block:: python

 def grayscale(image):
   return cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

 gray_image = grayscale(img)
 cv2.imwrite("temp/gray.jpg", gray_image)
 display("temp/gray.jpg")



.. code-block:: python

 thresh, im_bw = cv2.threshold(gray_image, 210, 230, cv2.THRESH_BINARY)
 cv2.imwrite("temp/bw_image.jpg", im_bw)
 display("temp/bw_image.jpg")

4.3.5 Suppression du bruit
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. figure:: /Documentation/Images/supp.png
   :width: 80%
   :align: center
   :alt: Alternative text for the image
   :name: Prétraitement

.. code-block:: python

 def noise_removal(image):
    import numpy as np
    kernel = np.ones((1, 1), np.uint8)
    image = cv2.dilate(image, kernel, iterations=1)
    kernel = np.ones((1, 1), np.uint8)
    image = cv2.erode(image, kernel, iterations=1)
    image = cv2.morphologyEx(image, cv2.MORPH_CLOSE, kernel)
    image = cv2.medianBlur(image, 3)
    return (image)



.. code-block:: python

 no_noise = noise_removal(im_bw)
 cv2.imwrite("temp/no_noise.jpg", no_noise)
 display("temp/no_noise.jpg")

4.3.6 Rotation / redressement
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. figure:: /Documentation/Images/rotation.png
   :width: 80%
   :align: center
   :alt: Alternative text for the image
   :name: Prétraitement

.. code-block:: python

 #https://becominghuman.ai/how-to-automatically-deskew-straighten-a-text-image-using-opencv-a0c30aed83df
 import numpy as np
 def getSkewAngle(cvImage) -> float:
    # Prep image, copy, convert to gray scale, blur, and threshold
    newImage = cvImage.copy()
    gray = cv2.cvtColor(newImage, cv2.COLOR_BGR2GRAY)
    blur = cv2.GaussianBlur(gray, (9, 9), 0)
    thresh = cv2.threshold(blur, 0, 255, cv2.THRESH_BINARY_INV + cv2.THRESH_OTSU)[1]

    # Apply dilate to merge text into meaningful lines/paragraphs.
    # Use larger kernel on X axis to merge characters into single line, cancelling out any spaces.
    # But use smaller kernel on Y axis to separate between different blocks of text
    kernel = cv2.getStructuringElement(cv2.MORPH_RECT, (30, 5))
    dilate = cv2.dilate(thresh, kernel, iterations=2)

    # Find all contours
    contours, hierarchy = cv2.findContours(dilate, cv2.RETR_LIST, cv2.CHAIN_APPROX_SIMPLE)
    contours = sorted(contours, key = cv2.contourArea, reverse = True)
    for c in contours:
        rect = cv2.boundingRect(c)
        x,y,w,h = rect
        cv2.rectangle(newImage,(x,y),(x+w,y+h),(0,255,0),2)

    # Find largest contour and surround in min area box
    largestContour = contours[0]
    print (len(contours))
    minAreaRect = cv2.minAreaRect(largestContour)
    cv2.imwrite("temp/boxes.jpg", newImage)
    # Determine the angle. Convert it to the value that was originally used to obtain skewed image
    angle = minAreaRect[-1]
    if angle < -45:
        angle = 90 + angle
    return -1.0 * angle
 #Rotate the image around its center
 def rotateImage(cvImage, angle: float):
    newImage = cvImage.copy()
    (h, w) = newImage.shape[:2]
    center = (w // 2, h // 2)
    M = cv2.getRotationMatrix2D(center, angle, 1.0)
    newImage = cv2.warpAffine(newImage, M, (w, h), flags=cv2.INTER_CUBIC, borderMode=cv2.BORDER_REPLICATE)
    return newImage



.. code-block:: python

 #Deskew image
 def deskew(cvImage):
    angle = getSkewAngle(cvImage)
    return rotateImage(cvImage, -1.0 * angle)
 fixed = deskew(new)
 cv2.imwrite("temp/rotated_fixed.jpg", fixed)
 display("temp/rotated_fixed.jpg")