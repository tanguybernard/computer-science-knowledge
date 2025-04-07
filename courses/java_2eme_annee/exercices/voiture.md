Bien sûr ! Voici une autre idée de jeu de société orientée PPO avec polymorphisme :

---

## 🎯 Exercice : "Jeu de Plateau - Course de Véhicules"

### 🧠 Objectifs pédagogiques
- Mettre en œuvre **l’abstraction**, **l’héritage** et le **polymorphisme**
- Travailler avec des **méthodes abstraites**
- Concevoir un système extensible pour un **jeu de course**

---

### 🏁 Contexte

Tu conçois un jeu de plateau où différents types de **véhicules** s'affrontent sur une piste. Chaque type de véhicule a une façon différente de se déplacer.

---

### 📚 Classes à concevoir

#### 1. `Vehicule` (classe abstraite)
- `String nom`
- `int position`

✅ Méthodes :
- `abstract void avancer()` — chaque véhicule avance à sa manière
- `void afficherPosition()` — affiche le nom et la position

---

#### 2. `Voiture` (hérite de `Vehicule`)
- Avance de **3 à 6 cases** à chaque tour (utilise `Random`)

---

#### 3. `Moto` (hérite de `Vehicule`)
- Avance de **2 à 8 cases**, mais a 30% de chance de glisser et perdre son tour (reste sur la meme case)

---

#### 4. `Camion` (hérite de `Vehicule`)
- Avance de **1 à 4 cases**, mais ne glisse jamais

---

#### 5. `Course`
- Liste des véhicules (`List<Vehicule>`)
- Méthodes :
  - `void lancerTour()` — chaque véhicule joue un tour
  - `boolean courseTerminee()` — la course se termine si un véhicule dépasse 50
  - `void afficherClassement()` — classement selon la position

---

### 🧪 Exemple d’utilisation

```java
Vehicule v1 = new Voiture("Ferrari");
Vehicule v2 = new Moto("Yamaha");
Vehicule v3 = new Camion("Volvo");

Course course = new Course(Arrays.asList(v1, v2, v3));

while (!course.courseTerminee()) {
    course.lancerTour();
    course.afficherClassement();
}
```

---

### 🔥 Bonus

- Afficher un **podium final**
- Gérer des **obstacles** ou des **bonus de vitesse** sur certaines cases
- Ajouter une méthode `boost()` (polymorphisme encore) que certains véhicules peuvent utiliser une fois par course

---

Tu veux une base de code pour ce jeu aussi ? Ou tu préfères réfléchir seul pour l'instant ?



Parfait ! Voici une **implémentation Java complète** de ce jeu de plateau avec polymorphisme 🚗🏍️🚛

---

### ✅ `Vehicule.java` (classe abstraite)

```java
public abstract class Vehicule {
    protected String nom;
    protected int position;

    public Vehicule(String nom) {
        this.nom = nom;
        this.position = 0;
    }

    public abstract void avancer();

    public void afficherPosition() {
        System.out.println(nom + " est à la position " + position);
    }

    public String getNom() {
        return nom;
    }

    public int getPosition() {
        return position;
    }
}
```

---

### ✅ `Voiture.java`

```java
import java.util.Random;

public class Voiture extends Vehicule {
    private Random random = new Random();

    public Voiture(String nom) {
        super(nom);
    }

    @Override
    public void avancer() {
        int avance = 3 + random.nextInt(4); // 3 à 6
        position += avance;
        System.out.println(nom + " (Voiture) avance de " + avance + " cases.");
    }
}
```

---

### ✅ `Moto.java`

```java
import java.util.Random;

public class Moto extends Vehicule {
    private Random random = new Random();

    public Moto(String nom) {
        super(nom);
    }

    @Override
    public void avancer() {
        if (random.nextInt(100) < 30) {
            System.out.println(nom + " (Moto) a glissé et ne bouge pas !");
            return;
        }
        int avance = 2 + random.nextInt(7); // 2 à 8
        position += avance;
        System.out.println(nom + " (Moto) avance de " + avance + " cases.");
    }
}
```

---

### ✅ `Camion.java`

```java
import java.util.Random;

public class Camion extends Vehicule {
    private Random random = new Random();

    public Camion(String nom) {
        super(nom);
    }

    @Override
    public void avancer() {
        int avance = 1 + random.nextInt(4); // 1 à 4
        position += avance;
        System.out.println(nom + " (Camion) avance de " + avance + " cases.");
    }
}
```

---

### ✅ `Course.java`

```java
import java.util.List;
import java.util.Comparator;

public class Course {
    private List<Vehicule> vehicules;
    private final int distanceArrivee = 50;

    public Course(List<Vehicule> vehicules) {
        this.vehicules = vehicules;
    }

    public void lancerTour() {
        System.out.println("\n🎲 Nouveau tour !");
        for (Vehicule v : vehicules) {
            v.avancer();
        }
    }

    public boolean courseTerminee() {
        return vehicules.stream().anyMatch(v -> v.getPosition() >= distanceArrivee);
    }

    public void afficherClassement() {
        System.out.println("\n📊 Classement actuel :");
        vehicules.stream()
            .sorted(Comparator.comparingInt(Vehicule::getPosition).reversed())
            .forEach(Vehicule::afficherPosition);
    }

    public void afficherPodium() {
        System.out.println("\n🏁 Course terminée ! Podium :");
        vehicules.stream()
            .sorted(Comparator.comparingInt(Vehicule::getPosition).reversed())
            .limit(3)
            .forEach(v -> System.out.println("🥇 " + v.getNom() + " avec " + v.getPosition() + " cases"));
    }
}
```

---

### ✅ `Main.java`

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        Vehicule v1 = new Voiture("Ferrari");
        Vehicule v2 = new Moto("Yamaha");
        Vehicule v3 = new Camion("Volvo");

        Course course = new Course(Arrays.asList(v1, v2, v3));

        while (!course.courseTerminee()) {
            course.lancerTour();
            course.afficherClassement();

            try {
                Thread.sleep(1000); // pause pour lisibilité
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }

        course.afficherPodium();
    }
}
```

---

### 🧪 Tu peux compiler tout ça avec :

```bash
javac *.java
java Main
```

---

Tu veux que je te propose une version améliorée avec des objets sur la piste, ou une interface graphique ensuite ? 😄
