# Computer Science Knowledge


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

### Caas

Le CaaS (Containers as a Service) fournit et gère toutes les ressources matérielles et logicielles permettant de développer et de déployer des applications à l'aide de conteneurs.

Le fournisseur de services cloud met à disposition :

- l'environnement de création d'applications conteneurisées
- le déploiement d'applications conteneurisées

Les clients doivent :
- écrir le code
- gérer leurs données
- gérer leurs applications


### Caas vs Paas

 Les composants essentiels d'un CaaS comprennent des services de conteneurs de base, un catalogue d'images appelé "registry", un logiciel de gestion de clusters 
 et un ensemble d'outils et d'API pour les développeurs. 

Il manque certains éléments dans le caas qui amenerai plus de flexibilité. Et c'est là qu'intervient le Paas.

Un PaaS comprends des fonctionnalités telles que la haute disponibilité, la mise à l'échelle automatique, le routage du trafic, la journalisation, la sécurité, la gestion du cycle de vie des applications, l'automatisation de l'infrastructure et bien d'autres.

Toutefois avec le Paas il y a des inconvénients :

- moins de contrôle sur les opérations et l'infrastructure globale
- personnalisations plus limitées


### Faas

//TODO

### Saas

//TODO

### Credits

https://azure.microsoft.com/fr-fr/resources/cloud-computing-dictionary/what-is-the-cloud

https://cloud.google.com/learn/paas-vs-iaas-vs-saas?hl=fr

https://cloudnativenow.com/topics/cloudnativedevelopment/caas-vs-paas-whats-right/
