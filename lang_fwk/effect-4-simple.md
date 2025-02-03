
V1 

```typescript
const getPost = (id: number) =>
        pipe(
          Effect.tryPromise({
            try: () => myfetch(id),
            catch: (error) => new Error(`Network error:`)
          }),
          Effect.flatMap((res) =>
            res.ok
              ? Effect.tryPromise({
                try: () => res.json(),
                catch: () => new Error("Invalid JSON response")
              })
              : Effect.fail(new Error(`Request failed with status: ${res.status}`))
          ),
          Effect.mapError((error) => new Error(`Fetch or Parse error: ${error.message}`))
        )


// Exécuter l'effet
      Effect.runPromise(getPost(1))
        .then(console.log)
        .catch(console.error)
```


V2

```typescript
      const myfetch =(id) => {
        return Promise.resolve({
          ok: true,
          status: 200,
          json: () => Promise.resolve({id: 34, name: "LOL"})})
      }//fetch(`https://jsonplaceholder.typicode.com/posts/${id}`)


      class HttpError {
        readonly _tag = "HttpError"
        constructor(readonly error: Error) {}
      }

      class PostNotFoundError {
        readonly _tag = "PostNotFoundError"
        constructor(readonly error: Error) {}
      }

      const myRealfetch = (id: number): Effect.Effect<any, Error, never> =>
        Effect.tryPromise({
          try: () => myfetch(`https://jsonplaceholder.typicode.com/posts/${id}`),
          catch: (error) => new Error("HttpError")
        })


     const  manageError  = (res) => {
       return res.ok
         ? Effect.tryPromise({
           try: () => res.json(),
           catch: (error) => new Error("JSON parsing error")
         })
         : Effect.fail(new Error("Post not found"))
     }






      const getPost2 = (id: number): Effect.Effect<string, Error, never> =>
        pipe(
          myRealfetch(id), // Appel à la fonction fetch
          Effect.flatMap(manageError),
          Effect.flatMap((post: any) => Effect.succeed(post.name)), // Transformation de la réponse
          Effect.orElseSucceed(() => "Default name"), // Valeur par défaut en cas d'erreur
          Effect.scoped // Assure que l'effet est géré dans le scope de l'exécution
        )

      const program = pipe(
        getPost2(1), // On teste avec l'ID 1
        Effect.match({
          onFailure: (error) => {
            console.error("Erreur:", error.message)
          },
          onSuccess: (name) => {
            console.log("Nom du post:", name)
          }
        })
      )

// Exécuter le programme
      Effect.runPromise(program)
```
