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
