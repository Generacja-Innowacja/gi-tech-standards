# GitHub repository standards

These guidelines ensure a consistent, maintainable, and robust backend codebase across all services developed
under our organization.

## Before you start

Hello dear volunteer, it's so nice to have you! To help us keep technical standards, please read steps below before 
starting work in any of Generacja Innowacja projects.

### Host OS

All our projects are well tested both on **Ubuntu 22.04** and **macOS Sonoma**. Some team members were also using **Windows**
for development, however it was very problematic. Use other platforms only on your own responsibility.
### Git

To enhance security, we require you to configure your local development environment in the way we can recognise your
identity. Please set up local `git` to add metadata on each push. You can do that by setting:

```shell
# replace <your name and surname> with your real name
git config user.name "<your name and surname>"

# replace <your email> with your real email that ends on @gi.org.pl
# if you don't have that email, contact administrator
git config user.email "<your email>"

# we usually recommend to sign off commits with SSH key you already have in your system
git config gpg.format ssh

# replace <path to your ssh key> with your real SSH public key
# example: ~/.ssh/id_ed25519.pub
git config user.signingkey <path to your ssh key>
```

You need to repeat these steps on each new machine you'll be using for development and in each of the projects. 
**Pull requests containing unsigned commits will not be possible to merge.**

### GitHub

On the GitHub platform we require two additional security steps:
- add your organization email address (ending with __@gi.org.pl__) to your account
  (you can do it [here](https://github.com/settings/emails)),
- enable 2-factor authorization in your **GitHub** account
  (you manage it [here](https://github.com/settings/security)),
- add your real name to your **GitHub** profile

These steps are allowing us to control exactly who is introducing the new changes into our repositories, thank you for
staying compliant with these rules.

That's all for now - happy coding!
