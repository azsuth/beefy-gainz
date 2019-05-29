# Beefy Gainz

## Related Repositories

All related repositories are named `beefy-gainz-{service name}`.

[beefy-gainz-client](https://github.com/azsuth/beefy-gainz-client) [![Build Status](https://travis-ci.org/azsuth/beefy-gainz-client.svg?branch=master)](https://travis-ci.org/azsuth/beefy-gainz-client)

[beefy-gainz-gateway](https://github.com/azsuth/beefy-gainz-gateway) [![Build Status](https://travis-ci.org/azsuth/beefy-gainz-gateway.svg?branch=master)](https://travis-ci.org/azsuth/beefy-gainz-gateway)

[beefy-gainz-router](https://github.com/azsuth/beefy-gainz-router) [![Build Status](https://travis-ci.org/azsuth/beefy-gainz-router.svg?branch=master)](https://travis-ci.org/azsuth/beefy-gainz-router)

[beefy-gainz-ingress](https://github.com/azsuth/beefy-gainz-ingress) [![Build Status](https://travis-ci.org/azsuth/beefy-gainz-ingress.svg?branch=master)](https://travis-ci.org/azsuth/beefy-gainz-ingress)

[beefy-gainz-exercise](https://github.com/azsuth/beefy-gainz-exercise) [![Build Status](https://travis-ci.org/azsuth/beefy-gainz-exercise.svg?branch=master)](https://travis-ci.org/azsuth/beefy-gainz-exercise)

[beefy-gainz-db](https://github.com/azsuth/beefy-gainz-db) [![Build Status](https://travis-ci.org/azsuth/beefy-gainz-db.svg?branch=master)](https://travis-ci.org/azsuth/beefy-gainz-db)

## Setup

Install `meta` globally.

```npm i -g meta```

Clone the meta repo.

```meta git clone https://github.com/azsuth/beefy-gainz.git```

## Running Locally

`docker` and `docker-compose` are required for running locally.

In the root `/beefy-gainz` repo, run `docker-compose up -d` to start all the services. The `Gateway` and `Client` applications will live reload without needing to be restarted (the browser will need to be refreshed when client code is changed).

An `idToken` header is necessary to authenticate with the backend APIs. Upon logging in with Google, the `idToken` is printed to the `Gateway` logs and can be obtained with `docker-compose logs -f gateway`. This can then be used with Postman for subsequent requests.

The client code is hosted at `http://localhost:3001`. The APIs are hosted behind `http://localhost:3001/api`, for example `GET http://localhost:3001/api/exercises` will return a list of exercises.

## Services

![flow](./data/flow.png)

### Gateway

Node app that validates a google token ID with `google-auth-library`. Traffic is proxied through to the appropriate service, based on the base path.

### Router

**ONLY IN DEVELOPMENT ENVIRONMENT**. Nginx reverse proxy server that routes traffic either to the gateway or client service.

### Ingress

**ONLY IN PRODUCTION ENVIRONMENT**. Yaml file describing a kubernetes ingress service, ClusterIssuer and Certificate for secure ingress into the beefy gainz application.

### Client

**Development:** create-react-app server hosting the development client code.<br>
**Production:** Static assets served from an nginx container.

### Exercise

Spring application providing CRUD operations for Exercises and Sets.

### Postgres

A container running postgres. On startup a script creates the table schema and a single user account with SELECT, INSERT, UPDATE, DELETE priviledges.

## Data

![data](./data/data.png)