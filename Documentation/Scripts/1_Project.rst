Introduction
=============

1.Définition
----------
Notre projet visait à développer une solution à la fois flexible et efficace pour extraire l’information à partir d’une variété de formats de documents. On est concentré sur l’utilisation de l’OCR (Optical Character Recognition) et des modèles à grand langage (LLMs) comme ChatGPT en utilisant les capacités contextuelles avancées des LLM.
L’innovation de cette méthode réside dans son adaptabilité, capable de traiter de nombreux types de documents sans formation approfondie ni règles spécifiques pour chaque format. Notre objectif était de démontrer une stratégie efficace pour l’extraction de données qui pourrait être un point de référence pour les défis similaires rencontrés dans divers contextes d’affaires. 

.. figure:: /Documentation/Images/descr.png
   :width: 100%
   :align: center
   :alt: Alternative text for the image
   :name: Projet

2.Déférentes possibilités
----------------------
Dans cette partie on explore les déférentes possibilités pour extraction  et l'analyse de l'information.
chaque solution avec ces avantages et inconvénients.

2.1.Methodology 1: GPT-4 Vision (GPT-V) by OpenAI
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`GPT-V` se distingue par sa capacité à analyser des images et à fournir des informations détaillées basées sur les requêtes des utilisateurs. Ce modèle permet aux utilisateurs de télécharger une image et de poser des questions spécifiques sur son contenu, auxquelles GPT-V répond avec des informations précises et pertinentes.
Dans le cadre de l’extraction de données à partir d’images, GPT-V offre une solution hautement intuitive et efficace. Le processus est remarquablement simple : vous téléchargez une image sur le modèle, et GPT-V traite cette image pour renvoyer les informations requises dans un format JSON structuré. 
Ces données peuvent ensuite être facilement stockées et récupérées pour une utilisation ultérieure.

**Avantages de l’utilisation de GPT-V :**

- *Simplicité et efficacité* : Le processus de téléchargement d’une image et de réception de données au format JSON est simple, ce qui minimise la complexité généralement associée à l’extraction de données.

- *Haute efficacité* : GPT-V utilise les capacités sophistiquées du modèle GPT-4, assurant une extraction de données précise et fiable à partir d’images.

**Inconvénients de l’utilisation de GPT-V :**

- *Considérations de coût* : L’utilisation de GPT-V peut être coûteuse, en particulier lors du traitement d’images à haute résolution, ce qui peut être un facteur important pour les projets avec des contraintes budgétaires.

- *Préoccupations relatives à l’autonomie des données* : Comme GPT-V est un service tiers, il existe des problèmes inhérents à la confidentialité et au contrôle des données. Cette dépendance envers un fournisseur externe peut poser des défis pour les projets où la sécurité et l’autonomie des données sont primordiales.

- *Latence et limites de débit de l’API* : Il peut y avoir des retards importants dans la réception des informations de l’API, et des limites de débit peuvent être imposées au compte, affectant l’évolutivité et la réactivité du système.

.. code-block:: bash

    pip uninstall -y tensorflow --quiet
    pip install ludwig --quiet
    pip install ludwig[llm] --quiet
    pip install datasets

.. code-block:: python

    from IPython.display import HTML, display

    def set_css():
    display(HTML('''
    <style>
        pre {
            white-space: pre-wrap;
        }
    </style>
    '''))

    get_ipython().events.register('pre_run_cell', set_css)

    def clear_cache():
    if torch.cuda.is_available():
        torch.cuda.empty_cache()






























