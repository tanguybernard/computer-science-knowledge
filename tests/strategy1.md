# Strategy


### Introduction

Document de haut niveau définissant, pour un programme, les niveaux de tests à exécuter et les tests dans chacun de ces niveaux (pour un ou plusieurs projets)

###  Scope And Overview

### Test approach

Définir le processus de test, le niveau de test, les rôles et les responsabilités de chaque membre de l'équipe.

#### Types

##### Unitaire

Les tests unitaires sont des tests effectués pour déterminer si les composants individuels du programme fonctionnent conformément aux spécifications de conception.

- Propriétaires: Développeurs principaux correspondants
- Approche de la mise en œuvre: A la discrétion du développeur
- Outils/Techniques: Tests automatisés

##### Integration


Les tests d'integration sont conçus pour tester un groupe de composants.

- Propriétaires: Développeurs principaux correspondants
- Approche de la mise en œuvre: A la discrétion du développeur
- Outils/Techniques: Tests manuels


### Test Environment


- Les développeurs effectuent des tests unitaires dans l'environnement de développement.
- Les tests d'intégration et de système ont lieu dans l'environnement de test.
- Les tests utilisateurs sont effectués dans l'environnement de recette (staging).

Notes :

- L'Identity providers dispose d'un environnement de recette, qui est utilisé pour le développement, les tests, et les environnements de recette.

### Testing tools

- Cypress 
- Jest : Frontend Test
- Postman: Api Test

### Release control

Les tickets doivent passer au statut "Terminé" et être marqués d'un numéro de release avant de pouvoir être publiées.

### Risk Analysis

Les risques potentiels sont les suivants :

- les retards dans le développement
- changements dans les exigences
- les problèmes de compatibilité des navigateurs

## Credits

https://www.softwaretestinghelp.com/writing-test-strategy-document-template/

https://katalon.com/resources-center/blog/test-strategy

https://blog.testlodge.com/wp-content/uploads/2022/06/test-strategy-example-pdf.pdf

https://latavernedutesteur.fr/2019/08/19/politique-strategie-et-plans-de-test/
