Voici une implémentation d'un jeu de combat fantaisie utilisant l'abstraction en Java, inspiré des concepts POO des résultats de recherche :

```java
// Interface pour les capacités spéciales
interface SpecialAbility {
    void useSpecialPower();
}

// Classe abstraite pour les personnages
abstract class GameCharacter {
    protected String name;
    protected int health;

    public GameCharacter(String name, int health) {
        this.name = name;
        this.health = health;
    }

    // Méthode abstraite à implémenter
    public abstract void attack();

    // Méthode concrète commune
    public void takeDamage(int damage) {
        health -= damage;
        System.out.println(name + " subit " + damage + " dégâts! Vie restante: " + health);
    }

    // Méthode concrète avec implémentation par défaut
    public void displayInfo() {
        System.out.println("Personnage: " + name + " | Vie: " + health);
    }
}

// Implémentation concrète pour un Guerrier
class Warrior extends GameCharacter implements SpecialAbility {
    public Warrior(String name) {
        super(name, 100);
    }

    @Override
    public void attack() {
        System.out.println(name + " attaque avec son épée!");
    }

    @Override
    public void useSpecialPower() {
        System.out.println(name + " utilise Coup de fureur! (+50% de dégâts)");
    }
}

// Implémentation concrète pour un Mage
class Mage extends GameCharacter {
    public Mage(String name) {
        super(name, 80);
    }

    @Override
    public void attack() {
        System.out.println(name + " lance un sort de feu!");
    }

    // Surcharge de méthode
    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Type: Mage");
    }
}

public class FantasyBattleGame {
    public static void main(String[] args) {
        GameCharacter[] characters = {
            new Warrior("Conan"),
            new Mage("Gandalf")
        };

        for (GameCharacter character : characters) {
            character.displayInfo();
            character.attack();
            
            if (character instanceof SpecialAbility) {
                ((SpecialAbility) character).useSpecialPower();
            }
            
            character.takeDamage(20);
            System.out.println("--------------------");
        }
    }
}
```

Points clés de l'implémentation :

1. **Abstraction avec la classe `GameCharacter`** :
   ```java
   abstract class GameCharacter {
       // Méthode abstraite
       public abstract void attack();
       
       // Méthode concrète
       public void takeDamage(int damage) { ... }
   }
   ```
   - Définit le comportement commun pour tous les personnages
   - Combine méthodes abstraites et concrètes[2][4]

2. **Implémentation d'interface `SpecialAbility`** :
   ```java
   class Warrior extends GameCharacter implements SpecialAbility {
       @Override
       public void useSpecialPower() { ... }
   }
   ```
   - Démonstration du principe d'interface vs classe abstraite[3][4]

3. **Polymorphisme** :
   ```java
   GameCharacter[] characters = { new Warrior(...), new Mage(...) };
   ```
   - Manipulation d'objets différents via leur type commun[1][8]

4. **Extensibilité** :
   - Ajout facile de nouveaux personnages en étendant `GameCharacter`
   - Implémentation facultative d'interfaces supplémentaires

Exécution du programme :
```
Personnage: Conan | Vie: 100
Conan attaque avec son épée!
Conan utilise Coup de fureur! (+50% de dégâts)
Conan subit 20 dégâts! Vie restante: 80
--------------------
Personnage: Gandalf | Vie: 80
Type: Mage
Gandalf lance un sort de feu!
Gandalf subit 20 dégâts! Vie restante: 60
--------------------
```

Pour améliorer cette base :
- Ajouter un système de gestion de tour
- Implémenter d'autres types de personnages (Archer, Prêtre)
- Créer une hiérarchie d'armes/magies abstraites
- Développer un système de combat plus complexe

Cette structure démontre les principes POO :
- **Abstraction** via la classe GameCharacter[2][6]
- **Encapsulation** avec les champs protégés
- **Héritage** via les sous-classes
- **Polymorphisme** dans le tableau de personnages[8]
