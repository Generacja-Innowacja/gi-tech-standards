# Backend tech stack

## Languages and technologies

All of our services are using **Node.js** with **TypeScript** and **Nest.js** framework to organize
code.

> **Our recommendation is to use this stack for all new backend projects in organization.**
>
> JavaScript is one of the most popular languages on the planet, making our code easiest to maintain. In organization
> where all developers are volunteers, we must write in language that is easiest to learn and where time cost of taking
> over a project is possibly the lowest.
>
> Also, all of these technologies have large communities and there are a lot of answers in the Internet for common
> issues new developers may encounter. Last, but not least: this stack is also very well handled by language models such
> as ChatGPT or GitHub Copilot.

Read more about those technologies:

- [JavaScript (MDN web docs)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- [TypeScript (official docs)](https://www.typescriptlang.org/)
- [Node.js (project docs)](https://nodejs.org/en)
- [Nest.js (framework docs)](https://nestjs.com/)

Awesome site that may help start you a web developer career is **roadmap.sh**. It provides a roadmaps describing
learning curve to be a successful programmer. Make sure to check these maps out:

- [Backend roadmap (generic)](https://roadmap.sh/backend)
- [JavaScript roadmap](https://roadmap.sh/javascript)
- [TypeScript roadmap](https://roadmap.sh/typescript)
- [Node.js roadmap](https://roadmap.sh/nodejs)
- [Docker roadmap](https://roadmap.sh/docker)

> **You cannot start a project in other stack than listed above without prior approval from organization Technical
> Leader.**
>
> Don't feel anxious to ask for approval. We are here to help you, and we want to make sure that you are using the best
> tools for the job.

## Environments

*"It works on my end!"* - is a known joke and phrase that everyone in IT industry heard at least once. To prevent this
kind of situations, we are using **Docker** to create development and production environments.

> **We use Docker in all backend projects in organization.**
>
> Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. Containers
allow a developer to package up an application with all the parts it needs, such as libraries and other dependencies,
and ship it all out as one package.

> **We are using Docker both for development and production environments.**
>
> This way we can be sure that our code will work in the same way on every machine, no matter if it's a developer's
> laptop or a production server.

> **We are using one Dockerfile standard across our projects.**
>
> Since our backend services are almost identical when it comes to system configuration, we are using one Dockerfile
> standard across all of our projects. You can look at these repositories to see how it looks like:
>
> - [dzialaj-org-api](https://github.com/Generacja-Innowacja/dzialaj-org-api/blob/main/Dockerfile)
> - [mypolitics-survey-producer-api](https://github.com/Generacja-Innowacja/mypolitics-survey-producer-api/blob/main/Dockerfile)

> **We use multi-stage builds to keep our images as small as possible.**
>
> This way we can reduce the time needed to build and push images to the registry. On production environment we are
> using only production dependencies, without any development tools such as test libraries or other dev runtime
> packages.

Read more about Docker:

- [Docker (official docs)](https://docs.docker.com/)
- [Docker Compose (official docs)](https://docs.docker.com/compose/)

## Databases

> **We are using **PostgreSQL** as our main database engine.**
>
> It's a powerful, open-source object-relational database system that uses and extends the SQL language combined with
> many features that safely store and scale the most complicated data workloads.
>
> However, since your project may have different requirements, you can use any other database. If you want to consult
> your choice, feel free to ask for advice from organization Technical Leader.
