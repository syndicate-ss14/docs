---
authors: [mqole]
tags:
  - guides
  - codebase

slug: /Guides/CodebaseManagement/upstream-merge
---

# Upstream Merges

:::warning[Work in Progress!]
This page is a work in progress. Expect to see it updated sometime in the future with more information.
:::


{/*a future guide should transplant some of this into a conventions page, but for now I'm keeping it all here.*/}
A single Upstream Merge pull request may contain dozens of features, each represented by its own commit within the pull request. For this reason and in order to maintain organisation of the codebase, upstream merges **must be merged via a merge commit** as opposed to squash merging.

Any "fix commits," or otherwise any commits that do not belong to Wizard's Den, must be rebased using `git rebase -i` to keep the number of commits to a minimum.

Upstream Merge pull requests require the following documentation:
- Any merge conflicts that were resolved between Macrocosm and Wizard's Den, and how they were resolved.
- Any changes made to Macrocosm content that could be classified as a 'breaking change' by the standards of other pull request categories (for example, replacing one component with another after an upstream refactor).
- Any changes that were made to resolve test fails if such a change was not already documented by the above criteria.