<div align="center">
</div><br>
<h1 align="center">
  Ardwells (NestJS Headless API)
</h1>

<p align="center">
<img alt="GitHub package.json version" src="https://img.shields.io/github/package-json/v/gobeam/truthy">
<img alt="Workflow test" src="https://github.com/gobeam/truthy/actions/workflows/ci.yml/badge.svg">
<img alt="GitHub" src="https://img.shields.io/github/license/gobeam/truthy">
<img alt="Lines of code" src="https://img.shields.io/tokei/lines/github/gobeam/truthy">
<img src='https://www.codetriage.com/gobeam/truthy/badges/users.svg' alt='Open Source Helpers' />
</p>
<p align="center">
<a href="https://www.buymeacoffee.com/ardwells" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-green.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>
</p>
<p align="center">
  <sub>Created by <a href="https://www.linkedin.com/in/ardiansyah-welly/">Welli Ardiansyah</a>.</sub>
</p>


## Table of Contents

- [Getting Started](#getting-started)
- [Prerequisites](#Prerequisites)
- [Available Scripts](#available-scripts)
- [Setup](#setup)
- [Docker Setup](#docker-setup)
- [File Structure](#file-structure)
- [Application Security](#application-security)

---

## Getting Started

This project was created to help developers by bootstrapping basic modules that need to be present while creating a standard CMS. The main motto of this project was to save precious time while developing CMS and focus more on the core part. This project is trying to follow the best possible standard to make it optimized and production-ready. Hope you like it.

---

## Prerequisites

NodeJS
https://nodejs.org/en/

Typescript
https://www.typescriptlang.org/

PostgresQL
https://www.postgresql.org/

Redis
https://redis.io/

---

### `yarn start:dev`

Runs the app in the development & watch mode.<br>
Open [http://localhost:7777/api-docs](http://localhost:7777/api-docs) to view swagger API docs in browser (only available in development mode).<br>
You will also see any lint errors in the console.

### `yarn build`

Builds the app for production to the `build` folder.<br>

### `yarn lint`

Lints all the files inside src,apps,libs,test folders and shows the results.

### `yarn format`

Formats all the files inside src using prettier with config provided in .prettierrc

### `yarn format`

Formats all the files inside src using prettier with config provided in .prettierrc

### `yarn coverage`

Runs coverage test command and creates coverage folder with detail report which can be checked with:
```bash
yarn coveralls
```

### `yarn orm-create migration_file_name`

Uses Type ORM to create a migration file. `migration_file_name` is Migration file name to be created.

### `yarn migrate`

This command is used to migrate existing migration file.

### `yarn migration:rollback`

This command is used to rollback migration.

### `yarn seed`

This command is used to run existing seeders.

---

## Setup

First, you need to install the project using npx command

```bash
npx ardwells-api
```

or clone it using

```bash
https://github.com/welliardiansyah/project-backend.git
```
**You also need to run PostgresQL for database and Redis for key-val storage which will be used for queue and throttling.**
After cloning the make changes in configuration file that exists in config folder which exists in root of project.
File names are named in accordance with environment you run project with. For example if you're running project in development environment you should make change in configuration of development.yml file. 
**Please keep in mind environment variables always overrides the config.**

If you want to run locally,
```bash
yarn start
```
*If you want to view swagger docs on development open http://localhost:7777/api-docs (assuming you are running application on 7777 port)*

Run Migration
```bash
yarn migrate
```

Run Seeders
```bash
yarn seed
```

Rollback Migration
```bash
yarn migration:rollback
```

---

## Docker Setup

**If you want to run project without docker you will not need to create .env file**

If you want to use **Docker** to deploy it on production or development stage
First create a .env file copying from .env.example and add environment for below parameters only since it will be used for building container using docker-compose

```env
SERVER_PORT=7777
DB_PASSWORD=root
DB_USERNAME=postgres
DB_DATABASE_NAME=ardwells
DB_PORT=5488
REDIS_PORT=6399
```

After creating env file make changes in configuration in accordance with you development environment. Follow setup guide in case you missed it.
 
Now to run containers do
```bash
docker-compose build .
docker-compose up -d
```
These commands will run 3 containers for PostgresQL, Redis and Main API.

To run migration on docker container
```bash
docker exec -it <container_id_or_name> yarn migrate
```

To run seeder on docker container
```bash
docker exec -it <container_id_or_name> yarn seed
```

---

## File Structure

This project follows the following file structure:

```text
truthy
├── config                                  * Contains all configuration files
│   └── default.yml                         * Default configuration file.
│   └── development.yml                     * Configuration file for development environment.
│   └── production.yml                      * Configuration file for production environment.
│   └── test.yml                            * Configuration file for test environment.    
├── coverage                                * Coverage reports after running `yarn coverage` command. 
├── dist                                    * Optimized code for production after `yarn build` is run.
├── images                                  * this folder is where uploaded profile images are stored. This folder is git ignored.
├── src                  
│   └── <module>                            * Folder where specific modules all files are stored
│       └── dto                             * Data Transfer Objects.
│       └── entity                          * Models for module.
│       └── pipes                           * Includes validation pipes for NestJS modules.
│       └── serializer                      * Includes serializer for model data.
│       └── <module>.controller.ts          * Controller file.
│       └── <module>.module.ts              * root module file for module.
│       └── <module>.service.ts             * Service file for <module>.
│       └── <module>.service.spec.ts        * Test file for service.
│       └── <module>.repository.ts          * Repository file for <module>.
│       └── <module>.repository.spec.ts     * Test file for repository.
│   └── common                              * Common helpers function, dto, entity, exception, decorators etc.
│   └── config                              * Configuration variables files.
│   └── database                            * Database folders that includes migration and seeders file
│       └── migrations                      * Migration folder includes all migration files.
│       └── seeds                           * Seeds folder includes all seeders files.
│   └── exception                           * Exception folder includes custom exceptions.
│   └── app.module.ts                       * Root module of the application.
│   └── main.ts                             * The entry file of the application which uses the core function NestFactory to create a Nest application instance.
├── test                                    * Contains E2E tests 
```

**Some important root files**

```text
.
├── .editorconfig                           * Coding styles (also by programming language).
├── .env                                    * Environment variables for docker.
├── .prettierrc.js                          * Formatting Prettier options.
├── .eslintrc.js                            * ESLint configuration and rules.
├── .docker-compose.yml                     * Docker compose configuration.
├── Dockerfile                              * Docker file for prod environment.
├── Dockerfile.dev                          * Docker file for dev environment.
├── tsconfig.json                           * Typescript configuration for application.
```

---

## Application Security

### Throttle

By default Throttle has been implemented for all API's. Redis is default driver to record throttle state data. You can easily change configuration from config files.

### Two Factor Authentication (2FA)

User Will have 2FA authentication option available to be turned on or off. For 2FA time-based one-time password is used. A time-based one-time password (TOTP) application automatically generates an authentication code that changes after a certain period of time. Applications like [Authenticator](https://play.google.com/store/apps/details?id=com.azure.authenticator&hl=en&gl=US), [1Password](https://support.1password.com/one-time-passwords/), [Authy](https://authy.com/guides/github/) etc. can be used to generate TOTP. When you enable 2FA, you will be sent a QR code in your email which should be scanned from above mentioned application and TOTP will be generated by those applications.

---
