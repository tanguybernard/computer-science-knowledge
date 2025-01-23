

script.mts

```typescript
import {Console, Context, Effect, Layer, Runtime} from "effect"
import {HttpClientEffect, HttpClientImplementationEffect} from "./http-client-effect.mjs";
import {cons} from "effect/List";


const makeUsers = Effect.gen(function*() {
    const client = yield* HttpClientEffect

    const findById = (id: number) => {
        const res = client.get(`/users/${id}`, {});
        return res.pipe(
            Effect.andThen((response) => response.json())
        );
    }
    return { findById } as const
})

const client = new HttpClientImplementationEffect('https://jsonplaceholder.typicode.com');

const layer = Layer.succeed(HttpClientEffect, client);

const mainEffect = Effect.gen(function* () {
    const mm = yield* makeUsers;

    const user = yield* mm.findById(1);
    return user;
});


const runnable = Effect.provide(mainEffect, layer)

console.log('Yaouh !!!')
const re = Effect.runPromise(runnable)

    re.then((e)=> console.log(e))
```

http-client-effect.mts

```typescript
import {Context, Effect, pipe} from 'effect';
import fetch, {Response} from 'node-fetch';


import { HttpsProxyAgent } from 'https-proxy-agent';
import {UnknownException} from "effect/Cause";

const proxyUrl = `http://vip-users.proxy.edf.fr:3131`;
const proxyAgent = new HttpsProxyAgent(proxyUrl);

export interface HttpClientEffect {
    readonly get: (
        endpoint: string,
        headers: Record<string, string>
    ) => Effect.Effect<Response, Error>;
}

export const HttpClientEffect = Context.GenericTag<HttpClientEffect>('HttpClientEffect');

export class HttpClientImplementationEffect implements HttpClientEffect {
    private baseUrl: string;

    constructor(baseUrl: string) {
        this.baseUrl = baseUrl;
    }

    get(
        endpoint: string,
        headers: Record<string, any> = {}
    ): Effect.Effect<Response, Error, never> {
        const url = `${this.baseUrl}${endpoint}`;


        const res =  fetch(url, {
            method: 'GET',
            agent: proxyAgent,
            headers: {
                'Content-Type': 'application/json',
                ...headers,
            },
        })

        return  Effect.tryPromise({try: () =>res, catch: ()=> new Error()});


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
```
