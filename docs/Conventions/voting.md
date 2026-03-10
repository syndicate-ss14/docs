---
tags:
  - conventions
---

# Voting

Macrocosm utilizes consensus decision-making, where any contributor may create a pull request, and each Microcosm must vote on that pull request before it is merged.

All pull requests fall under one of three categories:

* Category A: Universally Desired
* Category B: Universally Agreed-on
* Category C: Extreme Maintenance Burden

The categorization of each Pull Request is done by the triage team.

### Category A: Universally Desired

This is a pull request where all Microcosms agree that they want this content and are happy to have it in their codebase. 

Category A pull requests require unanimous agreement, **with no abstains or blocking votes**. Blocking votes are expected to have a written explanation behind the block, ideally with suggested course of action on what would be needed to change their vote.

Even if a pull request is under Category A, the policy regarding customization still applies: there should always be a simple way to disable the content.

### Category B: Universally Agreed-on

This is a pull request where all Microcosms are fine if not completely enthusiastic with the content. This is also where pull requests regarding altering a Wizard's Den upstream merge will land.

Category B pull requests require agreement **with no blocking votes**; abstentions are allowed. Blocking votes are expected to have a written explanation behind the block, ideally with suggested course of action on what would be needed to change their vote.

### Category C: Extreme Maintenance Burden

This is a pull request that represents the collaborative effort between multiple Microcosms on a project that is better handled on the shared platform rather than in their respective downstreams. Potential examples of a Category C pull request would be a mechanically complex major antagonist, a complete UI rework, or other large-scale gameplay overhaul.

Category C pull requests require agreement **with no blocking votes**; abstentions are allowed. Category C pull requests will receive the highest scrutiny out of anything as they represent the largest risk to the overall stability of the project.