---
name: wheelmachine-secrets-and-internet
description: Say which of the account's secrets a Wheelmachine machine gets, and what it may reach on the internet. Use it when a command there needs a secret, when a machine cannot reach a site, or to close a machine off or keep it to a list.
---

# A machine's secrets and internet

## Secrets

No tool takes a secret's value. A person sets values, with `wm secrets set` or the API.

- `list_secrets` names the account's secrets, each with the machines given it, and never a value.
- `give_secrets` says which of them a machine gets, by name. The names given take the place of the ones it had; an empty
  list takes them all away. Each must be set already. It needs a key with the `cloud:secrets:write` scope: if it answers
  `forbidden`, ask the person to give them.
- `secrets` on `create_machine` gives them from the start, with the same scope.

Every command in the machine gets each one as an environment variable of that name, so a command there can read it. A
variable given to `run_command` in `env` wins over a secret of the same name. An AI key, such as `ANTHROPIC_API_KEY`, is on
every machine unless it was set for the machines given it: a machine's `ai_keys` names the ones that reach it.

Do not ask for a Git token: see the wheelmachine-repositories skill.

## Internet

`set_network` sets what a machine may reach, at once and without a restart. `network` on `create_machine` sets it from the
start.

- `open`: the whole internet.
- `closed`: no internet in or out and no name lookups: a public port answers only as a private one. A push to your team's
  repositories still goes, and can start that repository's own CI, which runs outside the machine with its own internet.
- `allowed`: only what `allow` lists - domain names, exact or with a leading `*.` for every name under it, for HTTP and
  HTTPS, and IPv4 or IPv6 ranges for other ports.

Whatever it is, your team's repositories and folders still work where given.

A person may have closed a machine on purpose: ask before you open it or add to its list.
