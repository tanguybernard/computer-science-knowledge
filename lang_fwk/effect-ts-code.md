# Effect


## Example

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
