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
