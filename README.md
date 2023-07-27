# chubbyts-node-http-bridge

[![CI](https://github.com/chubbyts/chubbyts-node-http-bridge/workflows/CI/badge.svg?branch=master)](https://github.com/chubbyts/chubbyts-node-http-bridge/actions?query=workflow%3ACI)
[![Coverage Status](https://coveralls.io/repos/github/chubbyts/chubbyts-node-http-bridge/badge.svg?branch=master)](https://coveralls.io/github/chubbyts/chubbyts-node-http-bridge?branch=master)
[![Infection MSI](https://badge.stryker-mutator.io/github.com/chubbyts/chubbyts-node-http-bridge/master)](https://dashboard.stryker-mutator.io/reports/github.com/chubbyts/chubbyts-node-http-bridge/master)
[![npm-version](https://img.shields.io/npm/v/@chubbyts/chubbyts-node-http-bridge.svg)](https://www.npmjs.com/package/@chubbyts/chubbyts-node-http-bridge)

[![bugs](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-node-http-bridge&metric=bugs)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-node-http-bridge)
[![code_smells](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-node-http-bridge&metric=code_smells)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-node-http-bridge)
[![coverage](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-node-http-bridge&metric=coverage)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-node-http-bridge)
[![duplicated_lines_density](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-node-http-bridge&metric=duplicated_lines_density)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-node-http-bridge)
[![ncloc](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-node-http-bridge&metric=ncloc)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-node-http-bridge)
[![sqale_rating](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-node-http-bridge&metric=sqale_rating)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-node-http-bridge)
[![alert_status](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-node-http-bridge&metric=alert_status)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-node-http-bridge)
[![reliability_rating](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-node-http-bridge&metric=reliability_rating)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-node-http-bridge)
[![security_rating](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-node-http-bridge&metric=security_rating)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-node-http-bridge)
[![sqale_index](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-node-http-bridge&metric=sqale_index)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-node-http-bridge)
[![vulnerabilities](https://sonarcloud.io/api/project_badges/measure?project=chubbyts_chubbyts-node-http-bridge&metric=vulnerabilities)](https://sonarcloud.io/dashboard?id=chubbyts_chubbyts-node-http-bridge)

## Description

A node req/res http bridge.

## Requirements

 * node: 16
 * [@chubbyts/chubbyts-http-types][2]: ^1.2.3

## Installation

Through [NPM](https://www.npmjs.com) as [@chubbyts/chubbyts-node-http-bridge][1].

```ts
npm i @chubbyts/chubbyts-node-http-bridge@^1.2.0
```

## Usage

```ts
import {
  createServerRequestFactory,
  createStreamFromResourceFactory,
  createUriFactory,
} from '@chubbyts/chubbyts-http/dist/message-factory';
import { createServer, IncomingMessage, ServerResponse } from 'http';
import { createNodeToServerRequestFactory, createResponseToNodeEmitter } from '@chubbyts/chubbyts-node-http-bridge/dist/node-http';

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
```

## Copyright

2023 Dominik Zogg

[1]: https://www.npmjs.com/package/@chubbyts/chubbyts-node-http-bridge
[2]: https://www.npmjs.com/package/@chubbyts/chubbyts-http-types
