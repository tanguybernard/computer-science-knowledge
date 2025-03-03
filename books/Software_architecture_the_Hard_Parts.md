# Software Architecture The Hard Parts - My Notes

## Chapitre 2 Discerning Coupling in Software Architecture (Quantum, Quanta)

- Chaque quantum représente une unité déployable distincte au sein d'une architecture particulière.
- Le couplage statique fait référence aux dépendances structurelles entre les composants au moment de la compilation ou du déploiement. Il s'agit d'un couplage visible dans le code source. (Un service qui appel un autre directeement, l'appel direct à une base de données...).
- Le couplage dynamique concerne la manière dont les composants interagissent en temps d’exécution. (Communication, consistance, coordination)


Dans une Service-based architecture il n'y a qu'un quantum, car meme il existe plusieurs services qui servent un front et qui utilise qu'une seul base, tout est lié donc c'est un quantum complet.

Meme si on deploie le front à part, la base et les services à part, ils ont besoin les uns des autres pour fonctionner.

Pour qu'une architecture possède 2 quanta par exemple. Il faut que les 2 quantas et leur propres bases et que leurs services communiques de manières asynchrone.

Dans une archi microservices, si une interface call une APi Gateway par exemple en synchrone qui call les microservices derrières alors cela ce réduit à un quantum, donc encore une fois une seule unité déployable car ils dépendent du frontend pour fonctionner.


Pour répondre à cette problématique on peut utiliser des microfrontend, une interface qui call un service liés à une seule base de données. 
Dans le bouquin on voit 4 de services ayant cette disposition (un front, un service, un db) qui forment des quanta d'architecture.
Et chacun de ces services peut avoir des caractéristiques d'architecture différentes.

## Chapitre 3 - Architectural Modularity

- La maintenabilité concerne la facilité d'ajouter, de modifier ou de supprimer des fonctionnalités, ainsi que d'appliquer des changements internes tels que des correctifs de maintenance, des mises à niveau du framework, des mises à niveau de tiers, etc.
- La testabilité est définie comme la facilité des tests (généralement mis en œuvre par le biais de tests automatisés) ainsi que l'exhaustivité des tests.
- La déployabilité n'est pas seulement une question de facilité de déploiement, mais aussi de fréquence de déploiement et de risque global de déploiement.


Scalabilité et élasticité :

Bien que la scalabilité et l'élasticité s'améliorent toutes deux avec des services plus fins, l'élasticité est davantage fonction de la granularité (la taille d'une unité de déploiement), tandis que la scalabilité est davantage fonction de la modularité (la décomposition des applications en unités de déploiement distinctes).


L'élasticité repose sur le fait que les services ont un temps moyen de démarrage (mean time to startup - MTTS) très court, ce qui est possible d'un point de vue architectural grâce à des services très petits et à granularité fine.


Si vous devez les déployer sequentiellement apres avoir passé en microservices, retourner faire du monolithe.

## Chapitre 4 




