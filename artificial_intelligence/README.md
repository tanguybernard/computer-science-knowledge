# Artificial Intelligence

## LLM (Large Language Model)

### Base

C'est un réseau de neurones.

Les mots dans un réseau de neurones, graçe aux vecteurs. Les LLM's font parties des NLP (Natural Language Processing).

Les LLM's permettent de générer du langage naturel.

"Large" car par ex GPT-3 pour s'entrainer à lu 250 milliards de mots.

Prédiction du mot suivant.


Ils sont tous basés sur __l'architecture Transformer.__

### En profondeur

On a une phrase qu'on coupe en __token.__


Le modèle a besoin de comprendre le sens des mots. 

A ce moment la interviens le __Token Embedding__ qui est le  processus de représentation des jetons sous forme de vecteurs continus dans un espace à haute dimension, où les jetons similaires ont des représentations vectorielles similaires. Par exemple Chaise et pouf sont proches, table n'est pas très loin de chaise car 4 pieds...

Ensuite on cherche à positionner le mot dans la phrase, c'est le __Positional embedding__ dans l'architecture Transformer.





## Agent

Un logiciel capable d'agir de manière autonome.

Ex: (L'agence de voyage) Toutes les heures un agent s'execute, il va regarder les différents vols et il vous achète le vol adapter en fonction de vos besoins.


__Un agent IA = LLM + mémoire + objectifs + outils__

## RAG

Donner du contexte à votre LLM.


## Les Structured Outputs

Donne un schéma au LLM pour qu'il réponde en utilisant cette structure (ex: JSON Schema)


## Function Calling (Tools Calling)

Permet à l'IA d'éxecuter du code avec un requete JSON.

Cela lui permet d'agir.


## MCP = Model Context Protocol

Protocol standardisé qui permet aux LLM's d'utiliser des outils (Pour échanger des infos entre des LLMs et des serveurs)



## Sources


### Construire une IA agentique avec les Structured Outputs, Function Calling et MCP ++++ (Très Clair)


https://www.youtube.com/watch?v=sZOFEEhR4QY

Comment ça fonctionne ?

https://www.youtube.com/watch?v=47BlShlc4E8
