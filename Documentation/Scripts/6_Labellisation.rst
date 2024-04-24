labellisation 
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
   - c'est pour cela il faut convertir les images ou bien les données d'apprentissage en fichier json pour avoir la possibilité de labeliser  

l'interface affichée après lancement de label-studio est la suivante : 

.. figure:: /Documentation/Images/Capturelabelstudio.PNG
   :width: 100%
   :align: center
   :alt: Alternative text for the image
   :name: Prétraitement

