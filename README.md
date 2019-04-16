# Beefy Gainz

## Setup

Install `meta` globally.

```npm i -g meta```

Clone the meta repo.

```meta git clone https://github.com/azsuth/beefy-gainz.git```

## Services

![flow](./data/flow.png)

### Gateway

Node app that validates a google token ID. Provides simple, unauthenticated passthrough for all base routes. Authenticates routes beginning with `/api`. All traffic is passed to the router.

### Router

Nginx reverse proxy server.

### Client

Client web code.

### Exercise

Service providing CRUD operations for Exercises and Sets

## Data

![data](./data/data.png)