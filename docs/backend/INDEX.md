# Backend standards

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

_"It works on my end!"_ - is a known joke and phrase that everyone in IT industry heard at least once. To prevent this
kind of situations, we are using **Docker** to create development and production environments.

> **We use Docker in all backend projects in organization.**
>
> Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. Containers
> allow a developer to package up an application with all the parts it needs, such as libraries and other dependencies,
> and ship it all out as one package.

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

## Getting Started with GitHub

> We use GitHub to organize our work and collaborate on projects.
>
> You can learn more here:
>
> - [Git & GitHub Roadmap](https://roadmap.sh/git-github)
> - [Interactive Git branching tutorial](https://learngitbranching.js.org/)

> Below you’ll find the basic authentication setup.  
> Once you complete it, you’ll be able to clone our repositories and start working.
>
> Run all commands in **Windows PowerShell** or a **Linux terminal** as a **regular user**.  
> Configuration is stored locally and will be used on each contribution.

1. **Set up your Git identity**

   ```shell
   git config --global user.email "your_email@example.com"
   git config --global user.name "your_name"
   ```

2. **Generate an SSH authentication key**

   ```shell
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```

   You will be asked to specify a file location and passphrase — you can accept the defaults and leave the passphrase blank.

3. **Enable the SSH agent**

   > The `ssh-agent` service must be running for your SSH key to work.

   **[Linux]**

   ```shell
   eval "$(ssh-agent -s)"
   ```

   **[Windows]**

   > Run this code in a **new Windows PowerShell window as Administrator**.

   ```powershell
   Get-Service -Name ssh-agent | Set-Service -StartupType Automatic
   Start-Service ssh-agent
   ```

4. **Add your private key to the agent**

   > If you used a custom key name, adjust the file path accordingly.

   **[Linux]**

   ```shell
   ssh-add ~/.ssh/id_ed25519
   ```

   **[Windows]**

   ```powershell
   ssh-add $env:USERPROFILE\.ssh\id_ed25519
   ```

5. **Copy your public key and add it to GitHub**

   **[Linux]**

   ```shell
   cat ~/.ssh/id_ed25519.pub
   ```

   **[Windows]**

   ```powershell
   cat $env:USERPROFILE\.ssh\id_ed25519.pub
   ```

   Copy the entire key (including the email) and paste it on the  
   [**Add new SSH key** page on GitHub](https://github.com/settings/ssh/new).  
   Give it a descriptive title and do **not** change the key type.  
   After that, you’ll be able to authenticate with GitHub from your terminal.

   > **Signing commits:**  
   > To use the same key for commit signing:
   >
   > - Copy the same **public key** again.
   > - Go to [**Add new SSH key**](https://github.com/settings/ssh/new).
   > - Give it a descriptive title and set the **key type** to “Signing key”.

   ***

   > **Verification step:**  
   > Test your SSH key setup by connecting to GitHub:
   >
   > ```shell
   > ssh -T git@github.com
   > ```
   >
   > You should see:  
   > `"Hi username! You've successfully authenticated, but GitHub does not provide shell access."`

6. **Add signing key configuration**

   > If you used a custom key name, adjust the file path accordingly.

   ```shell
   git config --global gpg.format ssh
   git config --global user.signingkey ~/.ssh/id_ed25519.pub
   git config --global commit.gpgsign true
   ```

7. **Configure line endings (Windows only)**

   > Run this step only on **Windows** systems to ensure Docker compatibility.

   ```powershell
   git config --global core.autocrlf false
   git config --global core.eol lf
   ```
