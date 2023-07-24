# Computer Science Knowledge

# WORK IN PROGRESS


## Cloud 

Le cloud n’est pas une entité physique, mais un vaste réseau de serveurs distants éparpillés tout autour de la planète, 
reliés entre eux, et destinés à fonctionner comme un écosystème unique. 
 
Ces serveurs sont conçus pour stocker et gérer des données, exécuter des applications, ou fournir du contenu ou des services.


Le cloud computing possède trois principaux modèles de service cloud : l'IaaS (Infrastructure as a Service), le PaaS (Platform as a Service). et le SaaS (Software as a Service).

### Iaas

Le provider (fournisseur) fournit

-  le stockage
-  la mise en réseau
-  la virtualisation

Le client (vous) est responsables :

- du système d'exploitation
- du middleware
- des machines virtuelles
- de toutes les applications ou données

Exemple: AWS (EC2), Microsoft Azure (VM) 

### Caas

Le CaaS (Containers as a Service) fournit et gère toutes les ressources matérielles et logicielles permettant de développer et de déployer des applications à l'aide de conteneurs.

Le fournisseur de services cloud met à disposition :

- l'environnement de création d'applications conteneurisées
- le déploiement d'applications conteneurisées

Les clients doivent :
- écrir le code
- gérer leurs données
- gérer leurs applications


### Paas

La plateforme en tant que service (PaaS) implique que des tiers fournissent une plateforme combinée, comprenant à la fois du matériel et des logiciels. Le modèle PaaS permet aux utilisateurs finaux de développer, de gérer et d'exécuter leurs propres applications, tandis que le fournisseur de la plateforme gère l'infrastructure. Outre le stockage et d'autres ressources informatiques, les fournisseurs proposent généralement un ensemble d'outils pour le développement, le test et le déploiement des applications.

Exemple:

Azure SQL Database is a fully managed platform as a service (PaaS) database engine that handles most of the database management functions such as upgrading, patching, backups, and monitoring without user involvement.

### Faas

// TODO

### Saas

Le saas met à disposition des applications "pretes à l'emploi" (exemple: Gmail).


### Iaas, Paas, Saas

#### Components

Par exemple, si tu veux faire un site comme lafibre.info il y a 4 composants:

L'OS puis au dessus tourne un serveur web (Apache) qui appelle un interpréteur Php (qui exécute des pages php donc ce qui produit des pages html envoyés par le serveur Apache aux clients). Le code Php fait des appels a une base SQL pour lire/stocker les données (messages du forums) de façon à  avoir une persistance (stockage). La base SQL n'est pas forcement sur le meme serveur physique et il peut même y avoir plusieurs serveurs Apache (pour les gros sites notamment). Le code php est fournit pas SMF (Simple Machines Forum).

En mode IaaS, c'est a toi de gérer tout sauf le matériel.

En mode PaaS, un prestataire peut s'occuper pour toi de l'OS, d'Apache+PhP et de la base SQL. TU n'a qu'a founir le code php et gérer la conf du serveur Apache et de la base SQL. le prestataire s'occupe des installations, mises jour, déplacement si matériel en panne, backup, etc

Tu peux vouloir que déléguer la base SQL et pas le serveur web par exemple.

En mode SaaS, le prestataire va tout gérer y compris l'installation de SMF, t'aura plus qu'a t'en servir.

source: https://lafibre.info/datacenter/paas-cest-quoi/

#### Details

##### Middleware

L'intergiciel gère les services communs et les utilitaires tels que la messagerie, la gestion des API, le flux de données et l'authentification.

English : Middleware handles the common services and utilities like messaging, API management, data streaming, and authentication.

Middleware : API, RPC, Messaging

##### Runtime environment

L'environnement d'exécution fournit des facilités communes au système d'exploitation pour que les applications conçues dans un langage de programmation particulier fonctionnent sans heurts.

Runtime Env : JRE (Java Runtime Environment), Node

https://www.mongodb.com/cloud-explained/paas-platform-as-a-service


### Credits

https://azure.microsoft.com/fr-fr/resources/cloud-computing-dictionary/what-is-the-cloud

https://cloud.google.com/learn/paas-vs-iaas-vs-saas?hl=fr

https://cloudnativenow.com/topics/cloudnativedevelopment/caas-vs-paas-whats-right/
