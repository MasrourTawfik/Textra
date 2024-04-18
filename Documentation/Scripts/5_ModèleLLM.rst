Modèle LLM
=============

1.Définition
----------------------------

Un grand modèle de langage (LLM) est un type de programme d'intelligence artificielle (IA ) capable, entre autres tâches, de reconnaître et de générer du texte.Les LLM sont entraînés sur des ensembles de données massifs - d'où l'emploi de terme « large » (qui signifie grand) dans la dénomination anglaise « large language model ».Les LLM reposent sur l'apprentissage automatique: en particulier, un type de réseau neuronal appelé modèle de transformateur.

Plus simplement, un LLM est un programme informatique qui a reçu suffisamment d'exemples pour être capable de reconnaître et d'interpréter le langage humain ou d'autres types de données complexes. De nombreux LLM sont formés sur des données collectées sur Internet ; des milliers ou des millions de gigaoctets de texte. Mais la qualité des échantillons a une incidence sur l'apprentissage du langage naturel par les LLM, de sorte que les programmeurs d'un LLM peuvent utiliser un ensemble de données mieux structuré.

Les LLM utilisent un type d'apprentissage automatique appelé apprentissage en profondeur (Deep learning) afin de comprendre comment les caractères, les mots et les phrases fonctionnent ensemble. L'apprentissage en profondeur implique l'analyse probabiliste de données non structurées, ce qui permet au modèle d'apprentissage en profondeur de distinguer les différences entre les éléments de contenu sans intervention humaine.

Les LLM sont ensuite entraînés dans le cadre d'un réglage : ils sont réglés avec précision ou avec des invites en fonction de la tâche particulière que le programmeur souhaite leur confier, qu'il s'agisse d'interpréter des questions avant de générer des réponses ou de traduire un texte d'une langue à une autre.

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

Cependant, concerne les informations qu'ils fournissent, les LLM ne seront fiables que si les données qu'ils ingèrent le sont. S'ils reçoivent des informations erronées, les réponses qu'ils donneront aux demandes de l'utilisateur le seront également. Il arrive que les LLM « hallucinent » un peu : ils créent de fausses informations lorsqu'ils ne sont pas en mesure de fournir une réponse précise. Par exemple, en 2022, le magazine Fast Company a interrogé ChatGPT sur le dernier trimestre financier de l'entreprise Tesla ; ChatGPT a certes produit un article cohérent en réponse, cependant une grande partie des informations contenues dans l'article ont été inventées.

En matière de sécurité, les applications destinées aux utilisateurs et basées sur les LLM sont aussi sujettes aux bogues que n'importe quelle autre application. Les LLM peuvent également être manipulés par des intrants malveillants afin de fournir certains types de réponses plutôt que d'autres, y compris des réponses dangereuses ou contraires à l'éthique. Enfin, les LLM posent un certain nombre de problèmes de sécurité liés notamment au fait que les utilisateurs peuvent y importer des données sécurisées et confidentielles afin d'accroître leur propre productivité. Toutefois, pour entraîner leurs modèles, les LLM utilisent les données qu'ils reçoivent, et ils ne sont pas conçus pour être des coffres-forts sécurisés ; il peut arriver qu'ils exposent des données confidentielles en réponse à des requêtes provenant d'autres utilisateurs.

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
Modèles transformeurs
~~~~~~~~~~~~~~~~~~~~~~~~
Le type spécifique de réseau neuronal utilisé pour les LLM est appelé modèle transformeur. Les modèles transformeurs 
sont capables d'apprendre le contexte, ce qui est particulièrement important pour le langage humain, fortement dépendant
du contexte. Les modèles transformeurs utilisent une technique mathématique appelée auto-attention pour détecter la
manière subtile dont les éléments d'une séquence sont reliés entre eux. Ils sont donc plus à même de comprendre le
contexte que d'autres types d'apprentissage automatique. Ils comprennent, par exemple, comment la fin d'une phrase 
est reliée au début, et comment les phrases d'un paragraphe sont reliées entre elles.

Cela permet aux LLM d'interpréter le langage humain, même lorsque ce langage est vague ou mal défini, agencé dans des
combinaisons qu'ils n'ont jamais rencontrées auparavant, ou contextualisé d'une nouvelle manière. Dans une certaine mesure,
ils « comprennent » la sémantique dans le sens où ils peuvent associer des mots et des concepts en fonction de leur signification,
après les avoir vus regroupés de cette manière des millions ou des milliards de fois.
5.Comment les développeurs peuvent-ils rapidement commencer à concevoir leurs propres LLM ? ?
------------------------------------------------------------------------------------------------
Pour concevoir une application LLM, les développeurs ont besoin d'un accès facile à plusieurs ensembles de
données et d'endroits où faire résider ces derniers. Le stockage cloud et le stockage sur site développés 
à ces fins peuvent tous deux impliquer des investissements d'infrastructure hors de portée du budget des 
développeurs. En outre, les ensembles de données d'apprentissage sont généralement stockés à plusieurs 
endroits, mais le transfert de ces données vers un emplacement central peut entraîner des frais de trafic 
sortant considérables.

Heureusement, Cloudflare propose plusieurs services permettant aux développeurs de commencer rapidement à
concevoir des applications LLM et d'autres types d'IA. Vectorize est une base de données vectorielles distribuée à 
l'échelle mondiale qui permet d'interroger des données stockées au sein de systèmes de stockage d'objets sans frais de 
trafic sortant (R2) ou des documents stockés dans le référentiel clé-valeur Workers. En conjonction avec la plateforme de 
développement Cloudflare Workers AI, les développeurs peuvent utiliser Cloudflare pour commencer rapidement leurs expériences 
sur leurs propres LLM.

LLM Models Benchmarking
=========================
Nous avons fait une comparaison entre différents grands modèles de langage, nous avons cité différents modèles en utilisant Hugging Face et LM Studio. 

.. note:: 
   - il faut préparer les données pour chaque modèle pour le Finetuning, ça prend beaucoup de temps et chaque modèle se caractérise par un type des données d'entrée.
   C'est pour cela nous avons utiliser la partie Spaces sur Hugging face.

1.Magorshunov/layoutlm-invoices 
--------------------------------
.. figure:: /Documentation/Images/magorshunov-layoutlm-invoice.png
   :width: 80%
   :align: center
   :alt: Alternative text for the image
   :name: LLM MODEL 

.. note:: 
   - Vous pouvez essayer ce modèle en cliquant `ici <https://huggingface.co/spaces/shalinig/magorshunov-layoutlm-invoices>`_.
2.Faisalraza/layoutlm-invoices 
--------------------------------
.. figure:: /Documentation/Images/faisalraza-layoutlm-invoices.png
   :width: 80%
   :align: center
   :alt: Alternative text for the image
   :name: LLM MODEL 

.. note:: 
   - Vous pouvez essayer ce modèle en cliquant `ici <https://huggingface.co/spaces/Anushk24/faisalraza-layoutlm-invoices>`_.

3.Impira/layoutlm-invoices 
---------------------------
.. figure:: /Documentation/Images/impira-layoutlm-invoices.png
   :width: 80%
   :align: center
   :alt: Alternative text for the image
   :name: LLM MODEL 

.. note:: 
   - Vous pouvez essayer ce modèle en cliquant `ici <https://huggingface.co/spaces/udayzee05/impira-layoutlm-invoices>`_.

4.Invoice header extraction with Donut 
---------------------------------------
.. figure:: /Documentation/Images/donut.png
   :width: 80%
   :align: center
   :alt: Alternative text for the image
   :name: LLM MODEL 

.. note:: 
   - Vous pouvez essayer ce modèle en cliquant `ici <https://huggingface.co/spaces/to-be/invoice_document_headers_extraction_with_donut>`_.

5.Gemini application  
---------------------------------------
.. figure:: /Documentation/Images/gemini.png
   :width: 80%
   :align: center
   :alt: Alternative text for the image
   :name: LLM MODEL 

.. note:: 
   - Vous pouvez essayer ce modèle en cliquant `ici <https://huggingface.co/spaces/pc-17/invoice_extraction>`_.

6.Generative AI / invoice reader
--------------------------------------
.. figure:: /Documentation/Images/generativeAI.png
   :width: 80%
   :align: center
   :alt: Alternative text for the image
   :name: LLM MODEL 

.. note:: 
   - Vous pouvez essayer ce modèle en cliquant `ici <https://huggingface.co/spaces/niladridutta/genai_based_invoice_reader>`_.

7.Invoice Information Extraction using LayoutLMv3 model
----------------------------------------------------------
.. figure:: /Documentation/Images/layoutlmv3.png
   :width: 80%
   :align: center
   :alt: Alternative text for the image
   :name: LLM MODEL 

.. note:: 
   - Vous pouvez essayer ce modèle en cliquant `ici <https://huggingface.co/spaces/Theivaprakasham/layoutlmv3_invoice>`_.


Nous avons réalisé une analyse comparative approfondie de plusieurs modèles de langage de grande envergure (LLM) pour l'extraction de texte à partir de documents. Notre évaluation s'est principalement concentrée sur deux critères essentiels : le temps d'inférence requis par chaque modèle et le poids, ou la taille, de ces modèles. En examinant attentivement ces aspects, nous avons pu classer ces modèles en fonction de leur performance et de leur efficacité dans le contexte de l'extraction de texte. Cette classification nous a fourni des insights précieux sur les forces et les faiblesses de chaque modèle, nous permettant ainsi de prendre des décisions éclairées quant à leur utilisation dans divers scénarios d'application.

- 
    - **Voici une video qui vous aidera à trouver et essayer les modèles**:  |linkedin_mouad|
.. |linkedin_mouad| image:: ../Images/mp4.jpeg
    :width: 16
    :height: 16
    :target: C:\Users\hp\Desktop\Textra\Documentation\Videos\hugging face.mp4





