# One Page Test Plan

https://www.cloudnetcare.fr/2022/06/29/plan-de-test/

https://www.infometis.ch/blog/one-page-test-plan

https://metroretro.io/templates/one-page-test-plan

https://www.guru99.com/test-plan-for-project.html?utm_campaign=click&utm_medium=referral&utm_source=relatedarticles#13

https://www.javatpoint.com/test-plan

## Introduction

Introduction/contexte/objectifs : Décrivez le contexte de vos activités de test, le produit, ou les principaux objectifs de votre projet de test.

_Ex: MyAdmin est une application web qui permet de suivre la saisie du CRA de ses colaborateurs_

## Strategy

Stratégie : Quelle stratégie de test sera principalement appliquée ?

_Ex: Nous allons suivre la pyramide des tests_


Note: Il peut etre bon de rappeler la definition des types de tests.

Ex: Test unitaire: test qui a une raison d'échouer.

Ex: Test d'intégration : des modules individuels sont combinés et testés en tant que groupe

## In Scope

Dans le champ d'application : il est de la plus haute importance d'être clair sur le champ d'application de votre test, afin que vous puissiez vous concentrer facilement et efficacement sur ces domaines.


EX: 
- Sur la partie fonctionnel nous allons tester chaque fonctionnalités.
- Sur la partie technique, des tests de sécurités et de performances seront effectués.
- Des tests d'acceptance seront effectués par un groupe d'utilisateurs finaux, selectionnés.


## Out of scope

Hors du champ d'application : il est tout aussi important de définir les aspects qui ne doivent pas être pris en compte dans votre projet de test. En procédant ainsi, vous évitez de perdre du temps et des ressources, et vous pouvez être sûr d'atteindre les objectifs fixés. Vous pouvez par exemple exclure certains aspects des tests non fonctionnels, tels que la portabilité ou la fiabilité, s'ils ne font pas partie de votre mission de test.


Ex:

- Sur la partie non fonctionnel, aucun test responsive ne sera effectué.
- Aucun test d'accessibilité ne sera effectué.
- Aucun test sur safari ne sera effectué.
- Nous ne ferons aucun test sur une version de chrome anterieur à 120.0.6099.119
- L'application est traduite en anglais, aucun test d'internationalisation ne sera effectué.

## Environnement 

Spécifier les parties clés de l'environnement nécessaires à la réalisation des tâches de test ou à la réalisation de vos objectifs, par exemple le système sous test, la génération des données de test, la manipulation des données sensibles, la gestion des accès, etc.

_Ex: Les tests seront effectués sur les environnements de Staging et de preprod. Navigateur firefox et chrome. Environnement Windows (en local) et Linux._

## Tools

Outils : Dans cette section, vous pouvez lister les outils essentiels que vous utilisez dans les processus centraux de votre projet de test.

_Ex: Les outils utilisés sont: Cypress, Jest, Junit, TestContainers, Robot Framework_

## Roles and Responsabilities

Description détaillée des rôles et responsabilités des différents membres de l'équipe, par exemple:

- QA Analyst
- Test Manager
- Developers


## Risks & Issues

Documenter les risques et les problèmes

Ex:
- Des délais stricts
- Des estimations budgétaires insuffisantes ou inexactes
- Une mauvaise gestion
- Des problèmes avec le code
- Changements dans l'environnement de l'entreprise
- Ressources limitées pour les tests
- Retards imprévus pendant les tests
- La machine de Staging n'est pas iso Prod



## Bonus: Testing Tasks

Mentionnez toutes les tâches que vous prévoyez d'effectuer dans le cadre de vos efforts de test. Mentionnez les types de tests.

_Ex:_

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






