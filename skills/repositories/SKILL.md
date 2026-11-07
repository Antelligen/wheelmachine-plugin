---
name: wheelmachine-repositories
description: Clone, fetch and push GitHub and GitLab repositories in a Wheelmachine machine, with no token in the machine. Use it when work in a machine needs a repository, when git refuses a clone or a push there, before asking anyone for a Git token, or to get changes to a protected branch.
---

# Work with a repository in a machine

No token ever goes into a machine. Never ask for a Git token, and never add one to a machine, a command or a secret.

Try plain https git first, with the repository's https address:

    git clone https://github.com/acme/api.git
    git push

A fetch uses the team's access, and a push the linked account of the person who holds the machine. A `git@github.com:` address
needs an SSH key of the person's own, so use the https one. A machine has no name for commits until you set one:
`git config user.name` and `git config user.email`.

## If git refuses: the Code page

What a machine reaches is set on the dashboard's **Code** page, by a person. Tell them what is missing:

- **Connect GitHub** or **Connect GitLab**: an organisation's owners and admins, or the person in their own account.
- Give the team the repository, to **Read** or to **Read and push**: a team's full managers, the owners and admins, or the
  person in their own account.
- **Your accounts**: each person links their own GitHub and GitLab once. A machine can clone and fetch without a link; a
  push without one is refused.

A machine reaches its team's repositories while the person who holds it is in the team, so make it in that team (`project`
on `create_machine`).

## Work on a branch

No machine pushes to a protected branch. `main`, `master` and `release/**` are protected until an account's owners and
admins choose otherwise, so work on a branch and push that:

    git switch -c fix-login-test
    git push -u origin fix-login-test

Changes reach a protected branch through a pull request on GitHub, or a merge request on GitLab. A person opens it: there
is no token in the machine to open one with, and a machine does not carry `gh` or `glab`. The first push of a branch prints
a link for it, from GitHub or GitLab. Give that link to the person.

## What a refusal means

- `could not read Username`: the repository is not public and its team was not given it, or there is no such repository. A
  public repository clones, but a push asks the same. Point the person to the Code page.
- `this machine may read that repository, not push to it: its team was given it to read`, with a 403: the team has it to
  read. The person gives it **Read and push**.
- `a push needs your own GitHub account linked: link it on Wheelmachine's Code page, under Your accounts`, or GitLab: the
  person links theirs under **Your accounts**.
- `main is protected: changes reach it through a pull request`, or a merge request: push a branch instead.
- `this team's machines may push only to feature/** or fix/*`: a team's push rule. Name your branch to fit it, or ask for the
  team's **Push rules** to change.
- `not pushed: another ref in this push was refused`: a push goes whole or not at all. Fix the other ref it names.
- `this machine's internet does not reach github.com`, with a 403: see below.

## Its internet must reach the host

An open machine always reaches it. A machine with a list does only when the list names the host (`github.com`,
`gitlab.com` or a company's own GitLab). A closed machine never does. See the wheelmachine-secrets-and-internet skill, and
ask before you change a machine's internet.

## A company's own GitLab

Run this once in the machine, with the company's host for `gitlab.example.com`:

    git config --global url."http://169.254.169.251:7703/gitlab.example.com/".insteadOf https://gitlab.example.com/

On a GitLab connected by a group's token, nobody's account is linked: pushes there go with the group's token.

More: https://docs.wheelmachine.ai/code.html
