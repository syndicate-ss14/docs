---
authors: [portfiend]
tags:
  - guides
  - maintainers
---

# General Maintainer's Guide

:::note
This document was copy-pasted from [portfiend](/blog/authors/portfiend)'s document archive and is not specific to Macrocosm. It may be subject to further iteration in the future.
:::

This is a guide to the various conventions and procedures that Space Station 14 server maintainers use to upkeep their servers and maintain code standards / game stability.

In SS14, a **maintainer** is a staff position in a server given the privilege to integrate new changes into the game. They will perform code reviews on new feature additions ("pull requests") in order to bring them to a certain standard of quality. On many servers, maintainers have the responsibility of guiding the game's design - ensuring all new features "fit in" to the atmosphere the server wants - and fixing any game-breaking bugs that emerge as a result.

In other words - a maintainer's job is to ensure that the game keeps improving. SS14 is an open-source project that often encourages players to add things to the game that they want to see. Maintainers ensure everything fits together nicely enough that these changes can be added to the server with as few issues as possible.

Currently, few guides exist to explain the responsibilities of a maintainer, or how to perform the chores of a maintainer - people who become maintainers in this community are generally learning based on peer observation and mentoring from other maintainers, alongside whatever [conventions documentation](https://docs.spacestation14.com/en/general-development/codebase-info/conventions.html) they have been using thus far. The goal of this guide is to explain maintainer concepts that may not be accessible to those less-involved in the community.

## Terms to Know

The game's entire combined code and resources, such as its sprites or audio, come together to form what is known as a **repository** ("repo") or **codebase**. When someone talks about the "Wizard's Den codebase" or "Wizard's Den repository", they are talking about all of the content that makes up the Wizard's Den server.

There is a distinction between the codebase and the **server**. The codebase refers to all the game content, code, and assets itself, while the server is a hosted instance of this codebase that players can connect to - the game that people are actually playing. A single codebase can have multiple servers.

**Wizard's Den**, or **Wizden**, is the "official" codebase for SS14 - all other SS14 codebases descend from them in some form.

SS14 repositories have a lineage to them. When you make a new repository for your server that diverges from another, this is called **forking**. The new repository is known as a **fork** or **downstream**. The repository that this fork is diverging from is known as an **upstream** or a **base**. 

(These terms apply throughout the entire "chain" of inheritance - if server A forks from Wizden, and server B forks from server A, then server B is still downstream of Wizden. But server A is "*the* upstream".)

When a codebase integrates changes from another codebase that they do not inherit via downstreaming, this is a **port**. For example, if server B adds a new species, then server A can port that species.

**Contributor** or **developer** are used interchangeably to refer to people who make changes to the game. Anyone can become a contributor to the SS14 project. Maintainers are pretty much always contributors as well.

New changes to the game do not actually show up on the game server until a **publish** operation is ran. For example, you may merge several changes throughout the day, but the publish only runs once per day, which triggers a server restart.

### What is Git?

Git is version control software. It maintains a timeline of incremental changes - a contributor can move backwards or forwards along this timeline, **revert** individual changes, or integrate new changes from external sources to add to this timeline. Repositories are stored on **GitHub**, which keeps an online record of this entire timeline.

An individual change to a repository is a **commit**. A contributor makes a copy of the game's repository to do development work - a fork. They will **clone** this fork's files to their computer for work. As the game is continuously improving, the game's repository will accumulate changes over time, and the contributor may need to **pull** these new changes and **merge** them into their fork to stay up-to-date.

The contributor may want to add a new feature, so they make a **branch** in their own repository. They may edit files to make their changes and save them. Then, they have to **stage** their changes so they will be included in the next commit, and then they commit these changes.

Once the contributor has new commits in their branch, they may **push** these changes back to their own fork on GitHub. Once they're ready, the contributor can make a **pull request** pointing from their development branch to the game repository's "master" branch, which contains all of their changes.

(A "pull request" is effectively *requesting* that the repository *pull* your changes, integrating them into its own timeline.)

Imagine the game's repository as a large box of contents. Each contributor gets their own copy of the box, and they may add remove contents at will. Then, the contributor makes a pull request, telling the game repository to make the same changes to its own contents, such as adding a new feature. After reviews, a maintainer merges this pull request, syncing the contributor's changes to the game's repository. This is how new features are made!

Having a comprehensive timeline of the game's changes creates accountability and makes it easier for maintainers to revert changes as they please. You know exactly who made every feature, and when, and why.

## Responsibilities of a Maintainer

Maintainers are tasked with keeping their server stable and up-to-date, as well as controlling the flow of new feature additions, tweaks, and fixes to the game. Some tasks maintainers frequently oversee include:

- **Performing pull request reviews:** You may look over the code and assets of new feature additions and ensure the code quality is up to server standards - such as structure, readability, and performance. Make sure the feature works as intended, doesn't introduce game-breaking bugs, and is in-line with what your server's tone, direction, and design wants. You also perform the final merge, which is what actually integrates these changes into the game.
- **Mentoring and advising contributors:** Maintainers are generally selected from experienced contributors and usually have a good idea of the game's organization and development process. New contributors will often look to you for advice - make sure everything is going in the right place. You should have a good general idea of where to look when someone asks where something is. When someone's code breaks, you can help them fix it.
- **Regular codebase maintenance:** If your server is a downstream, you'll probably want to be regularly pulling new changes and fixes from your upstream. When old code becomes deprecated, you might need to replace it. Maintainers may handle bugfixing work. You may be given the authorization to manually publish new changes to the server.
- **Developing guides, standards, and documentation:** You are often responsible for communicating conventions to contributors to make it easier to review pull requests. You might develop tools to make contribution easier for future developers, and then have to write instructions on how to use those tools. As you often have to read the code that others create, it's in your best interest to make sure they're easy to understand. This documentation saves time for you and contributors!

At the very minimum, a maintainer should know how to set up the Space Station 14 developer environment - this is the first step for any contribution, and for many the biggest hurdle to getting started contributing to the game. This also teaches you basic skills in navigating GitHub and using Git to clone a repository.

An absolutely essential read for maintainers is [The Robust Book](https://docs.spacestation14.com/index.html), Wizard's Den's official documentation for development. This book has WizDen's maintainer conventions, as well as development guides and tutorials.

As a maintainer, you will work pretty intensively with Git, so it's in your best interest to learn how to perform common tasks with Git such as pushing/pulling/making commits, branch management, remote management, merges, merge conflict resolution, cherry-picks, and reversions.

**You do not know everything about development in order to be a maintainer!** Servers have teams of maintainers that often specialize in different areas. Some maintainers do not know C# at all, and only review YAML / asset pull requests. Some people know how to develop maps, some people know how to design UI, some people perform more technical chores like tooling and workflows. All of this is perfectly fine!

## Guides in this Series

- [The Structure of Space Station 14](ss14-structure) (WIP)

--- 

TODO: write guides for various maintainer-relevant topics:

- [x] Game structure
- [ ] Git guide
- [ ] Common conventions (e.g. namespacing)
- [ ] PR reviews
- [ ] Integration tests
- [ ] Upstream merges
- [ ] Ports / cherry-picking
- [ ] Reversions
- [ ] Workflows / publishing

## Useful Reading

- [The Robust Book](https://docs.spacestation14.com/index.html) (WizDen documentation)
- [Refactoring Guru](https://refactoring.guru/)

### Specific Maintainer / Development Resources

- [Quick Guide to Space Station 14 Codebase Setup](https://gist.github.com/portfiend/6529ca0b1a5f98747e99ec2beea6a741) by portfiend
- [Cherry-Picking Cheat Sheet](https://gist.github.com/portfiend/be07e98d0103f3606e83f718f69d250d) by portfiend
- [The Slartiguide](https://hackmd.io/@Slart/S1hsoGFm1l) by Slartibartfast (C# and YAML development with examples)
- [Converting Oldbody to Nubody](https://docs.spacestation14.com/en/ss14-by-example/converting-oldbody-to-nubody.html) by mqole
- [Nubody vs old BodySystem](https://hackmd.io/@pontaos/HyITzBH0Zx) by pontaos
- [Guide to Prediction](https://docs.spacestation14.com/en/ss14-by-example/prediction-guide.html) by Slartibartfast
- [A Quick Guide to Feedback](https://docs.google.com/document/d/1-FfZou99gg5i4zdTKy01r-8VkyFn-ILwunuEYeQ94Uc/edit)
- [Forker's Cheat Sheet](https://gist.github.com/moonheart08/2d3945faf3cf691437e1e1fa0e922420) by moonheart08
- [SS14 Editor](https://www.ss14editor.com/) (web-based mapping editor)
