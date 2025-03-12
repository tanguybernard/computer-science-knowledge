
Course :

https://crazy-crafters.gitlab.io/red-maple/

https://gitlab.com/crazy-crafters/red-maple

Chapitre à introduire:

https://www.codecademy.com/learn/learn-intermediate-java



## 1. Intro 



### Notes

 - int: 4 octets (32 bits)

////////////////////////////

      Byte (1 octet)
      Taille : 1 octet (8 bits)1
      
      Plage de valeurs :
      
      Signé : -128 à 127
      
      Non signé : 0 à 2555
      
      Utilisé pour : caractères ASCII, petites valeurs numériques

////////////////

      Short (2 octets)
      Taille : 2 octets (16 bits)5
      
      Plage de valeurs :
      
      Signé : -32 768 à 32 767
      
      Non signé : 0 à 65 5355
      
      Utilisé pour : petits entiers, économie de mémoire


#### Class

En Java, une classe est une structure conceptuelle utilisée pour créer des objets, mais elle n'est pas elle-même un objet.

#### Passage par valeur

```java
public class Exemple {
    public static void incrementer(int x) {
        x++;
    }

    public static void main(String[] args) {
        int nombre = 10;
        incrementer(nombre);
        System.out.println(nombre); // Affiche toujours 10
    }
}
```


#### Passage par reference 


Pour les objets, la référence (adresse en mémoire) de l'objet est passée par valeur. Cela signifie que la méthode reçoit une copie de la référence, mais les deux références (l'originale et la copie) pointent vers le même objet.

```java
public class Exemple {
    static class Personne {
        String nom;
        Personne(String nom) {
            this.nom = nom;
        }
    }

    public static void changerNom(Personne personne) {
        personne.nom = "Alice";
    }

    public static void main(String[] args) {
        Personne p = new Personne("Bob");
        changerNom(p);
        System.out.println(p.nom); // Affiche "Alice"
    }
}
```

#### Remplacer une référence

La méthode remplacerReference crée un nouvel objet et modifie la copie de la référence. Cela n'affecte pas la référence originale dans main.

```java
public class Exemple {
    static class Personne {
        String nom;
        Personne(String nom) {
            this.nom = nom;
        }
    }

    public static void remplacerReference(Personne personne) {
        personne = new Personne("Charlie");
    }

    public static void main(String[] args) {
        Personne p = new Personne("Bob");
        remplacerReference(p);
        System.out.println(p.nom); // Affiche toujours "Bob"
    }
}
```

## 2. Introduction OOP

https://crazy-crafters.gitlab.io/red-maple/development/oop/basics/#/


Mars Rover Kata


Kata Video Store à la toute fin ?

https://github.com/cleancode-katas/cleancode-kata-videostore

## Abstraction

Se concentrer sur ce que fait un objet plutôt que sur comment il le fait.

Par exemple, une méthode ajouter() peut être définie pour une liste, mais l’utilisateur n’a pas besoin de savoir si cette liste est implémentée comme un tableau ou une structure chaînée.

### Encapsulation

Cache les données pour protéger leur intégrité.


## 3. Abstraction

https://crazy-crafters.gitlab.io/red-maple/development/oop/abstraction/#/

## Encapsulation

https://crazy-crafters.gitlab.io/red-maple/development/oop/encapsulation/#/


## Composition

https://crazy-crafters.gitlab.io/red-maple/development/oop/inheritance_vs_composition/#/

## Polymorphisme

Le nom de polymorphisme vient du grec et signifie qui peut prendre plusieurs formes. Cette caractéristique est un des concepts essentiels de la programmation orientée objet. Alors que l'héritage concerne les classes (et leur hiérarchie), le polymorphisme est relatif aux méthodes des objets.

https://crazy-crafters.gitlab.io/red-maple/development/oop/polymorphism/#/

_Le switch est considérés en POO comme « une occasion manquée d’utiliser du polymorphisme. »_


### Ad hoc

Le polymorphisme ad hoc permet d'avoir des fonctions de même nom, avec des __fonctionnalités similaires__, dans des __classes__ sans __aucun rapport entre elles__.

Exemple : La classe image et la classe lien peuvent avoir chacune une fonction "afficher".

https://web.maths.unsw.edu.au/~lafaye/CCM/poo/polymorp.htm

### Paramétrique

Le polymorphisme paramétrique, appelé généricité, représente la possibilité de définir __plusieurs fonctions de même nom__ mais possédant des __paramètres différents__.

- La méthode int addition(int, int) pourra retourner la somme de deux entiers
- La méthode float addition(float, float) pourra retourner la somme de deux flottants
- La méthode char addition(char, char) pourra définir au gré de l'auteur la somme de deux caractères

### Polymorphisme d'héritage

La possibilité de redéfinir une méthode dans des classes héritant d'une classe de base s'appelle la spécialisation. Il est alors possible d'appeler la méthode d'un objet sans se soucier de son type intrinsèque : il s'agit du polymorphisme d'héritage. Ceci permet de faire abstraction des détails des classes spécialisées d'une famille d'objet, en les masquant par une interface commune (qui est la classe de base).


Imaginons un __jeu d'échec__ comportant des objets __roi, reine, fou, cavalier, tour et pion__, héritant chacun de l'objet __piece__.
La méthode __mouvement()__ pourra, grâce au polymorphisme d'héritage, effectuer le mouvement approprié en fonction de la classe de l'objet référencé au moment de l'appel. Cela permettra notamment au programme de dire piece.mouvement sans avoir à se préoccuper de la classe de la pièce.



## REST

https://happycoding.io/tutorials/java-server/rest-api
