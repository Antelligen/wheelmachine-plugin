---
name: wheelmachine-make-machines
description: Make Wheelmachine machines - computers in the cloud, made usually in about a second and paid by the second - and find them again. Use it when work needs a machine of its own, to build or test code away from this computer or run something long, or to choose a machine's size, team, region or GPU.
---

# Make a machine

The `wheelmachine` MCP tools reach the account of the API key they were set up with. `whoami` names the account and the
key, the key's scopes and projects, and whether the account can spend.

1. When one may already be there, look first: `list_machines`, by `labels`, `state` or `project`.
2. `create_machine` with a `name` and `labels` you will find it by again, such as `{"task": "fix-login-test"}`. Every
   argument may be left out. It answers once the machine runs, usually in about a second.
3. If it answers with `state` `starting`, follow it with `get_machine` until it is `running`. One that never comes up
   says `failed`, and `failure` says why.

A machine is named by its id (`m_...`) or its name in every tool.

## What you can ask for

- `cpus`: 2, 4 or 8, with 2 GB of memory each. Left out, 2.
- `project`: its team, by id (`prj_...`) or name; the account's first when left out. A machine reaches the repositories
  its team was given, so make it in that team.
- `region`: an id from `list_regions`, to run near. The machine's `location` says where it actually runs.
- `gpu`: an id from `list_gpus`, with a key that holds the `cloud:gpus` scope. `for_sale` is false while GPU machines are
  not open to every account. A GPU machine can take minutes: it is answered as `starting` within about a second.
- `sleep_when_idle` and `idle_after_s`: a machine pauses by itself once it is idle - nothing has reached it for
  `idle_after_s`, five minutes unless you say otherwise, and its programs have been quiet as long - and wakes for the next
  command. Give `sleep_when_idle` false only for work that must keep running unwatched: it runs, charged, until it is
  paused or stopped.
- `desktop`: true turns its desktop on behind the answer, for a first picture of it to find ready. See the
  wheelmachine-desktop skill.
- `secrets` and `network`: what its commands get, and what it may reach on the internet. See the
  wheelmachine-secrets-and-internet skill.

Running time is charged by the second while a machine runs. The wheelmachine-clean-up skill says how to stop that.
