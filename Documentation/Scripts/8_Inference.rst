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
    <img src="/Documentation/Images/Exemple_Images.png" alt="PaddleOCR" width="200" height="100"/>
    </a>















