# Dynatrace

## Dynatrace, c'est quoi ?

Leader mondial de l’APM (Application Performance Management), Dynatrace se présente comme une plateforme « tout-en-un » (full stack) qui permet d’optimiser le business numérique d’une entreprise. 
Avec son approche holistique (dans sa globalité), cet outil convient parfaitement pour mesurer toute la chaîne applicative dans une démarche DevOps. 
Il s’attache principalement à analyser l’expérience client, en étudiant les performances des applications, des services cloud et des infrastructures numériques. 
Il est doté d’un moteur d’intelligence artificielle, sous forme d’un assistant virtuel.




## Utilisation Projet TKL

### Visualiser le flow (apache => nodejs => postgres), les requetes les plus longues

Dans l'onglet Application Observability

    Services
      > Apache
        > Dynamic web requests (Click: View dynamic requests)
          > Top requests/enpoints
            > Click Actions en face du nom de la requetes
              > Distributed Traces
                > Actions
                  > Services Flow
  
