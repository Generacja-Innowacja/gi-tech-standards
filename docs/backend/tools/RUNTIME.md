# Runtime environment

The following technology stack is selected for server-side apps:

- [Docker](https://www.docker.com/)
- [Node.js](https://nodejs.org/)
- [Nest.js](https://nestjs.com/)
- [PostgreSQL](https://www.postgresql.org/)

> **#0: Do not start a project in another stack than listed above, without a prior approval from the _Engineering_
> team.**
>
> Do not feel anxious to ask for the approval. They are here to help, and they want to make sure that the best tools for
> the job are used.

## Docker

> **#1: Use Docker-based runtime environments in server-side projects.**
>
> _“It works on my end”_ is a known joke and phrase that everyone in the IT industry heard at least once. To prevent
> this, **Docker** should be used to create development and production environments.
>
> Docker is a tool designed to make it easier to create, deploy, and run applications in different environments by using
> containers. Containers allow a developer to package up an application with all the parts it needs, such as libraries
> and other dependencies, and ship it all out as one package.

> **#2. Use Docker containers for development and production environments.**
>
> By using virtualization, the code will work in the same way on every machine: no matter if it is a developer's
> laptop or a production server.

> **#3. Use Alpine Linux as a base image for Docker containers.**

> **#4: Use standardized Dockerfile across different projects.**
>
> Aim to maintain backend services almost identical when it comes to system configuration. One Dockerfile should be used
> as a standard across all the projects. Take a look at these repositories to see how it is implemented:
>
> - [dzialaj-org-api](https://github.com/Generacja-Innowacja/dzialaj-org-api/blob/main/Dockerfile)
> - [mypolitics-survey-producer-api](https://github.com/Generacja-Innowacja/mypolitics-survey-producer-api/blob/main/Dockerfile)

> **#5. Use multi-stage builds to keep our images as small as possible.**
>
> This way we can reduce the time needed to build and push images to the registry. In a production environment we are
> using only production dependencies, without any development tools, test libraries, and other development-related
> packages.

> **#6. Expose framework default port in the container.**
>
> For **Nest.js**, it is port `3000`.

> **#7. Tie services together using Docker Compose for local development.**

Read more about Docker:

- [Docker (official docs)](https://docs.docker.com/)
- [Docker Compose (official docs)](https://docs.docker.com/compose/)

## Node.js & TypeScript

> **#1: Use Node.js in version 24.**
>
> Use the latest LTS version of Node.js to ensure access to modern JavaScript features, performance improvements,
> and leading security standards. Node.js 24 provides excellent support for ES modules, improved performance, and better
> security.

> **#2: Use `npm` as package manager for Node.**

> **#3: Use TypeScript in version 5.9.**
>
> TypeScript brings type safety to JavaScript, catching errors at compile-time rather than runtime. This significantly
> reduces bugs and improves the developer experience with better IDE support and autocomplete.

> **#4: Use standardized `tsconfig.json`.**
>
> Example:
>
> - [standardized tsconfig.json file](https://github.com/oskarbarcz/flight-tracker-api/tsconfig.json)

Read more about Node.js:

- [Node.js official documentation](https://nodejs.org/)
- [Node.js release schedule](https://github.com/nodejs/release#release-schedule)

Read more about TypeScript:

- [TypeScript official documentation](https://www.typescriptlang.org/)
- [TypeScript handbook](https://www.typescriptlang.org/docs/handbook/intro.html)

## Nest.js

> **#1: Use Nest.js in version 11.**

Read more about Nest.js:

- [Nest.js official documentation](https://docs.nestjs.com/)

## Databases

> **#1: For relational databases, use PostgreSQL in version 15.**
>
> **PostgreSQL** a powerful, open-source object-relational database system that uses and extends the SQL language
> combined with many features that safely store and scale the most complicated data workloads, while still keeping
> reasonable performance and cost-effectiveness.

> **#2: Ask for advice before using any other database engine.**
>
> To avoid unnecessary costs and additional complexity, do not use any other database engine than PostgreSQL.
>
> Feel free to ask for advice about what database engine to use for a new project. **Organization is open to using any
> other database engines if they fit the project requirements better than PostgreSQL**, but each decision must be
> consulted by the **_Engineering_** team before proceeding.

> **#3: Use Prisma ORM for database access layer.**

> **#4: If applicable, use Prisma in version 7.**

> **#5: If applicable, keep Prisma client in `prisma/client/` directory.**

Read more about Prisma:

- [Nest.js official documentation](https://docs.nestjs.com/)
