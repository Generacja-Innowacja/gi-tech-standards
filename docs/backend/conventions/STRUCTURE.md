# Structure

Keeping the project structure in a one, standardized manner is important. Developers in an organization often switch
between different projects, and a similar structure keeps things organized.

## Top-level structure

For repository structure for server-side applications developer SHOULD follow the standard, recommended by Nest.js 
structure.

On the top level, these directories are present in any running project:
```
.
├── .github/
├── dist/
├── docker/
├── features/
├── node_modules/
├── prisma/
└── src/
```

In the structure as above, each directory serves its own purpose:
- `.github` directory contains the GitHub workflows and other configuration files,
- `dist` contains the compiled application,
- `docker` contains the docker-related environment configuration and scripts,
- `features` contains the functional tests and contexts required to run those tests,
- `node_modules` contains the installed dependencies,
- `prisma` directory contains the database schema, database test data and generated database client.
- `src` directory contains the source code of the application.

> **#1: Only directories listed above SHOULD be present in the repository.**

> **#2: The `dist` and `node_modules` directory MUST NOT be present in the repository.**

## Source code

Application source code is divided:
```
.
└── src/
    ├── core/
    ├── modules/
    ├── app.module.ts
    └── main.ts
```

Source code is divided into the following directories:
- `core` contains the core app features, that are not related to any specific module (domain),
- `modules` contains the application modules — the domain-specific features.

> **#3: Only `core/` and `modules/` directories SHOULD be present in the `./src/` directory.**

> **#4: No files SHOULD be present in the `./src/` directory directly, except for the `app.module.ts` and `main.ts` file.**

> **#5: Application entrypoint SHOULD be present in the `./src/` directory, and it SHOULD be named `main.ts`.** 

> **#6: The `app.module.ts` file SHOULD be present in the `src` directory.**

### Core

Core features are the features that are not related to any specific module.

### Modules

Modules are the domain-specific features of the application. Each module should have its own directory and should be 
responsible for a specific domain of the application.

An example directory structure looks like that:

```
.
└── src/
    ├── core/
    └── modules/
        ├── users/
        ├── offers/
        └── surveys/
```

> **#7: Directories under the `./src/modules` directory SHOULD be named after the domain they represent.**
> 
> It is RECOMMENDED to use the plural form of the domain name, and it is also RECOMMENDED to use single-word names.

#### Minimal module structure

The simplest module should contain only the `<domain>.module.ts` file. All other directories and files are up for developer
consideration.

#### Recommended module structure (CQRS)

Once the module begins to be bigger and more complex, it is recommended to split it into DDD-like structure. Defining
`application`, `infra`, `model` layers is a good practice.

```
.
└── src/
    ├── core/
    └── modules/
        ├── users/
        ├── offers/
        └── surveys/
            ├── application/
            ├── infra/
            ├── model/
            └── surveys.module.ts
```

In this structure layers are defined as follows:
- `application` layer is responsible for commands and queries (CQRS).
- `infra` layer is responsible for the close-to-metal actions: database read/write, handling HTTP requests and so on.
- `model` layer is responsible for keeping the business decisions and data structures as a model.

Request comes from `infra` level (usually an HTTP request), it is processed by `application` layer that uses
`model` to understand the logic of the domain. Database changes are reflected by `infra` layer and then response is sent
back to the client also by `infra` layer. 

Fully operating domain may look like that:
```
.
└── src/
    ├── core/
    └── modules/
        ├── users/
        ├── offers/
        ├── surveys/
        │   ├── application/
        │   │   ├── command/
        │   │   │   ├── create-offer.command.ts
        │   │   │   └── assign-candidate-to-offer.ts
        │   │   └── query/
        │   │       ├── get-all-offers.query.ts
        │   │       └── get-offer-by-id.query.ts
        │   ├── infra/
        │   │   ├── database/
        │   │   │   └── repository/
        │   │   │       ├── offers.repository.ts
        │   │   │       └── candidates.repository.ts
        │   │   └── http/
        │   │       ├── controller/
        │   │       │   ├── offers.controller.ts
        │   │       │   └── candidates.controller.ts
        │   │       └── request/
        │   │           ├── offers.request.ts
        │   │           └── candidates.request.ts
        │   └── model/
        │       ├── offer.model.ts
        │       └── candidate.model.ts
        └── surveys.module.ts
```
