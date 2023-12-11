# Plan

Norme IEEE 829

## 1. Identifiant (Test Plan Identifier)

Historique

|Version            | Auteur          | Description              | Date         |
| :---------------: |:---------------:|: -----------------------:|: -----------:|
| v1.0.0            |  Tanguy Bernard |  Initialisation document | 11 dec. 2023 |
|                   |                 |                          |              |


## 2. Les références

-- Ici Bibliographie

## 3. Introduction

Le plan de test est conçu pour prescrire la portée, l'approche, les ressources et le calendrier de toutes les activités de test du projet __Portail d'administration__.

Le plan identifie les éléments à tester, les fonctionnalités à tester, les types de tests à effectuer, le personnel responsable des tests, les ressources et le calendrier requis pour réaliser les tests, ainsi que les risques associés au plan.

## 4. Éléments de test (Test Items)

Les systèmes à tester comprennent le site web frontal destiné aux clients.

Ces systèmes doivent être testés dans les dernières versions stables de Chrome et FireFox (sous entendu: __Pas de tests sur :__ Safari et Microsoft Edge. )

Les systèmes doivent être testés sur une machine Windows.

## 5. Caractéristiques à tester

- En tant que Super Admin je peux accéder à tous les espaces métiers
- En tant que Super Admin je peux accéder à l'espace d'administration
- En tant que Super Admin je peux créer un role Admin d'Esapce
- En tant que Super Admin je peux assigner à un Admin d'Esapce, des espaces
- En tant qu'admin d'espace je peux accéder aux espaces qui m'ont été assigné


## 6. Caractéristiques à exclure des tests

Ces fonctionnalités ne sont pas testées car elles ne sont pas incluses dans les spécifications logicielles requises :

- Pas de tests sur la responsivité
- Sécurité et performances du site Web


## 7. Approche du test

Sur chaque US un exemple de test sera écrit. Le développeur implementera le test et le jouera.

Le PO devra tester l'US et le marqué comme Validé, Ignoré ou Echoué.

Lorsque les tests sont marqués comme étant en échec, des rapports de bogues seront automatiquement créés dans Jira.

## 8. Critères de réussite/échec


## 9. Produits livrables du test

Un rapport de couverture de test sera produit.

## 10. Tâches de test

Les activités suivantes doivent être réalisées :
- Préparation du plan de test.
- Les spécifications fonctionnelles sont rédigées et remises à l'équipe chargée des tests.
- L'environnement doit être prêt pour les tests (données de test, identifiants de connexion, informations de paiement, etc.)
- Effectuer les tests.
- Préparer le rapport de synthèse des tests.

## 11. Besoins environnementaux

Un environement de recette est mis à disposition.

## 12. Responsabilités

- Le Chef de projet est chargé de faciliter le projet de test, de coordonner la disponibilité et le calendrier des développeurs/testeurs et de les former si nécessaire.
- Le PO est en charge d'effectuer un tes en recette sur chaque US développé.
- Le développeur est en charge de réaliser les tests.

## 13. Besoins en personnel et en formation


## 14. Calendrier

A chaque déploiement les tests unitaires sont lancés via la pipeline.

Avant chaque mise en prod, le PO devra effectuer les tests des nouvelles US sur la recette.

## 15. Risques et imprévus

- Risque sur l'OS, ne testant que sur Windows, quid de mac ?
- Risque sur les mobiles, responsive non testé
- 


## 16. Approbations

Le chef de projet et le PO doivent se mettre  d'accord sur l'achèvement du projet de test et déterminer quand il est prêt à passer à l'étape suivante.


## Credits:

https://commentouvrir.com/definitions/une-vue-densemble-de-lieee-829/

https://docs.google.com/document/d/1F1TUX5BkviRbw8auI2Xq2K2wyGTS-Ag14DRymiELmzc/edit
