# ts-node-server [WIP]
[![Build Status](https://travis-ci.com/henry781/ts-node-server.svg?branch=master)](https://travis-ci.com/henry781/ts-node-server)

ts-node-server is node framework for developing RESTful web services in Typescript.

It pulls together some of the best node libraries :

* [Fastify](https://github.com/fastify/fastify) : Fast and low overhead web framework, for Node.js

* [Pino](https://github.com/pinojs/pino) : Super fast, all natural JSON logger for Node.js

* [Inversify](https://github.com/inversify/InversifyJS) : A powerful and lightweight inversion of control container for JavaScript & Node.js apps powered by TypeScript.

* [Swagger UI](https://github.com/swagger-api/swagger-ui) : A collection of HTML, Javascript, and CSS assets that dynamically generate beautiful documentation from a Swagger-compliant API.

* [MongoDB driver](https://github.com/mongodb/node-mongodb-native) : Mongo DB Native NodeJS Driver

## Features

### Route decorators

ts-node-server use decorators to build *fastify* routes. 

```
@controller('/v1/users')
export class UserController {

    @httpGet(':name')
    public async get(@pathParam('name')name: string) {
    }

    @httpPost()
    public async create(@queryParam('clone')clone: boolean) {
    }
```

### Type validation

ts-node-server use *tipify* to validate, serialize and deserialize. It ensures that no property can be accidentally exposed.

```
@jsonObject()
export class StellarSystem {

    @jsonProperty('_id', ObjectIdConverter)
    private _id?: string;

    @jsonProperty('name', String)
    private _name?: string;

    @jsonProperty('planets', [Planet])
    private _planets?: Planet[];
} 
```

### Swagger generator

ts-node-server use route decorators and tipify decorators to build a swagger configuration.

### Metrics

ts-node-server imports [fastify-metrics](https://github.com/fastify/fastify-metrics) and exposes all your app metrics at `/metrics`.

### Healthcheck

ts-node-server provides an healthcheck (`/healthcheck`). You can add more checks by extending `Healthcheck` class :

```
@injectable()
export class MongoHealthcheck implements Healthcheck {

    constructor() {
    }

    public getName(): string {
        return 'mongodb';
    }

    public check(): Promise<HealthcheckResult> {
        return {
            true,
            'content'
        };
    }

}
```

### Authentication

## Usage

See [ts-node-server-starter](https://github.com/henry781/ts-node-server-starter) for an example.
