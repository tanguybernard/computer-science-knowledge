### **Exercice : Création d’une API REST en Spring Boot (sans base de données)**  

#### **Objectif**  
Développer une API REST en **Spring Boot** permettant de gérer une liste d’utilisateurs en mémoire.  

#### **Instructions**  
1. **Créer un projet Spring Boot** avec les dépendances :  
   - `spring-boot-starter-web`

2. **Modéliser une entité `User`** contenant :  
   - Un identifiant unique (`UUID`)  
   - Un prénom  
   - Un nom de famille  
   - Une adresse e-mail  

3. **Créer un service `UserService`** qui stocke les utilisateurs en mémoire (dans une `List`). Il doit permettre :  
   - D’ajouter un utilisateur  
   - De récupérer tous les utilisateurs  
   - De récupérer un utilisateur par son ID  
   - De modifier un utilisateur  
   - De supprimer un utilisateur  

4. **Créer un contrôleur `UserController`** exposant les endpoints suivants :  
   - `GET /users` → Retourne la liste des utilisateurs  
   - `GET /users/{id}` → Retourne un utilisateur par son ID  
   - `POST /users` → Ajoute un utilisateur  
   - `PUT /users/{id}` → Modifie un utilisateur existant  
   - `DELETE /users/{id}` → Supprime un utilisateur  

5. **Tester l’API REST** avec **Postman** ou **cURL**.  

#### **Critères d’évaluation**  
✅ Respect des bonnes pratiques Spring Boot  
✅ API fonctionnelle et sans erreur  
✅ Bon usage des annotations (`@RestController`, `@RequestMapping`, `@Service`, etc.)  
✅ Réponses structurées en JSON  

**Bonus** ✨ : Ajouter la validation des entrées avec `@Valid` et `@NotBlank`.  

💡 **Remarque** : Cette API ne doit pas utiliser de base de données, mais stocker les données en mémoire dans une `List`.  

Bonne chance ! 🚀
