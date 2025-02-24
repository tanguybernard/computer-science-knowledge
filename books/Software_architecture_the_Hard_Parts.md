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





