v0
```typescript
   const program = async (id: number) => {
        try {
          const res =await  myfetch(id)
          if(res.status === 404) {
            throw new PostNotFoundError("Post not found with id")
          }
          if(!res.ok) {
            throw new HttpError("HttpError")
          }
          try {
            let json = await res.json();
            return json.name
          }
          catch (e) {
            throw new JsonParseError("JSON parsing error")
          }
        }
        catch (error) {
          if(error instanceof JsonParseError) {
            console.log(`Error`)
          }
          else if(error instanceof PostNotFoundError){
            console.log(`Post missing. Falling back to a default.`)
            return "Default name"
          }
          else {
            return "Default name"
          }

        }

      }
```

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


V3

```typescript
    it('should lalal', async () => {

      const myfetch = (id: number) => {
        return Promise.resolve({
          ok: true,
          status: 200,
          json: () => Promise.resolve({ id: 34, name: "Test" }),
        });
      };

      class HttpError extends Error {
        readonly _tag = "HttpError";
        constructor(readonly message: string) {
          super(message);
        }
      }

      class PostNotFoundError extends Error {
        readonly _tag = "PostNotFoundError";
        constructor(readonly message: string) {
          super(message);
        }
      }

      class JsonParseError extends Error {
        readonly _tag = "JsonParseError"; // Correction ici
        constructor(readonly message: string) {
          super(message);
        }
      }

      const myRealfetch = (id: number): Effect.Effect<any, HttpError, any> =>
        Effect.tryPromise({
          try: () => myfetch(id),
          catch: (error) => new HttpError("HttpError"),
        });

      const manageError = (res: any): Effect.Effect<{name: string}, HttpError | PostNotFoundError | JsonParseError, never> =>
        res.status === 404
          ? Effect.fail(new PostNotFoundError("Post not found with id"))
          : res.ok
            ? Effect.tryPromise({
              try: () => res.json(),
              catch: (error) => new JsonParseError("JSON parsing error"),
            })
            : Effect.fail(new HttpError("Post not found"));

      const getPost2 = (id: number): Effect.Effect<string, never, any> =>
        pipe(
          myRealfetch(id),
          Effect.flatMap(manageError),
          Effect.catchTags({
            HttpError: (error) =>
              Effect.logError(`Exiting.`).pipe(
                Effect.flatMap(() => Effect.fail(error))
              ),
            PostNotFoundError: (error) =>
              Effect.log(`Post missing. Falling back to a default.`).pipe(
                Effect.flatMap(() => Effect.fail(error))
                //Effect.map(() => "Default post")
              ),
          }),
          Effect.flatMap((post: any) => Effect.succeed(post.name)),
          Effect.orElseSucceed(() => "Default name"),
          //Effect.scoped
        );


//Avec un orElseFail a la place du succès changer signature : Effect.Effect<string, Error, any> =>
//Effect.orElseFail(() => new Error("Request failed and no fallback available"))

      pipe(
        getPost2(1),
        Effect.match({
          onFailure: (error: Error) => {
            console.error("Erreur:", error.message);
          },
          onSuccess: (name) => {
            console.log("Nom du post:", name);
          },
        }),
        Effect.runPromise

      );

      expect(true).toEqual(true);
    });
```
