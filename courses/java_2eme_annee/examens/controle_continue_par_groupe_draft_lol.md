
## Objectif du controle

Créer un programme Java qui :
1. Lit un fichier CSV (qui vous sera fourni) contenant l'historique des matchs.
2. Analyse les taux de victoire des compositions d'équipe.
3. Propose la meilleure composition d'équipe pour contrer une composition adverse donnée (dans la console et dans un fichier .txt)

---


## Exemple pour la Lecture du fichier CSV

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class CsvReader {
    public static void main(String[] args) {
        System.out.println("Reading CSV using BufferedReader");

        System.out.println("Working Directory = " + System.getProperty("user.dir"));

        // Path to our CSV file
        String csvFile = "src/matchinfo.csv";

        // Lists to store our data
        List<List<String>> data = new ArrayList<>();

        try (BufferedReader br = new BufferedReader(new FileReader(csvFile))) {
            String line;

            // read first line (skip header)
            br.readLine();

            // Read each line from the file
            while ((line = br.readLine()) != null) {
                // Split the line by comma and convert to a List
                String[] values = line.split(",");
                List<String> lineData = Arrays.asList(values);

                // Add the line data to our main list
                data.add(lineData);
            }

            // Print the data we read
            System.out.println("\nData read from CSV file:");
            for (int i = 0; i < data.size(); i++) {
                List<String> row = data.get(i);
                System.out.println("Row " + i + ": " + String.join(", ", row));
            }

        } catch (IOException e) {
            System.err.println("Error reading the CSV file: " + e.getMessage());
        }
    }
}
```

## Ecrire dans un fichier

```java
import java.io.FileWriter;
import java.io.IOException;

public class Main {

    public static void main(String[] args) {

        try (FileWriter writer = new FileWriter("example.txt")) {
            writer.write("Hello, World!");
        } catch (IOException e) {
            e.printStackTrace();
        }

    }

}
```

---


## Barème (20 points)

1. Lecture/écriture de fichiers (4 points)
2. Structure des données (4 points)
3. Algorithme de contre-composition (6 points)
4. Sortie des résultats (2 points)
5. Qualité du code (4 points)
6. Bonus présentation (2 points)