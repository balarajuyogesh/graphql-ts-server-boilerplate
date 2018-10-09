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
