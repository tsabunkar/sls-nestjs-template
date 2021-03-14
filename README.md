## Running the app locally

Run in development mode as nestjs app

```bash
npm start:dev
```

or run using offline mode (like Serverless App)

```bash
npm run start:offline
```

### Skiping cache invalidation

Skiping cache invalidation is the same behavior as a deployed function

```bash
npm start -- --skipCacheInvalidation
```

### Deploy

In order to deploy the endpoint, simply run:

```bash
npm run build && sls deploy
```

or

```bash
npm run deploy:dev
```

- Goto AWS Management Console > Lambda > Functions > serverless-nest-template-dev-main
- Configuration (tab)
- API endpoint: https://wawiuis7da.execute-api.us-east-1.amazonaws.com/dev/
- hit this endpoint in the browser you will see hello-world :)

## Tail logs

```bash
sls logs --function main --tail
```

### Use Swagger for development

```
$ npx ts-node src/swagger.ts
```

```
[Nest] 6890   - 2019-03-24 15:11   [NestFactory] Starting Nest application...
[Nest] 6890   - 2019-03-24 15:11   [InstanceLoader] AppModule dependencies initialized +11ms
[Nest] 6890   - 2019-03-24 15:11   [RoutesResolver] AppController {/}: +224ms
[Nest] 6890   - 2019-03-24 15:11   [RouterExplorer] Mapped {/, GET} route +2ms
[Nest] 6890   - 2019-03-24 15:11   [NestApplication] Nest application successfully started +2ms
```

Then browse http://localhost:3001/api

**This function is for development.** If you want to use production, change package.json dependencies and serverless.yml.

### Benchmark

A basic benchmark script can be used locally, it performs 1000 "GET" requests on "http://localhost:3000/hello"

```bash
# /!\ The app must run locally
npm start # Or npm start -- --skipCacheInvalidation for better performances

# Run bench
node bench.js
```

The expected result should be similar to:

```bash
$ node bench.js
1000 "GET" requests to "http://localhost:3000/hello"
total: 8809.733ms
Average:  8.794ms
```

---

## Optional Moditifications

### Hot start

See : https://serverless.com/blog/keep-your-lambdas-warm/

These behavior can be fixed with the plugin serverless-plugin-warmup

1 Install the plugin

```
$ npm install serverless-plugin-warmup --save-dev
```

2 Enable the plugin

```
plugins:
  - '@hewmen/serverless-plugin-typescript'
  - serverless-plugin-optimize
  - serverless-offline
  - serverless-plugin-warmup

custom:
  # Enable warmup on all functions (only for production and staging)
  warmup:
      - production
      - staging
```

---

# Ref:

- https://github.com/serverless/examples/tree/master/aws-node-typescript-nest
- https://github.com/rdlabo-team/serverless-nestjs
