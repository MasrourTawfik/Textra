Training
====================================

7.1 Creation de dataSet sur HuggingFace
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

- bbox (les coordonnées des rectangles de chaque labelisation `[xmin,ymin,xmax,ymax]` ) ne sont pas normalisés entre `[100,1000]`.

- Dans la nouvelle forme, on a une liste contient les informations des images, chacune est représentée par un  dictionnaire dont les clés sont `['id', 'image', 'bboxes', 'ner_tags', 'tokens']`
