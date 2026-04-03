# Accesibilité


## UI vs Structure (sémantique)

L’**UI**, c’est le **costume** (l’apparence) ; la **Structure**, c’est le **rôle** (la fonction).

* **L'UI (ex: Composant `Subtitle`) :** Définit que le texte doit être en 14px, gris et italique. C'est une étiquette pour le développeur et un indice visuel pour l'utilisateur valide.
* **La Structure (ex: Balise `<h2>`) :** Définit la position logique dans l'arbre du document. Elle dit au lecteur d'écran : *"Ceci est le début d'une section majeure"*.

**L'erreur classique :** Utiliser un composant `Subtitle` (UI) codé avec une simple balise `<div>`. Visuellement, c'est joli, mais pour un aveugle, ce titre n'existe pas.

**La règle d'or :** Un élément peut avoir l'apparence d'un "Subtitle" (UI) tout en étant techniquement un `<h2>`, `<h3>` ou même un `<p>` (Structure), selon l'endroit où il se trouve dans la page.



## Extension Navigateur

- HeadingsMap
- Measure Everything

