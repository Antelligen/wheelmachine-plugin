# Changelog

Wheelmachine's plugin and Gemini CLI extension: its MCP server, set up in one step, and skills for its tools. Each
release is tagged `plugin-v<version>`.

## 0.3.0

- The skill for a machine's desktop says more of what the docs say: how far a picture can be drawn down before a model misreads
  places, which `format` to ask for, that a paused machine is woken and charged for a picture or a click, who may work a screen,
  and how much one call and one key may do.
- The README gives three things to ask your agent, and says what the plugin runs and sends. The `.codex-plugin` manifest
  carries what a directory of plugins reads: a short description of at most 30 characters, a category, a support address,
  the three things to ask and a square icon; its marketplace lists the plugin under the same category. `assets/logo.png`, the
  mark on a white plate, is for a directory that asks for a logo on one.
- The README names the dashboard's Agents page, where a key for the plugin is made.

## 0.2.0

- The plugin has a repository of its own, `Antelligen/wheelmachine-plugin`. Add its marketplace at this address: the plugin's
  files leave `Antelligen/wheelmachine`.
- The plugin comes for two more agents, the ones that look for `.codex-plugin` and `.cursor-plugin`: the same MCP server and
  the same skills, with the API key read from `WHEELMACHINE_API_KEY`, as those two cannot ask for it.
- One skill became nine, one task each: make machines, run commands, fork and back up, open apps, work a desktop, secrets and
  internet, clean up, a failed call, and working with a repository.
- The skill for a repository teaches an agent never to ask for a Git token: plain https git works with no token in the
  machine, a branch is pushed and a person opens the pull request or merge request, and each of git's refusals says what to
  do.
- The Gemini CLI extension waits the 10 minutes a command may run.
- The plugin names its privacy policy, and carries our mark as an icon.

## 0.1.0

The first public release.

- The plugin's marketplace, `wheelmachine`, with one plugin: the MCP server at `https://api.wheelmachine.ai/mcp`, with
  the API key asked for once and kept as a secret, and a skill that teaches an agent to make, fork and run machines and
  open their apps.
- The same as a Gemini CLI extension, with its context file.
