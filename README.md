# Maybe: An open-source personal finance app

🚨 NOTE: This is the original React/Next.js app of the now-defunct personal finance app, Maybe. This original version used many external services (Plaid, Finicity, Auth0, etc) and getting it to fully function will be a decent amount of work.

The README below was what we used internally, so many of the links won't work and the instructions won't necessarily be applicable.

There's a LOT of work to do to get this functioning, but it should be feasible.

The best way to get involved is on [Discord](https://discord.gg/xfysSaSsfN) and in the [Issues](https://github.com/maybe-finance/maybe/issues).

## Monorepo File Structure Overview

This repository uses the monorepo management tools from NRWL called `nx`. The NX dev tools come with pre-configured TS, ESLint, Prettier, Jest, Cypress and more, and provide an extensive suite of commands to lint, test, serve, and build applications. [Here's a great 10 minute video](https://nx.dev/l/r/getting-started/intro#10-minute-nx-overview) that walks through what nx can do.

### Structure

**Notes**

Through ESLint, the following rules apply:

- libs/shared can be imported to any app OR lib
- libs/server can be imported to server and workers apps
- libs/client can be imported to client app
- libs/client/shared can be imported to any libs/client/features
- libs/server/shared can be imported to any libs/server/features

```
apps/
  client/
  server/
  workers/
libs/
  design-system/
  client/
    src/
      features/
        {feature1-name}/
        {feature2-name}/
      shared/
  server/
    src/
      features/
        {feature1-name}/
        {feature2-name}/
      shared/
  shared/
    src/
      features/
        {feature1-name}/
        {feature2-name}/
      utils/
      types/
```

### Decision Tree

![folder-structure-diagram](https://github.com/maybe-finance/maybe/assets/35243/fbe702b0-a6a7-41b1-a677-80ff7fe7f656)


----

## ⚠️ Everything below is archived from the original repo and we're slowly working to replace/update it. 

# Quick Start

For an overview of this repository, please [see the wiki](https://github.com/maybe-finance/maybe-app/wiki)

## System Prerequisites

-   Docker (if not using Docker, you will need Node LTS 14.7.x and Postgres 13.x)
-   (Optional, highly recommended) - Install the [NX Console](https://marketplace.visualstudio.com/items?itemName=nrwl.angular-console) for [using the nx client](#nrwl-nx-overview)

## Run the app locally

### Setup ENV

```
cp .env.example .env
```

A working local development `.env` file can be found in 1Password under the "Engineering" folder.

### With Docker (preferred)

#### Start server and client apps

```
yarn install
yarn dev
```

#### Migrate DB

In a separate terminal, run the following command. This will connect to the Postgres DB running inside Docker and run all the migrations in `/prisma/migrations`.

```
yarn prisma:migrate
```

You will also want to seed the database (includes account types and subtypes for categorization).

```
yarn prisma:seed
```

### Manually

_NOTE: Make sure Postgres 13.x is running on your machine_

```
yarn install
nx serve client # Terminal 1
nx serve server # Terminal 2
yarn prisma:migrate && yarn prisma:seed # Terminal 3 - after apps are running
```

# Reference

## Authentication

[See this wiki page](https://github.com/maybe-finance/maybe/wiki/Auth0) for an explanation of how authentication/authorization works in this codebase.
