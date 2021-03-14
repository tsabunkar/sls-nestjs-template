## Running the app locally

```bash
npm start
```

or using offline mode

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
npm run deploy:dev
```

## Tail logs

```bash
sls logs --function main --tail
```

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
