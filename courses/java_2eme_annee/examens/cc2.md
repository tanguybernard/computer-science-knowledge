Voici un examen avec deux exercices de même complexité, incluant un barème détaillé pour l'évaluation.

---

### **Examen Java : Programmation Orientée Objet (POO)**

#### **Exercice 1 : Gestion d'une banque (15 points)**

##### 1. Création des classes de base (6 points)

- **(3 points)** Créez une classe `CompteBancaire` avec les attributs suivants :
  - `titulaire` (String)
  - `solde` (double)
  - `numeroCompte` (String)
  
  La classe doit également contenir :
  - Un constructeur pour initialiser les valeurs des attributs.
  - Des méthodes `getters` et `setters` pour chaque attribut.

- **(3 points)** Ajoutez une méthode `deposer(double montant)` qui ajoute le montant au solde, et une méthode `retirer(double montant)` qui retire le montant du solde, en vérifiant si le solde est suffisant. Si le solde est insuffisant, affichez un message d'erreur.

##### 2. Héritage et classes dérivées (4 points)

- **(2 points)** Créez une classe `CompteEpargne` qui hérite de `CompteBancaire` et ajoute un attribut `tauxInteret` (double). Ajoutez une méthode `calculerInteret()` qui retourne le montant d'intérêt gagné sur le solde actuel en fonction du taux d'intérêt.
  
- **(2 points)** Créez une classe `CompteCourant` qui hérite de `CompteBancaire` et ajoute un attribut `decouvertAutorise` (double). Ajoutez une méthode `verifierDecouvert(double montant)` qui vérifie si un retrait ne dépasse pas le découvert autorisé.

##### 3. Interface et gestion des comptes (5 points)

- **(2 points)** Créez une interface `Affichable` avec une méthode `afficherDetails()` qui affiche les détails du compte (titulaire, solde, numéro de compte).
  
- **(3 points)** Implémentez cette interface dans les classes `CompteBancaire`, `CompteEpargne`, et `CompteCourant`. Créez une classe `Banque` contenant une liste de comptes et une méthode `afficherTousLesComptes()` qui affiche les détails de tous les comptes. Testez la classe en ajoutant des comptes et en affichant les informations.

##### **Test de votre application (2 points)**

Écrivez une classe `TestBanque` avec une méthode `main` où vous :
- Créez plusieurs comptes (bancaires, épargne, courant).
- Déposez et retirez de l'argent sur différents comptes.
- Affichez les détails de tous les comptes dans la banque pour vérifier que tout fonctionne correctement.


##### QCM

Voici un QCM sur la programmation orientée objet en Java :

###### Question 1 : Quel est l'objectif principal de la programmation orientée objet (POO) ?

- A) Simplifier les applications en supprimant la nécessité de méthodes.
- B) Organiser le code sous forme de classes et d'objets pour améliorer la réutilisabilité et la maintenance.
- C) Utiliser uniquement des fonctions globales pour le code.
- D) Réduire la taille du code en le rendant plus compact.

###### Question 2 : Qu'est-ce qu'une classe en Java ?

- A) Un objet qui contient des données et des méthodes.
- B) Une sorte de modèle à partir duquel des objets peuvent être créés.
- C) Un type de donnée primitif.
- D) Une méthode utilisée pour manipuler des données.

###### Question 3 : Quel est l'effet de la déclaration `private` sur une variable dans une classe ?

- A) La variable peut être accédée uniquement dans la classe elle-même.
- B) La variable est accessible dans toutes les autres classes du même package.
- C) La variable est accessible à toutes les classes sans restriction.
- D) La variable peut être modifiée directement sans restriction.

###### Question 4 : Qu'est-ce que l'héritage en Java ?

- A) Un mécanisme permettant à une classe de hériter des méthodes et propriétés d'une autre classe.
- B) Un processus de duplication de code dans plusieurs classes.
- C) Un type de données utilisé pour stocker des objets.
- D) Un type de méthode qui n'accepte pas d'arguments.



###### Question 5 : Quand utilise-t-on le mot-clé "super" en Java ?

- A) Pour appeler un constructeur de la classe parente
- B) Pour créer une instance d'une sous-classe
- C) Pour accéder aux méthodes privées d'une classe parente
- D) Pour appeler des méthodes statiques dans une classe parent

###### Question 6 :  Qu'est ce que l'encapsulation ?

- A) Le fait de cacher les détails d'implémentation
- B) Le fait de ne pas définir ce que fait une fonction ou une classe
- C) Le fait de réduire la taille des objets pour les transporter
- D) Le fait d'échanger du code contre des capsules


###### Question 7 :  Que signifie le mot-clé extends en Java ?

- A) Il permet à une classe de hériter d'une autre classe.
- B) Il permet de déclarer une méthode abstraite.
- C) Il permet d'implémenter une interface.
- D) Il est utilisé pour instancier un objet.


###### Question 8 :  Qu'est-ce que la composition en Java ?

- A) Une relation entre classes où une classe contient une instance d'une autre classe
- B) Une relation d'héritage entre classes
- C) Une méthode qui modifie les variables d'instance
- D) Une interface avec des méthodes concrètes

---

#### **Exercice 2 : Gestion des employés dans une entreprise (15 points)**

##### 1. Création des classes de base (6 points)

- **(3 points)** Créez une classe `Employe` avec les attributs suivants :
  - `nom` (String)
  - `prenom` (String)
  - `id` (int)
  - `salaire` (double)
  
  La classe doit contenir un constructeur pour initialiser ces attributs et des méthodes `getters` et `setters`.

- **(3 points)** Ajoutez une méthode `augmenterSalaire(double pourcentage)` qui augmente le salaire de l'employé en fonction du pourcentage passé en paramètre.

##### 2. Héritage et classes dérivées (4 points)

- **(2 points)** Créez une classe `Manager` qui hérite de `Employe` et ajoute un attribut `budget` (double) pour gérer le budget de l'équipe.
  
- **(2 points)** Créez une classe `Technicien` qui hérite de `Employe` et ajoute un attribut `competences` (String) pour décrire les compétences techniques du technicien.

##### 3. Polymorphisme et gestion des employés (5 points)

- **(3 points)** Créez une méthode `afficherDetails()` dans la classe `Employe` qui affiche les informations personnelles de l'employé. Redéfinissez cette méthode dans les classes `Manager` et `Technicien` pour afficher des informations supplémentaires spécifiques à chaque type d'employé (par exemple, afficher le budget pour les managers et les compétences pour les techniciens).
  
- **(2 points)** Créez une classe `Entreprise` qui contient une liste d'employés et une méthode `afficherTousLesEmployes()` qui affiche les détails de tous les employés de l'entreprise. Testez votre classe en ajoutant des employés et en affichant les informations.

##### **Test de votre application (2 points)**

Écrivez une classe `TestEntreprise` avec une méthode `main` où vous :
- Créez plusieurs employés (managers, techniciens).
- Appliquez une augmentation de salaire et affichez les nouveaux salaires.
- Affichez les détails de tous les employés dans l'entreprise pour vérifier que tout fonctionne correctement.

---

### **Barème de l'examen :**

#### **Exercice 1 : Gestion d'une banque (15 points)**

- **Partie 1 : Création des classes de base**  
  - Correctness du constructeur et des `getters` et `setters` : 3 points  
  - Méthodes `deposer` et `retirer` : 3 points  

- **Partie 2 : Héritage et classes dérivées**  
  - Implémentation de `CompteEpargne` et méthode `calculerInteret` : 2 points  
  - Implémentation de `CompteCourant` et méthode `verifierDecouvert` : 2 points  

- **Partie 3 : Interface et gestion des comptes**  
  - Création de l'interface `Affichable` : 2 points  
  - Implémentation dans les classes dérivées et gestion des comptes dans `Banque` : 3 points  

- **Test de l'application** : 2 points

#### **Exercice 2 : Gestion des employés dans une entreprise (15 points)**

- **Partie 1 : Création des classes de base**  
  - Correctness du constructeur et des `getters` et `setters` : 3 points  
  - Méthode `augmenterSalaire` : 3 points  

- **Partie 2 : Héritage et classes dérivées**  
  - Implémentation de `Manager` et `Technicien` : 2 points  
  - Implémentation des attributs spécifiques : 2 points  

- **Partie 3 : Polymorphisme et gestion des employés**  
  - Redéfinition de `afficherDetails()` et gestion du polymorphisme : 3 points  
  - Implémentation de la gestion des employés dans `Entreprise` : 2 points  

- **Test de l'application** : 2 points

---

Ces exercices permettent de tester à la fois la compréhension des concepts de la POO, comme l'encapsulation, l'héritage, le polymorphisme, et l'interface, tout en impliquant des scénarios pratiques sur la gestion d'une banque et d'une entreprise. Le barème aide à évaluer le détail de l'implémentation et la logique de programmation.
