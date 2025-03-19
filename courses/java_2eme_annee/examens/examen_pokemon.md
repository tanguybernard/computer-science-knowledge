Bien sûr, je peux t'aider à préparer un examen sur le thème Pokémon en programmation orientée objet (POO) en Java. Pour cela, voici une proposition d'examen avec les consignes et un barème de notation. L'examen sera divisé en plusieurs parties : théorie et pratique, avec des questions qui abordent les concepts de base de la POO (classes, objets, héritage, polymorphisme, etc.).

---

## **Examen : Programmation Orientée Objet en Java (Thème Pokémon)**

### **Durée : 2 heures**

### **Barème : 20 points**

---

### **Partie 1 : Questions théoriques (8 points)**

Répondez aux questions suivantes en expliquant clairement vos réponses.

**1. Qu’est-ce que l’encapsulation en POO ?**

**2. Qu’est-ce que l’héritage et comment est-il utilisé en POO ? Donne un exemple dans le contexte Pokémon.**

**3. Qu’est-ce que le polymorphisme et comment peut-il être utilisé dans un jeu Pokémon ?**

**4. Expliquez la différence entre une classe abstraite et une interface en Java.**

---

### **Partie 2 : Exercice pratique (12 points)**

Développez une partie du programme de gestion des Pokémon, en utilisant les concepts de la POO.

**Énoncé :**

Vous devez créer un système pour gérer des Pokémon avec les fonctionnalités suivantes :

**1. Classes de base :**  
Créez une classe `Pokemon` qui possède les attributs suivants :
- `nom` : le nom du Pokémon (type String)
- `niveau` : le niveau du Pokémon (type int)
- `type` : le type du Pokémon (type String, ex : "Électrique", "Feu", "Eau", etc.)

La classe doit inclure les méthodes suivantes :
- Un constructeur pour initialiser ces trois attributs.
- Une méthode `attaquer()` qui affiche un message : "Le Pokémon [nom] attaque avec [attaque] !" (Vous pouvez choisir une attaque générique).
- Une méthode `evoluer()` qui augmente le niveau de 1 (ou plus, selon le type d'évolution).
- Une méthode `afficherInfo()` qui affiche les informations du Pokémon (nom, niveau, type).

**2. Héritage :**  
Créez deux sous-classes qui héritent de `Pokemon` :
- `PokemonElectrique` (ex : Pikachu) : ajoute un attribut `voltage` (type int) et une méthode `utiliserAttaqueElectrique()`.
- `PokemonFeu` (ex : Salamèche) : ajoute un attribut `temperature` (type int) et une méthode `utiliserAttaqueFeu()`.

**3. Polymorphisme :**  
Utilisez le polymorphisme pour que chaque sous-classe redéfinisse la méthode `attaquer()`, afin que l’attaque soit spécifique à chaque type de Pokémon (exemple : Pikachu attaque avec une décharge électrique, Salamèche avec une flamme).

---

### **Barème :**

| Critère                                                   | Points |
|-----------------------------------------------------------|--------|
| **Partie théorique**                                      |        |
| Réponse à la question 1 (Encapsulation)                   | 2      |
| Réponse à la question 2 (Héritage)                        | 2      |
| Réponse à la question 3 (Polymorphisme)                   | 2      |
| Réponse à la question 4 (Classe abstraite vs Interface)   | 2      |
| **Partie pratique**                                       |        |
| Création de la classe `Pokemon` avec les méthodes de base | 4      |
| Création des sous-classes `PokemonElectrique` et `PokemonFeu` | 4      |
| Utilisation du polymorphisme pour la méthode `attaquer()` | 2      |
| **Total**                                                 | **20**  |

---

### **Conseils pour les étudiants :**
1. **Respectez la syntaxe Java**, surtout en ce qui concerne les conventions de nommage des classes et des méthodes.
2. **Testez votre code** avant de soumettre. Assurez-vous que toutes les méthodes fonctionnent comme prévu.
3. N'hésitez pas à ajouter des commentaires dans votre code pour expliquer vos choix de conception.

