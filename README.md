# Awesome Project Build with TypeORM
        
Steps to run this project:

1. Run `npm i` command
2. Setup database settings inside `ormconfig.json` file
3. Run `npm start` command

# Start the project

- Add type orm interfaceusing quick start for now `typeorm init --name graphql-ts-server-boilerplate --database postgres`

```bash
npm install -g npm i npm-check-updates #checks for updates in package.json
ncu -a # updates all your versions # not recommended in the live projects

# Change ormconfig.json
# Change username, password, database name according to your system
createdb graphql-ts-server-boilerplate

npm install
npm start
```

- Change `tsconfig.json`

```json
// source: tsconfig.json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "lib": ["dom", "es6", "es2017", "esnext.asynciterable"],
    "sourceMap": true,
    "outDir": "./dist",
    "moduleResolution": "node",

    "removeComments": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "strictFunctionTypes": true,
    "noImplicitThis": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "allowSyntheticDefaultImports": false,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true
  },
  "exclude": ["node_modules"],
  "include": ["./src/**/*.tsx", "./src/**/*.ts"]
}
```

- Setup tslint

```bash
npm i --save-dev tslint tslint-config-prettier
```

> Reload the code editor the `tslint.json` is created.

```json
// source: tslint.json
{
  "defaultSeverity": "error",
  "extends": ["tslint:latest", "tslint-config-prettier"],
  "jsRules": {},
  "rules": {
    "no-console": false,
    "member-access": false,
    "object-literal-sort-keys": false,
    "ordered-imports": false,
    "interface-name": false,
    "no-submodule-imports": false
  },
  "rulesDirectory": []
}
```

- Remove the below code from `src/index.ts`

```ts
// Remove it to build our own tables
import {createConnection} from "typeorm";
import {User} from "./entity/User";

createConnection().then(async connection => {

    console.log("Inserting a new user into the database...");
    const user = new User();
    user.firstName = "Timber";
    user.lastName = "Saw";
    user.age = 25;
    await connection.manager.save(user);
    console.log("Saved a new user with id: " + user.id);
    
    console.log("Loading users from the database...");
    const users = await connection.manager.find(User);
    console.log("Loaded users: ", users);
     
    console.log("Here you can setup and run express/koa/any other framework.");
    
}).catch(error => console.log(error));
```

- Add the below piece of code into `src/index.ts`

```ts
// Source: src/index.ts
import "reflect-metadata";

import { GraphQLServer } from 'graphql-yoga'

const typeDefs = `
  type Query {
    hello(name: String): String!
  }
`

const resolvers = {
  Query: {
    hello: (_: any, { name }: any) => `Hello ${name || 'World'}`,
  },
}

const server = new GraphQLServer({ typeDefs, resolvers })
server.start(() => console.log('Server is running on localhost:4000'))
```

> Test with `yarn start`

Goto `localhost:4000` and test the below query
```
{
  hello
}
```


```bash
yarn add -D nodemon
```

- Update `package.json`. This listens for changes and reloads the server automaticallygit

```json
{
  ...

  "scripts": {
      "start": "nodemon --exec ts-node src/index.ts"
   }
}
```

## Creating TypeORM Entity Part 1

[Reference](https://www.youtube.com/watch?v=-iwjiiCGiO0)

- Right now we only have single entity `src/entity/User.ts`
- We are going to start from this and add on to it

> Each entity more or less correlates to a table in the database

- Here we have a single table named `User` we will rename it as `Users`

```ts
// Source: src/entity/User.ts
export class User {

    // Numeric number which just increments
    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    firstName: string;

    @Column()
    lastName: string;

    @Column()
    age: number;

}
// Changed to the below lines
export class User {

    // We shall add a library to automatically create uuid (npm i --save uuid)
    // Better one because it hides ID people can't guess it Ex: acgsjavh16213 16-bit number
    @PrimaryColumn("uuid")
    id: string;

    @Column()
    firstName: string;

    @Column()
    lastName: string;

    @Column()
    age: number;

}
```

- We shall add a library to automatically create uuid(npm i --save uuid or yarn add uuid)