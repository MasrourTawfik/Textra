Creation de dataSet sur HuggingFace 
====================================
pour la suite on va  prendre comme exemple les deux images suivantes:

.. figure:: /Documentation/Images/Exemple_Images.png
   :width: 100%
   :align: center
   :alt: Alternative text for the image
   :name: Exemple_Images

Aprés labelisation de vos images et obtenir le fichier json,de cette `forme <https://github.com/MasrourTawfik/Textra/blob/main/Codes/Exemple/Exemple_Training.json#L2>`_.
.. hint::
   Le json est de forme d'une liste contenait deux dictionnaires, chacun pour une image
   on a pris que deux images à titre d'exemple, mais vous allez utiliser plusieurs.
   
7.1 Preparation de fichier json
-------------------------------
Le fichuer obtenue jusqu'à maintenent n'est pas encore compatible avec la forme qui accepte la famille des models LayoutLM
parmi ces non compatibilités :
- bbox (les coordonnées des rectangle de chaque labelisation [xmin,ymin,xmax,ymax] ) ne sont pas normalisés entre [100,1000].
- 
