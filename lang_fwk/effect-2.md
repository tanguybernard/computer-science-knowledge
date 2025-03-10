

tsconfig


    {
      "compilerOptions": {
        "module": "ESNext",
        "target": "ESNext",
        "moduleResolution": "node",
        "outDir": "./dist",
        "allowJs": true,
        "esModuleInterop": true,
        "resolveJsonModule": true,
        "skipLibCheck": true
      },
      "include": ["src/**/*"],
      "exclude": ["node_modules"]
    }


package


    {
      "name": "effect-demo",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "type": "module",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "start": "npx tsx src/index.mts"
      },
      "keywords": [],
      "author": "",
      "license": "ISC",
      "dependencies": {
        "effect": "^3.12.5",
        "https-proxy-agent": "^7.0.6",
        "node-fetch": "^3.3.2"
      },
      "devDependencies": {
        "ts-node": "^10.9.2",
        "tsx": "^4.19.2",
        "typescript": "^5.7.3"
      }
    }


src/http-client.mts


    import { Context } from 'effect';
    import fetch from 'node-fetch';
    
    
    import { HttpsProxyAgent } from 'https-proxy-agent';
    
    const proxyUrl = `http://vip-users.proxy.edf.fr:3131`;
    const proxyAgent = new HttpsProxyAgent(proxyUrl);
    
    export interface HttpClient {
        readonly get: (
            endpoint: string,
            headers: Record<string, string>
        ) => Promise<Response>;
    }
    
    export const HttpClient = Context.GenericTag<HttpClient>('HttpClient');
    
    export class HttpClientImplementation implements HttpClient {
        private baseUrl: string;
    
        constructor(baseUrl: string) {
            this.baseUrl = baseUrl;
        }
    
        async get(
            endpoint: string,
            headers: Record<string, any> = {}
        ): Promise<any> {
            const url = `${this.baseUrl}${endpoint}`;
            console.log(url)
            const response = await fetch(url, {
                method: 'GET',
                agent: proxyAgent,
                headers: {
                    'Content-Type': 'application/json',
                    ...headers,
                },
            });
    
            return response;
        }
    
        async post(
            endpoint: string,
            body: any,
            headers: Record<string, string> = {}
        ): Promise<any> {
            const url = `${this.baseUrl}${endpoint}`;
            const response = await fetch(url, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    ...headers,
                },
                body: JSON.stringify(body),
            });
    
            return response;
        }
    }


src/index.mts

    import {Context, Effect, Layer} from "effect";
    import { Data } from "effect"
    import {HttpClient, HttpClientImplementation} from "./http-client.mjs";
    
    const myClient = new HttpClientImplementation('https://jsonplaceholder.typicode.com')
    
    
     myClient.get('/posts/1', {})
         .then((r) => r.json())
         .then(r => console.log(r))
         .catch(e => console.log(e));
    
    
    
    
    class MissingUser extends Data.TaggedError("MissingUser")<{
        message: string
    }> {}
    
    type User = {id: number, userId: number, email: string}
    
    export interface UserService {
        readonly getUserById: ({ id }: { id: number }) => Effect.Effect<
        User,
        MissingUser,
        HttpClient
        >;
    }
    
    export const UserService = Context.GenericTag<UserService>("UserService");
    
    
    
    const id = 1;
    
    export const UserServiceLive = () => Layer.effect(
        UserService,
        Effect.map(HttpClient, (client) => ({
            getUserById: ({ id }: { id: number }) =>
                id === 1
                    ? Effect.succeed({ id: 1, userId: 3, email: "test@example.com" })
                    : Effect.fail(new MissingUser({ message: "User not found" })),
        }))
    );
    
    export const getAllEffect = (userId: number) =>
        Effect.gen(function* () {
            const http = yield* HttpClient;
    
            const response: Response = yield* Effect.tryPromise(() =>
                http.get('/users/'+userId, {})
            );
    
            const json: User = yield* Effect.tryPromise(() =>
                response.json()
            );
    
            return json;
        });
    
    
    
        const service = getAllEffect(id).pipe(
            Effect.provideService(HttpClient, myClient),
        );
    
        const response = service.pipe(
            Effect.matchEffect({
                onFailure: (e) => {
                    console.error('Erreur lors de la récupération des commandes :', e);
                    return Effect.succeed({
                        statusCode: 400,
                        body: '',
                    });
                },
                onSuccess: (user) => {
                    return Effect.succeed({
                        statusCode: 200,
                        body: {
                            message: 'Orders fetched successfully',
                            user,
                        },
                    });
                },
            })
        );
    
    const user = Effect.runPromise(response);
    
    user.then(console.log)



Better src/index.mts:



    import {Context, Effect, Layer} from "effect";
    import { Data } from "effect"
    import {HttpClient, HttpClientImplementation} from "./http-client.mjs";
    
    const myClient = new HttpClientImplementation('https://jsonplaceholder.typicode.com')
    
    
     myClient.get('/posts/1', {})
         .then((r) => r.json())
         .then(r => console.log(r))
         .catch(e => console.log(e));
    
    
    
    
    class MissingUser extends Data.TaggedError("MissingUser")<{
        message: string
    }> {}
    
    type User = {id: number, userId: number, email: string}
    
    export interface UserService {
        readonly getUserById: ({ id }: { id: number }) => Effect.Effect<
        User,
        MissingUser,
        HttpClient
        >;
    }
    
    export const UserService = Context.GenericTag<UserService>("UserService");
    
    
    
    const id = 1;
    
    export const UserServiceLive = (httpClient: HttpClient) =>
        Layer.succeed(
            UserService, // Le contexte fourni par cette couche
            {
                getUserById: ({ id }: { id: number }) =>
                    id === 1
                        ? Effect.succeed({ id: 1, userId: 3, email: "test@example.com" })
                        : Effect.fail(new MissingUser({ message: "User not found" })),
            }
        );
    
    export const getAllEffect = (userId: number) =>
        Effect.gen(function* () {
            const http = yield* HttpClient;
    
            const response: Response = yield* Effect.tryPromise(() =>
                http.get('/users/'+userId, {})
            );
    
            const json: User = yield* Effect.tryPromise(() =>
                response.json()
            );
    
            return json;
        });
    
    
    
        const service = getAllEffect(id).pipe(
            Effect.provideService(HttpClient, myClient),
        );
    
        const response = service.pipe(
            Effect.matchEffect({
                onFailure: (e) => {
                    console.error('Erreur lors de la récupération des commandes :', e);
                    return Effect.succeed({
                        statusCode: 400,
                        body: '',
                    });
                },
                onSuccess: (user) => {
                    return Effect.succeed({
                        statusCode: 200,
                        body: {
                            message: 'Orders fetched successfully',
                            user,
                        },
                    });
                },
            })
        );
    
    const user = Effect.runPromise(response);
    
    user.then(console.log)
    
    
    
    export const UserService2Live = Layer.effect(
        UserService,
        Effect.map(HttpClient, (http) => UserService.of({
            getUserById: ({ id }) => {
                return Effect.succeed({userId:1, id:1, email:"test@example.com"});
            }
    
        }))
    );
    
    
    
    const mainEffect = Effect.gen(function* () {
        const userService = yield* UserService;
    
        const user = yield* userService.getUserById({ id: 1 });
        return user;
    });
    
    
    const runnable = Effect.provide(mainEffect, UserService2Live)
        .pipe(Effect.provideService(HttpClient, myClient))
    
    console.log('Yaouh !!!')
    Effect.runPromise(runnable).then(console.log).catch(console.error);


