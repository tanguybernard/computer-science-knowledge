# Effect

- https://www.sandromaglione.com/articles/complete-introduction-to-using-effect-in-typescript
- https://dnlytras.com/blog/effect-ts
- https://tobyhobson.com/posts/effect/why-effect/#dependency-injection


## Context

### GenericTag

Example:

  export interface UserApi {
    getAllWithCsv: () => Promise<Buffer<ArrayBuffer>>;
    getuserById: (userId: UUID) => Promise<User>;
  }
  
  export const UserApi = Context.GenericTag<UserApi>('UserApi');

GenericTag : Un GenericTag est utilisé pour identifier des services ou dépendances dans un contexte fonctionnel. Les dépendances sont enregistrées dans un Context et injectées dans des effets.


