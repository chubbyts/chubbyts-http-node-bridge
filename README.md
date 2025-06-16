# chubbyts-http-node-bridge

[![CI](https://github.com/chubbyts/chubbyts-http-node-bridge/workflows/CI/badge.svg?branch=master)](https://github.com/chubbyts/chubbyts-http-node-bridge/actions?query=workflow%3ACI)
[![Coverage Status](https://coveralls.io/repos/github/chubbyts/chubbyts-http-node-bridge/badge.svg?branch=master)](https://coveralls.io/github/chubbyts/chubbyts-http-node-bridge?branch=master)
[![Mutation testing badge](https://img.shields.io/endpoint?style=flat&url=https%3A%2F%2Fbadge-api.stryker-mutator.io%2Fgithub.com%2Fchubbyts%2Fchubbyts-http-node-bridge%2Fmaster)](https://dashboard.stryker-mutator.io/reports/github.com/chubbyts/chubbyts-http-node-bridge/master)
[![npm-version](https://img.shields.io/npm/v/@chubbyts/chubbyts-http-node-bridge.svg)](https://www.npmjs.com/package/@chubbyts/chubbyts-http-node-bridge)

[![bugs](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-http-node-bridge&metric=bugs)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-http-node-bridge)
[![code_smells](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-http-node-bridge&metric=code_smells)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-http-node-bridge)
[![coverage](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-http-node-bridge&metric=coverage)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-http-node-bridge)
[![duplicated_lines_density](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-http-node-bridge&metric=duplicated_lines_density)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-http-node-bridge)
[![ncloc](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-http-node-bridge&metric=ncloc)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-http-node-bridge)
[![sqale_rating](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-http-node-bridge&metric=sqale_rating)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-http-node-bridge)
[![alert_status](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-http-node-bridge&metric=alert_status)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-http-node-bridge)
[![reliability_rating](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-http-node-bridge&metric=reliability_rating)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-http-node-bridge)
[![security_rating](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-http-node-bridge&metric=security_rating)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-http-node-bridge)
[![sqale_index](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-http-node-bridge&metric=sqale_index)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-http-node-bridge)
[![vulnerabilities](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-http-node-bridge&metric=vulnerabilities)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-http-node-bridge)

## Description

A node req/res http bridge.

## Requirements

 * node: 18
 * [@chubbyts/chubbyts-http-types][2]: ^3.0.0

## Installation

Through [NPM](https://www.npmjs.com) as [@chubbyts/chubbyts-http-node-bridge][1].

```ts
npm i @chubbyts/chubbyts-http-node-bridge@^2.0.1
```

## Usage

```ts
import {
  createServerRequestFactory,
  createStreamFromResourceFactory,
  createUriFactory,
} from '@chubbyts/chubbyts-http/dist/message-factory';
import { createServer, IncomingMessage, Server, ServerResponse } from 'http';
import { createNodeToServerRequestFactory, createResponseToNodeEmitter } from '@chubbyts/chubbyts-http-node-bridge/dist/node-http';

const shutdownServer = (server: Server) => {
  server.close((err) => {
    if (err) {
      console.warn(`Shutdown server with error: ${err}`);
      process.exit(1);
    }

    console.log('Shutdown server');
    process.exit(0);
  });
};

const app = ...;

const nodeToServerRequestFactory = createNodeToServerRequestFactory(
  createUriFactory(),
  createServerRequestFactory(),
  createStreamFromResourceFactory(),
);

const responseToNodeEmitter = createResponseToNodeEmitter();

const server = createServer(async (req: IncomingMessage, res: ServerResponse) => {
  responseToNodeEmitter(await app(nodeToServerRequestFactory(req)), res);
});

const host = '0.0.0.0';
const port = 8080;

server.listen(port, host, () => {
  console.log(`Listening to ${host}:${port}`);
});

process.on('SIGINT', () => shutdownServer(server));
process.on('SIGTERM', () => shutdownServer(server));
```

## Copyright

2025 Dominik Zogg

[1]: https://www.npmjs.com/package/@chubbyts/chubbyts-http-node-bridge
[2]: https://www.npmjs.com/package/@chubbyts/chubbyts-http-types
