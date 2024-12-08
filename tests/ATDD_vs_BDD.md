

## ATDD

L’ATDD est souvent la première étape du TDD et du Test First en général, en commençant par un premier cas de test de plutôt haut niveau, qui est un test d’acceptation.

- ATDD définit les attentes métier avant tout développement.
- Le client vient prêter assistance à l’équipe technique pour l’implementation.

Note: Ce cas de test est automatisé sinon en général on n’appelle pas ça ATDD.



## BDD

- Collaboration entre toutes les parties prenantes, y compris les utilisateurs finaux.
- On se concentre sur les __comportements utilisateur__ ou système.

En BDD la finalité n'est pas les tests, la finalités c'est la compréhension par l'exemple, par des scénarios.

#Example Mapping


## ATDD VS BDD

- ATDD est plus focalisé sur la validation des critères d’acceptation
- BDD se concentre sur la définition du comportement du logiciel



## Example Mapping

### 1ere approche

Il y a un mode qu’on pourrait qualifier de “revue de spec” : le PO débarque avec les cartes de règles déjà faites, il les pose sur la table, on écrit ensemble les cartes d’exemple, on challenge ensemble les règles, éventuellement on les ajuste en mode 3 Amigos. Là, on fait du SpecByExample.

### 2eme approche : Vrai BDD

On arrive avec juste le besoin (la carte racine de la Map) et on se pose la question des Exemples : quand on est dans telle situation, qu’est-ce qu’il devrait logiquement arriver ? Et ainsi de suite, pour chaque exemple de situation, on décide du bon comportement à adopter. Et les cartes de __Règles__, finalement, elles __émergent à partir de ces exemples__. Quand on utilise l’Example Mapping comme ça, où les règles émergent des exemples plutôt que d’avoir des exemples qui illustrent des règles déjà fixées, alors là vous faites du BDD — du vrai BDD : Behavior-Driven Development.

source: https://jp-lambert.me/tdd-atdd-bdd-et-plus-522bd71ab64e



