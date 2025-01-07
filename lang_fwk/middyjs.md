src/app.mts

```javascript
import middy from '@middy/core';
import httpRouterHandler, { Route } from '@middy/http-router';
import httpHeaderNormalizer from '@middy/http-header-normalizer';
import { APIGatewayProxyEvent, APIGatewayProxyResult } from 'aws-lambda';
import { OrderService } from './services/order-service.mjs';
import { OrderController } from './order-controller.mjs';

const orderService = new OrderService();

const orderController = new OrderController(orderService);

const getHandler = (handler: (event: any) => Promise<any>) => middy(handler);

const routes: Route<APIGatewayProxyEvent, APIGatewayProxyResult>[] = [
  {
    method: 'GET',
    path: '/orders',
    handler: getHandler(orderController.getOrders),
  },
  {
    method: 'GET',
    path: '/health',
    handler: middy().handler((event, context) => {
      return {
        statusCode: 200,
        body: '{}',
      };
    }),
  },
];


export const lambdaHandler = middy()
  .use(httpHeaderNormalizer())
  .handler(httpRouterHandler(routes));
```

src/order-controller.mts

```javascript
import { APIGatewayProxyEvent, APIGatewayProxyResult } from 'aws-lambda';
import { OrderService } from './services/order-service.mjs';

export class OrderController {
  private orderService: OrderService;

  constructor(orderService: OrderService) {
    this.orderService = orderService;
  }

  getOrders = async (
    event: APIGatewayProxyEvent
  ): Promise<APIGatewayProxyResult> => {
    const orders = await this.orderService.getOrders();

    return {
      statusCode: 200,
      body: JSON.stringify({
        message: 'Orders fetched successfully',
        orders,
      }),
    };
  };
}

```






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

package.json


    {
      "name": "admin-service",
      "version": "1.0.0",
      "description": "Admin microservice",
      "main": "app.mjs",
      "type": "module",
      "scripts": {
        "lint": "eslint . --ext .mts,.ts",
        "build": "tsc -p tsconfig.json",
        "test": "vitest run",
        "test:coverage": "vitest run --coverage",
        "format:check": "prettier -c \"**/*.{ts,mts,js,json,cjs}\"",
        "format:write": "prettier -w \"**/*.{ts,mts,js,json,cjs}\""
      },
      "dependencies": {
        "@middy/core": "^5.3.5",
        "@middy/http-error-handler": "^5.3.2",
        "@middy/http-event-normalizer": "^5.4.2",
        "@middy/http-header-normalizer": "^5.4.2",
        "@middy/http-json-body-parser": "^5.3.2",
        "@middy/http-response-serializer": "^5.4.2",
        "@middy/http-router": "^5.4.2",
        "@types/aws-lambda": "^8.10.92",
        "winston": "^3.14.2",
        "zod": "^3.23.8"
      },
      "devDependencies": {
        "@types/node": "^18.11.4",
        "@typescript-eslint/eslint-plugin": "^5.10.2",
        "@typescript-eslint/parser": "^5.10.2",
        "@vitest/coverage-v8": "^1.6.0",
        "eslint": "^8.8.0",
        "eslint-config-prettier": "^8.3.0",
        "eslint-plugin-prettier": "^4.0.0",
        "prettier": "^2.8.8",
        "ts-node": "^10.9.1",
        "typescript": "^4.8.4",
        "vitest": "^1.6.0"
      },
      "optionalDependencies": {
        "@rollup/rollup-linux-x64-gnu": "^4.21.2"
      }
    }
