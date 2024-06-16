LLM modèles
=============

1.Définition
----------------------------

Un grand modèle de langage (LLM) est un type de programme d'intelligence artificielle (IA ) capable, entre autres tâches, de reconnaître et de générer du texte.Les LLM sont entraînés sur des ensembles de données massifs - d'où l'emploi de terme « large » (qui signifie grand) dans la dénomination anglaise « large language model ».Les LLM reposent sur l'apprentissage automatique: en particulier, un type de réseau neuronal appelé modèle de transformateur.
Plus simplement, un LLM est un programme informatique qui a reçu suffisamment d'exemples pour être capable de reconnaître et d'interpréter le langage humain ou d'autres types de données complexes.

2.À quoi servent les LLM ?
----------------------------

Les LLM peuvent être entraînés pour un certain nombre de tâches. L'une des utilisations les plus connues est leur application en IA générative : ils sont capables de produire un texte de réponse à une invite ou une question. Par exemple, le LLM ChatGPT, disponible pour le grand public, peut générer des essais, des poèmes et d'autres formes textuelles en réponse aux entrées de l'utilisateur.
Tout ensemble de données complexes et de grande taille peut être utilisé pour entraîner des LLM, y compris les langages de programmation. Certains LLM peuvent aider les programmeurs à écrire du code. Ils peuvent écrire des fonctions à la demande ou terminer l'écriture d'un programme à partir d'un code qui leur a été donné comme point de départ. Les LLM peuvent également être utilisés pour les besoins suivants :

Analyse des sentiments
Recherche sur l'ADN
Service à la clientèle 
Chatbots
Recherche en ligne
Parmi les exemples de LLM réels, citons ChatGPT (OpenAI), Bard (Google), Llama (Meta) et Bing Chat (Microsoft). Le Copilot de GitHub est un autre exemple, mais pour il s'applique au codage et non au langage humain naturel.

3.Quels sont les avantages et les limites des LLM ? ?
----------------------------------------------------------------

L'une des principales caractéristiques des LLM est leur capacité à répondre à des requêtes imprévisibles. Un programme informatique traditionnel reçoit des commandes dans sa syntaxe acceptée, ou à partir d'un certain ensemble d'entrées de l'utilisateur. Un jeu vidéo dispose d'un ensemble fini de boutons, une application dispose d'un ensemble fini d'éléments sur lequel l'utilisateur peut cliquer ou qu'il peut saisir, et un langage de programmation est composé d'énoncés précis de type « si » et « alors ».
De son côté, un LLM peut répondre à un langage humain naturel et utiliser l'analyse de données pour répondre à une question non structurée ou à une invite d'une manière logique. Alors qu'un programme informatique classique ne reconnaîtrait pas une question telle que « Quels sont les quatre plus grands groupes de funk de l'histoire ? », un LLM peut répondre par une liste de quatre groupes de ce type et exposer un argument convaincant de ce qui en fait les meilleurs.

4.Comment fonctionnent les LLM ?
---------------------------------

Apprentissage automatique et apprentissage en profondeur
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Au départ, les LLM reposent sur l'apprentissage automatique. L'apprentissage automatique est une composante de l'intelligence artificielle, qui consiste à alimenter un programme avec de grandes quantités de données afin de l'entraîner à identifier les caractéristiques de ces données sans intervention humaine.

Les LLM utilisent un type d'apprentissage automatique appelé l'apprentissage en profondeur (Deep learning). Les modèles d'apprentissage en profondeur peuvent concrètement s'entraîner à distinguer les différences, sans intervention humaine, même si un minimum de mise au point humaine est généralement nécessaire.

L'apprentissage en profondeur utilise les probabilités pour « apprendre. » Par exemple, dans la phrase « Le renard brun et rapide a sauté par-dessus le chien paresseux, » les lettres « a » et « e » sont les plus courantes, apparaissant six et dix fois respectivement. Partant de là, un modèle d'apprentissage en profondeur peut conclure (à raison) que ces caractères sont parmi les plus susceptibles d'apparaître dans un texte en anglais.
Soyons réalistes, un modèle d'apprentissage en profondeur ne peut rien conclure à partir d'une seule phrase. Mais après avoir analysé des milliers de phrases, il peut en apprendre suffisamment pour savoir comment terminer de façon logique une phrase incomplète, voire générer ses propres phrases.

Réseaux neuronaux
~~~~~~~~~~~~~~~~~~~~

Afin de permettre ce type d'apprentissage en profondeur, les LLM sont construits sur des réseaux neuronaux.
À l'instar du cerveau humain constitué de neurones qui se connectent et s'envoient des signaux, un réseau 
neuronal artificiel (généralement abrégé en « réseau neuronal ») est constitué de nœuds de réseau qui se 
connectent les uns aux autres. Ils sont composés de plusieurs « couches » : une couche d'entrée, une couche
de sortie et une ou plusieurs couches intermédiaires. Les couches ne se transmettent des informations que si
leurs propres résultats dépassent un certain seuil.

Transformeurs
~~~~~~~~~~~~~~~~~~~~~~~~

Le type spécifique de réseau neuronal utilisé pour les LLM est appelé modèle transformeur. Les modèles transformeurs 
sont capables d'apprendre le contexte, ce qui est particulièrement important pour le langage humain, fortement dépendant
du contexte. Les modèles transformeurs utilisent une technique mathématique appelée auto-attention pour détecter la
manière subtile dont les éléments d'une séquence sont reliés entre eux. Ils sont donc plus à même de comprendre le
contexte que d'autres types d'apprentissage automatique. Ils comprennent, par exemple, comment la fin d'une phrase 
est reliée au début, et comment les phrases d'un paragraphe sont reliées entre elles.


5.Notre cas de figure :
------------------------

Dans la première partie, on a utilisé un modèle de NER `Token classification`, qui fait tout simplement
la classification des tokens en des classes prédéfinies.

**Inconvénients de cette méthode :**

- Faible flexibilité dans le modèle, car il sait seulement les classes qu'il a appris au cours du training, si on veut une autre information sur le document, on ne peut pas !

**Avantages de cette méthode :**

- Le modèle est très petit (ne dépasse pas 500M de paramètres généralement), ce qui le rende économique en termes de ressources.
- Le modèle est fiable, car il classifie juste les classes prédéfinies.

Dans une deuxième approche, on va utiliser un LLM avec sa capacité de comprendre le texte, pour extraire non pas seulement des classes, mais une description complète de documents.
bien précisément on va utiliser le modèle open source `lama3-8b` la dernière version de famille `llama` de `Meta`.

.. note:: 
    - On va adopter cette solution avec un modèle pré-entraîné, sans faire de Finetuning ou RAG `(perspectives futures)`.

.. figure:: /Documentation/Images/LLM_way.png
   :width: 100%
   :align: center
   :alt: Alternative text for the image
   :name: LLM method

**Avantages de cette méthode :**

- Grande flexibilité sur les types des documents ou les informations qu'on peut obtenir.

**Inconvénients de cette méthode :**

- Les modèles sont généralement très grands, ce qui le rende demande des bonnes ressources.
- Le modèle moins fiable, ça reste un modèle de génération de texte.

5.1.Ollama:
~~~~~~~~~~~

.. figure:: /Documentation/Images/ollama_logo.png
   :width: 30%
   :align: center
   :alt: Alternative text for the image
   :name: ollama_logo


L'interface ollama vous facilite l'utilisation des LLMs OpenSource sur votre machine locale. Le guide d'installation `ici <https://ollama.com/>`_.

On va utiliser llma3-8billion paramètres qui demande au mois 8Go sur votre RAM et un CPU de 2 cors, pour s'exécuter 
(Elle va être très lente).

Vous pouvez interagir avec ollama soit a partir de Command prompt sur Windows ou à travers python, on va illustrer les deux.

**Avec Command prompt**

Aprés installation de ollama, sur un cmd vous tapez ollama (pour lancer le serveur ollama), une description des déférentes commandes apparaître.

Vous testez, par exemple

.. code-block:: bash

    ollama run llama3

Une installation va commencer si vous n'avez pas encours installer le modèle. Plus de détail `ici <https://github.com/ollama/ollama?tab=readme-ov-file>`_.

**Avec Python**

On commnece par installer library ollama

.. code-block:: bash

   !pip install ollama

pour utiliser un LLM, c'est simple, juste exécuter les linges suivants :

.. code-block:: python

   import ollama
   response = ollama.chat(model='Model Name', messages=[
   {
      'role': 'user',
      'content': 'Your Prompt',
   },
   ])
   print(response['message']['content'])

- `Model Name` vous tester par exemple `llama3` ou autre.
- `Your prompt` c'est votre message.

.. attention:: 

   - Assurez que le serveur ollama est lancé, sinon vous aurez une erreur de connexion. Pour s'assurer, vous pouvez taper `ollama` après `ollama serve` sur un cmd.
   - Plus de détails `ici <https://github.com/ollama/ollama-python>`_.
   
**Utilisation de llama3 pour notre tache**

Il suffit tout simplement d'ajuster le prompt en ajoutant le texte donné par l'OCR

.. code-block:: python

   import ollama
   response = ollama.chat(model='llama_2', messages=[
   {
      'role': 'user',
      'content': f'Extract main infos  form this invoice text :{Text}',
   },
   ])
   print(response['message']['content'])

- `Text` est un string contient le text donné par Paddle-OCR.

5.2.HuggingFace:
~~~~~~~~~~~~~~~~

On va faire la même chose avec HuggingFace, on va utiliser Phi3 3.8B. Vous pouvez utiliser un autre modèle
mais le code peut changer un petit peu, vous vérifiez toujours dans la description du modèle sur
HuggingFace. `Phi3 <https://huggingface.co/microsoft/Phi-3-mini-4k-instruct>`_.

On commence par installation de quelques bibliothèques.

.. code-block:: bash

   !pip install transformers
   !pip install accelerate

.. code-block:: python

   import torch
   from transformers import AutoModelForCausalLM, AutoTokenizer, pipeline

   torch.random.manual_seed(0)

   model = AutoModelForCausalLM.from_pretrained(
      "microsoft/Phi-3-mini-4k-instruct", # ID of the model from HuggingFace
      device_map="cuda", # The modle will run on a GPU
      torch_dtype="auto", 
      trust_remote_code=True, 
   )
   tokenizer = AutoTokenizer.from_pretrained("microsoft/Phi-3-mini-4k-instruct")


Utilisation du modèle avec un simple prompt.

.. code-block:: python

   messages = [
      {"role": "user", "content": "Why the sky is blue?"}
   ]

   pipe = pipeline(
      "text-generation",
      model=model,
      tokenizer=tokenizer,
   )

   generation_args = {
      "max_new_tokens": 5000,
      "return_full_text": False,
      "temperature": 0.0,
      "do_sample": False,
   }

   output = pipe(messages, **generation_args)
   print(output[0]['generated_text'])

.. raw:: html

   <a href="https://colab.research.google.com/github/MasrourTawfik/Textra/blob/main/Notebooks/LLM_OCR.ipynb" target="_blank"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>


















