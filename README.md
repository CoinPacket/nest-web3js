# Web3js module for NestJS that allow to work with blockhains

This is first release of this module. Readme under construction but here are a couple of tips

## Installation

#### Yarn
`yarn add @coinpacket/nest-web3js`

#### NPM
`yarn add @coinpacket/nest-web3js`

## Getting started with module

Register Web3Module module in yours `app.module.ts` (or other main module of yours project)

```typescript
import { Module } from '@nestjs/common';
import { Web3Module } from '@coinpacket/nest-web3js';

@Module({
    imports: [
        Web3Module.forRoot({
            name: 'eth',
            url: 'http://localhost:3450',
        }),
    ]
})
export class AppModule {}

```

Or with Async

```typescript
import { Module } from '@nestjs/common';
import { Web3Module } from '@coinpacket/nest-web3js';

@Module({
    imports: [
        Web3Module.forRootAsync({
            useFactory: (configService: ConfigService) => configService.get('web3'),
            inject:[ConfigService]
        }),
    ]
})
export class AppModule {}
```

### Configuration

For now module accept two parameters:

```typescript
export interface Web3ModuleOptions {
  name?: string;
  url: string;
}
```

### Using in project

```typescript
import { Injectable } from '@nestjs/common';
import { Web3Service } from "@coinpacket/nest-web3js";

@Injectable()
export class SomeClass {
    constructor(
        private readonly web3Service: Web3Service
    ) {}
    
    async method(): Promise<number> {
        const client = this.web3Service.getClient('eth'); // we are give name of client in config file
        return await client.eth.getChainId();
    }
}
```

Available methods and API of Web3 available here https://web3js.readthedocs.io/

## About
Fork from https://github.com/owl1n/nestjs-web3