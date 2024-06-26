# Distributed Ledger Technology


## Definition

Les ledgers ou les registres distribués représentent une base de données qui a pour but d’être distribuée sur un ou plusieurs réseaux.

Plusieurs réseaux peuvent être impliqués, avec plusieurs noeuds qui traitent et vérifient chaque élément des transactions.



## Implementation

- Blockchain
- Directed acyclic graph - DAG
- Hashgraph

## DAG

### Definition

Un DAG est une structure de données ou “graphes” qui représente en un ensemble de nœuds, également appelés “vertex“, et de “edges” (ou arêtes), qui les relient. 

Ce qui distingue un DAG des autres types de graphes, c'est que les edges ont une direction définie, et qu'il n'y a pas de boucles dans la structure.

### Utilisations

Organigrammes, Arbres généalogiques, pyramide des besoins de Maslow, transactions sécurisées (Chaque transaction est un nœud du graphe.)


## Le trilemme de la blockchain 

- Sécurité
- Scalabilité
- Décentralisation

_Selon Vitalik Buterin, le cofondateur d’Ethereum, il est impossible de concevoir une blockchain qui satisfasse simultanément ces trois critères._

### Exemple

Par exemple, pour améliorer la sécurité, il est possible de réduire la décentralisation en faisant appel à des autorités centrales pour valider les transactions. 
De même, pour améliorer la scalabilité, il est possible de sacrifier la sécurité en utilisant des algorithmes de validation plus rapides mais moins sécurisés.



## Source

DLT : 

https://www.lemagit.fr/definition/Registres-distribues-DLT

https://cryptomaniaks.com/distributed-ledger-technology-for-dummies

Noeud :

https://cryptoast.fr/noeud-cryptomonnaies/

Transaction Bitcoin

https://coinacademy.fr/cours/fonctionnement-complet-dune-transaction-bitcoin/

https://www.pensezblockchain.ca/les-transactions-bitcoin-partie-1

DAG:

https://fr.wikipedia.org/wiki/Graphe_orient%C3%A9_acyclique

https://coinacademy.fr/academie/technologie-dag/


## Lexique

Consensus : Le consensus est un processus qui permet aux différents noeuds du réseau de s’accorder sur l’état du registre.


Noeuds : Ce sont eux qui vérifient et valident les transactions du réseau, et qui, par conséquent, assurent son fonctionnement et sa sécurité.


Réseau : Ensemble de noeuds.


Transaction : Une transaction est une opération qui modifie l'état du registre après avoir été validée et consignée selon le mécanisme de consensus propre au réseau.



Mempool : Le mempool est une structure de données en mémoire au sein d’un noeud dans un registre distribué, qui stocke les transactions candidates avant qu’elles ne soient exploitées.
