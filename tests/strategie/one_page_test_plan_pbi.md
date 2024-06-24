

## Introduction

Le plan de test est conçu pour prescrire la portée, l'approche, les ressources et le calendrier de toutes les activités de test du projet __Portail d'administration PowerBI__.

Le plan identifie les éléments à tester, les fonctionnalités à tester, les types de tests à effectuer, le personnel responsable des tests, les ressources et le calendrier requis pour réaliser les tests, ainsi que les risques associés au plan.


## Ressource

https://www.ministryoftesting.com/articles/the-one-page-test-plan

Test unitaire: test qui a une raison d'échouer.

Test d'intégration : des modules individuels sont combinés et testés en tant que groupe

## In Scope

Le site web frontal.

Ces systèmes doivent être testés dans les dernières versions stables de Chrome et FireFox (sous entendu: Pas de tests sur : Safari et Microsoft Edge. )

Les systèmes doivent être testés sur une machine Windows.


Le backend.


## Out of scope

- Sur la partie non fonctionnel, aucun test responsive ne sera effectué.
- Aucun test d'accessibilité ne sera effectué.
- Aucun test sur safari ne sera effectué.
- Nous ne ferons aucun test sur une version de chrome anterieur à 120.0.6099.119
- L'application est traduite en anglais, aucun test d'internationalisation ne sera effectué.
- Pas de tests de Sécurité et performances du site Web

## Environnement 

Les tests seront effectués sur les environnements de Staging et de preprod. Navigateur firefox et chrome. Environnement Windows (en local) et Linux._

## Tools

Les outils utilisés sont: Cypress, Jest, Junit

## Roles and Responsabilities

Developpeurs, developpeuses : Tanguy et Oumaima

PO: Nadia

Chef de Projet : Jean-Baptiste


## Risks

- Les tests e2e ne peuvent etre joué que sur notre poste en local.

## Assumptions/ Conditions

- Le service Power BI prepord doit etre up et ISO prod.
- Le service Active Directory doit etre up.
- Le service Ldap doit etre up.



## Testing Tasks


_Ex:_

Préparation
- Identifier le scénario de test à executer
- Identifier les données de tests nécessaires

Développeur

- Développement d'un test e2e avec Cypress (Front + Back + Base de données)
- Developpement de tests d'integration front (Composant front)
- Developpement de tests d'integrations back (controller + useCase + vrai Db)
- Developpement de tests unitaires (useCase + In Memory Db)
- Generation d'un rapports de couvertures

Testeurs

- Developpement de scénario avec Robot Framework
- Generation d'un rapport

PO

- Sur la Preprod, test manuels du PO
- Validation de l'US

