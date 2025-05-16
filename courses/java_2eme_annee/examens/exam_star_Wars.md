

# 📝 Examen – Java Avancé : Programmation Orientée Objet & Intégration API

**Thème : Star Wars**
**Durée : 1h30**

---

## 🎯 Contexte

Vous devez développer une application capable d’analyser les personnages de l’univers Star Wars. L’objectif est de concevoir un modèle orienté objet pertinent, de récupérer des données via l’API SWAPI et d’effectuer un traitement spécifique.

---

## 📌 Travail demandé

### 1. Modélisation orientée objet

Concevez un modèle Java pour représenter les personnages de Star Wars.

* Réfléchissez aux types de personnages, à leurs caractéristiques communes et leurs différences.
* Vous devrez utiliser au moins un mécanisme d’héritage (classe abstraite, interface, etc.) pour structurer votre modèle.
* Pensez à exploiter le polymorphisme pour les comportements communs ou spécifiques.

### 2. Récupération des données

* Récupérez les 10 premiers personnages depuis l’API [https://swapi.dev/api/people](https://swapi.dev/api/people).
* Pour chaque personnage, récupérez au minimum :

  * Le nom
  * Le genre
  * La taille
  * La planète d’origine (en effectuant la requête sur le lien `homeworld` fourni)
* Instanciez les objets de votre modèle avec ces données.

### 3. Traitement métier

Écrivez une fonction qui regroupe ces personnages par planète d’origine.
La fonction retournera une structure qui associe à chaque nom de planète la liste des personnages qui en sont originaires.

---

### 4. Tests unitaires (Bonus)

* Écrivez au moins deux tests unitaires validant votre regroupement.
* L’utilisation de JUnit est un plus.

---

## 📊 Barème

* Modélisation orientée objet (héritage, abstraction, polymorphisme) : 6 points
* Intégration avec l’API : 5 points
* Traitement métier (regroupement) : 4 points
* Clarté et organisation du code : 3 points
* Tests unitaires : 2 points (+1 bonus si JUnit bien utilisé)

---

Si tu veux, je peux aussi te préparer un PDF ou un template Maven pour lancer les étudiants.
Veux-tu que je te prépare ça ?
