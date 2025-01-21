# Effect


## Example 

__Get orders from order-service with http call, manage injection dependencies and errors with Effect-ts__

Controller 

```javascript
import { APIGatewayProxyEvent, APIGatewayProxyResult } from 'aws-lambda';

import { Effect } from 'effect';
import { getAllEffect } from './services/order-live-service.mjs';
import { HttpClient } from './http-client.mjs';

export class OrderController {

  constructor(public httpClient: HttpClient) {
  }

  getAll = async (
    event: APIGatewayProxyEvent
  ): Promise<any> => {
    console.log("GET ALL");
    const service = Effect.provideService(getAllEffect, HttpClient, this.httpClient);

    const response = service.pipe(
        Effect.matchEffect( {
          onFailure: (e) => {
            console.error("Erreur lors de la récupération des commandes :", e);
            return Effect.succeed({
              statusCode: 400,
              body: ""
            })
          },
          onSuccess: (orders) => {
            return Effect.succeed({
              statusCode: 200,
              body: {
                message: 'Orders fetched successfully',
                orders,
              }
            })
          }}
        )
      );

    return Effect.runPromise(response);
  };
}
```

order-live-service.mts

```javascript
import { Effect } from 'effect';
import { HttpClient,  } from './../http-client.mjs';
import { OrderResponse } from './OrderResponse.mjs';
import { OrderApiResponse } from './OrderApiResponse.mjs';

export const getAllEffect = Effect.gen(function* () {
  const http = yield* HttpClient
  const response: Response = yield* Effect.tryPromise(() => http.get('/orders', {}));
  const json: OrderApiResponse[] = yield* Effect.tryPromise(() => response.json())
  return json.map(order =>
    new OrderResponse(
      order.creationDate,
      { firstname: 'Julie', lastname: 'Cousin' },//TODO mocked until order service give these info
      {address: order.delivery.address, additionalAddress: order.delivery.additionalAddress, zipcode: order.delivery.zipcode, city: order.delivery.city},
      { email: 'Aleth_Remy31@hotmail.fr', phone: '0710559139' },//TODO mocked until order service give these info
      {isOnline: !order.isOffline},
      order.tiwattsNumber,
      order.num,
      null,
      order.status
    )
  )
})

```

http-client.ts

```javascript
import { Context } from 'effect';


export interface HttpClient {
  readonly get: (endpoint: string, headers: Record<string, string>) => Promise<Response>
}

export const HttpClient = Context.GenericTag<HttpClient>('HttpClient');

export class HttpClientImplementation implements HttpClient {
  private baseUrl: string;

  constructor(baseUrl: string) {
    this.baseUrl = baseUrl;
  }

  async get(endpoint: string, headers: Record<string, string> = {}): Promise<Response> {
    const url = `${this.baseUrl}${endpoint}`;
    const response = await fetch(url, {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
        ...headers,
      },
    });

    return response;
  }
}
```

app.mts (Usage)

```javascript
const orderController = new OrderController(new HttpClientImplementation(process.env.ORDER_SERVICE_URL as string));
```



## Example With Multiple dependency injection, use Effect.gen and Effect.foreach

__Get orders from order-service with http call, for each command get user info from aws lambda__


order-live-service.ts  (Le coeur de l'implementation)

```typescript
import { Effect, pipe } from 'effect';
import { HttpClient } from './../http-client.mjs';
import { OrderResponse } from './OrderResponse.mjs';
import { OrderApiResponse } from './OrderApiResponse.mjs';
import { UserApi } from './../ports/user.api.mjs';

export const getAllEffect = Effect.gen(function* () {
  const http = yield* HttpClient;
  const userService = yield* UserApi; // Ajout du userService

  const response: Response = yield* Effect.tryPromise(() =>
    http.get('/orders', {
      'User-Id': '5255f404-4031-7002-b7b9-0aaa6c994e5b',
    })
  );

  const json: OrderApiResponse[] = yield* Effect.tryPromise(() =>
    response.json()
  );

  const transformOrder = (order: OrderApiResponse) =>
    Effect.gen(function* () {
      const customerId = order.customers[0].id;

      const user = yield* Effect.tryPromise(() =>
        userService.getUserById(customerId)
      );
      return new OrderResponse(
        order.creationDate,
        { firstname: user.firstname, lastname: user.lastname },
        {
          address: order.delivery.address,
          additionalAddress: order.delivery.additionalAddress,
          zipcode: order.delivery.zipcode,
          city: order.delivery.city,
        },
        { email: user.email, phone: '0710559139' },
        { isOnline: !order.isOffline },
        order.tiwattsNumber,
        order.num,
        null,
        order.status
      );
    });

  return yield* Effect.forEach(json, transformOrder);
});

```


user-api.mts

```typescript
import { Context } from 'effect';
import { UUID } from 'node:crypto';

export type User = {
  lastname: string;
  firstname: string;
  email: string;
  phone: string;
};

export interface UserApi {
  getAll: () => Promise<Buffer<ArrayBuffer>>;
  getUserById: (userId: UUID) => Promise<User>;
}

export const UserApi = Context.GenericTag<UserApi>('UserApi'); //Important for EFFECT
```


user.service.mts  (Implement user-api)


```typescript
import { User, UserApi } from 'ports/user.api.mjs';
import { invokeUserService } from './../lambda-client.mjs';
import { convertToCSV } from './../utils/csv-utils.js';
import { UUID } from 'node:crypto';

export class UserService implements UserApi {
  async getAll(): Promise<Buffer<ArrayBuffer>> {
    const powerplants = await invokeUserService({
      headers: {},
      httpMethod: 'GET',
      path: '/users',
    });

    const csv = convertToCSV(powerplants.body);

    return Buffer.from(csv, 'utf-8');
  }

  async getUserById(userId: UUID): Promise<User> {
    const result = await invokeUserService({
      headers: {},
      httpMethod: 'GET',
      path: `/users/${userId}`,
    });

    return Promise.resolve(result.body);
  }
}
```

Controller

```typescript
import { APIGatewayProxyEvent, APIGatewayProxyResult } from 'aws-lambda';

import { Effect, pipe } from 'effect';
import { getAllEffect } from './services/order-live-service.mjs';
import { HttpClient } from './http-client.mjs';
import { UserApi } from './ports/user.api.mjs';

export class OrderController {
  constructor(public httpClient: HttpClient, public userApi: UserApi) {}

  getAll = async (event: APIGatewayProxyEvent): Promise<any> => {
    const service = getAllEffect.pipe(
      Effect.provideService(HttpClient, this.httpClient),
      Effect.provideService(UserApi, this.userApi)
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
        onSuccess: (orders) => {
          return Effect.succeed({
            statusCode: 200,
            body: {
              message: 'Orders fetched successfully',
              orders,
            },
          });
        },
      })
    );

    return Effect.runPromise(response);
  };
}
```

app.mts (Instance du controller)

```typescript
const userApi = new UserService();
const orderController = new OrderController(
  new HttpClientImplementation(process.env.ORDER_SERVICE_URL as string),
  userApi
);

tsconfig.json

    {
      "compilerOptions": {
        "outDir": "dist",
        "target": "ESNext",
        "module": "NodeNext",
        "strict": true,
        "preserveConstEnums": true,
        "esModuleInterop": true,
        "forceConsistentCasingInFileNames": true,
        "moduleResolution": "NodeNext",
        "paths": {
          "*": ["./src/*"]
        }
      },
      "include": ["src/**/*"]
    }

```
