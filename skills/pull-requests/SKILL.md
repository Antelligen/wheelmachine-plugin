---
name: wheelmachine-pull-requests
description: Open a pull request or merge request from a Wheelmachine machine, with no token in the machine, and see which repositories it reaches. Use it as the last step of work on a branch, when changes should reach a protected branch, or to learn whether a push will go.
---

# Open a pull request from a machine

A machine holds no token and does not carry `gh` or `glab`: do not install them or ask for a token. `open_pull_request` opens it.
It does not merge, approve or close anything: people do.

## What a machine reaches

`list_repositories` says what the machine reaches now: each repository's `access`, whether the holder's account is `linked`, whether
a push will go (`can_push`), and the `protected_branches`. Ask it when you are not sure a push will go. For what to do if one is
missing, see the wheelmachine-repositories skill.

## Open it

Work on a branch and push it. Then give `open_pull_request`:

- `machine`, and `repository` as `list_repositories` gives it. `host` only where the same path is on two hosts.
- `head`, the branch with the changes: a branch of the same repository that the team's machines may push to, so not a fork and not
  a protected branch.
- `base`, the branch to merge them into. It may be protected.
- `title`, one line, and `body`, what it changes and how you tested it. `draft` true opens it as a draft.

Only the person who holds the machine may ask, with a key that may run commands.

## On GitHub

Push the branch first. It opens at once under the holder's own linked account, and answers its `number` and `url`. Give the person
the `url`.

## On GitLab

It answers `opened` false and `run`, a line of git, with nothing open yet. Run that line in your clone with `run_command`, as your
last push: GitLab opens the merge request, or updates the one open from that branch, and git prints its address. Give the person
that address.

- That push has to send new commits. If git says everything is up to date, make a commit first.
- A `body` with a line beginning with `/` is refused, as GitLab would run that line as a command: write `\/` to show one.

## What a refusal means

- `only the person who holds this machine opens a pull request from it`: ask that person.
- `this machine does not reach acme/api: ask which repositories it does`: look with `list_repositories`, then point the person to
  the dashboard's **Code** page.
- `this machine may read acme/api, not push to it: its team was given it to read`: the person gives the team **Read and push**.
- `a pull request needs your own GitHub account linked: link it on Wheelmachine's Code page, under Your accounts`, or a merge request
  and GitLab: the person links theirs under **Your accounts**.
- `head is a branch of this repository: a pull request from a fork is not opened here`: push a branch to the repository itself.
- `GitHub does not let Wheelmachine open pull requests on acme yet`: an owner of that account on GitHub must accept a new permission.
  The answer says which, and where: give the person those words.
- `rate_limited`: too many opened just now. Wait `retry_after_s`.

If it cannot be opened, the first push of a branch prints a link for one, from GitHub or GitLab. Give that link to the person.

More: https://docs.wheelmachine.ai/code.html#pull-requests
