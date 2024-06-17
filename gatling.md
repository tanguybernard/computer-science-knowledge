# Gatling


## Simple Test

En utilisant la version standalone 3.11.13

1. Lancer le recorder en mode HAR converter

    .\mvnw.cmd gatling:recorder

2. Enregistrer depuis chrome le scenario.

    Inspect > Network > Record Network log > Save all as HAR
   
3. Enlever les statics
4. Appuyer sur start
5. Lancer le test

    .\mvnw.cmd gatling:recorder

6. Dans le prompt choisir le scenario
7. Editer le .java, la simulation enregistrer dans src/test/java/
8. Voir le resultat dans target


## Source

https://gatling.io/blog/migrate-to-the-maven-build-tool
  
