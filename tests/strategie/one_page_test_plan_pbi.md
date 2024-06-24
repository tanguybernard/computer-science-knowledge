

## Introduction

Le plan de test est conçu pour prescrire la portée, l'approche, les ressources et le calendrier de toutes les activités de test du projet __Portail d'administration PowerBI__.

Le plan identifie les éléments à tester, les fonctionnalités à tester, les types de tests à effectuer, le personnel responsable des tests, les ressources et le calendrier requis pour réaliser les tests, ainsi que les risques associés au plan.


## Links

https://www.ministryoftesting.com/articles/the-one-page-test-plan

Test e2e: test d'un use case depuis l'interface

Test d'acceptance: test défini par les 3 amigos répondant au besoin métier défini dans l'US.

Test d'intégration : des modules individuels sont combinés et testés en tant que groupe

Test unitaire: test qui a une raison d'échouer.


## In Scope

Les systemes : site web frontal, backend, base de données

Le site web frontal.

Ces systèmes doivent être testés dans les dernières versions stables de Chrome et FireFox (sous entendu: Pas de tests sur : Safari et Microsoft Edge. )

Les systèmes doivent être testés sur une machine Windows.


- L'api du backend doit répondre aux exigences.
- La logique métier doit etre testé.


## Out of scope

- Aucun test responsive ne sera effectué.
- Aucun test d'accessibilité ne sera effectué.
- Aucun test sur safari ne sera effectué.
- Aucun test sur une version de chrome anterieur à 120.0.6099.119
- L'application est traduite en anglais, aucun test d'internationalisation ne sera effectué.
- Pas de tests de Sécurité et performances du site Web

## Environnement 

Les tests seront effectués sur les environnements de preprod. Navigateur firefox et chrome. Environnement Windows (en local) et Linux._

## Tools

Les outils utilisés sont: 

- Front: Cypress, Jest
- Back: Junit, assertJ

## Roles and Responsabilities

Developpeurs, developpeuses : Tanguy et Oumaima - Développements des tests automatisés.

PO: Nadia - Test manuels du projet sur les environnements de prod et preprod chaque US.

Chef de Projet : Jean-Baptiste - Test sur l'environnement de prod.


## Risks

- Si la preprod power BI tombe certains tests echoueront.
- Certains utilisateurs utiliseront l'application sur mobile, qui n'est pas responsive.

## Requirements 

- Le service Power BI prepord doit etre up et ISO prod.
- Le service Active Directory doit etre up.
- Le service Ldap doit etre up.


## Testing Tasks


Préparation (3 amigos)
- Identifier les scénarios de tests à executer (ex: Example mapping)
- Identifier les données de tests nécessaires

Développeurs/ses

- Développement d'un test e2e avec Cypress (Front + Back + Base de données)
- Developpement de tests d'integration front (Composant front)
- Devloppement de tests unitaire front
- Développment de tests d'acceptance back (useCase + ...)
- Developpement de tests d'integrations back (controller + useCase + vrai Db)
- Developpement de tests unitaires (useCase + In Memory Db)
- Generation d'un rapports de couvertures

Note: 
- Approche TDD: Outside In
- Stratégie de pyramide des tests 

PO
- Sur la Preprod, test manuels du PO
- Validation de l'US
- Test sur prod

