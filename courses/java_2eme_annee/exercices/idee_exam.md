Voici un sujet d'examen avec un exercice de Java sur les notions de programmation orientée objet, accompagné des critères d'évaluation :

## Exercice : Gestion d'une bibliothèque (60 points)

Vous devez implémenter un système simplifié de gestion de bibliothèque en Java en utilisant les concepts de la programmation orientée objet.

### Partie 1 : Création des classes de base (20 points)

1. Créez une classe abstraite `Document` avec les attributs suivants :
   - `titre` (String)
   - `auteur` (String)
   - `anneePublication` (int)
   - `cote` (String)

   Ajoutez un constructeur, les getters/setters nécessaires, et une méthode abstraite `afficherDetails()`.

2. Créez deux classes concrètes `Livre` et `Revue` qui héritent de `Document` :
   - `Livre` ajoute un attribut `nombrePages` (int)
   - `Revue` ajoute un attribut `numero` (int)

   Implémentez la méthode `afficherDetails()` pour chaque classe.

### Partie 2 : Gestion des emprunts (25 points)

3. Créez une interface `Empruntable` avec les méthodes :
   - `emprunter()`
   - `retourner()`
   - `estDisponible()`

4. Implémentez l'interface `Empruntable` dans la classe `Livre`.

5. Créez une classe `Emprunt` qui gère les emprunts avec les attributs :
   - `document` (Document)
   - `dateEmprunt` (java.time.LocalDate)
   - `dateRetourPrevue` (java.time.LocalDate)

### Partie 3 : Gestion de la bibliothèque (15 points)

6. Créez une classe `Bibliotheque` qui contient une liste de `Document` et des méthodes pour :
   - Ajouter un document
   - Rechercher un document par titre
   - Afficher tous les documents
   - Emprunter un document
   - Retourner un document

## Critères d'évaluation

1. Conception des classes et utilisation de l'héritage (15 points)
   - Utilisation correcte de la classe abstraite et des classes concrètes
   - Implémentation appropriée des méthodes abstraites

2. Implémentation de l'interface (10 points)
   - Utilisation correcte de l'interface `Empruntable`
   - Implémentation cohérente des méthodes de l'interface

3. Encapsulation et gestion des attributs (10 points)
   - Utilisation appropriée des modificateurs d'accès
   - Implémentation correcte des getters et setters

4. Polymorphisme (10 points)
   - Utilisation du polymorphisme dans la gestion des documents

5. Gestion des collections (8 points)
   - Utilisation appropriée des collections Java pour stocker les documents

6. Qualité du code et bonnes pratiques (7 points)
   - Nommage clair des variables, méthodes et classes
   - Organisation logique du code
   - Commentaires pertinents

Temps alloué : 2 heures

Bon courage !

Citations:
[1] https://www.pandacodeur.com/pages/examen-pandacodeur/examen-java/examen-java-01-.html
[2] https://devskiller.com/fr/tests-de-codage-competences/java/
[3] https://waytolearnx.com/2018/09/qcm-java-programmation-orientee-objet.html
[4] https://waytolearnx.com/2024/09/exercices-corriges-java-programmation-orientee-objet-partie-6.html
[5] https://zestedesavoir.com/tutoriels/pdf/274/les-tests-unitaires-en-java.pdf
[6] https://www.youtube.com/watch?v=jlgeeRK6hPg
[7] https://home.mis.u-picardie.fr/~furst/docs/exercicesPOO.pdf
[8] http://jl.baril.u-bourgogne.fr/java-1-20.pdf
[9] https://esling.github.io/documents/exam_12112019.pdf
[10] https://www.math.univ-paris13.fr/~chaussar/Teaching/2010-2011/IN120/corrige_test_final.pdf
