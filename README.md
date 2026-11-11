# Wheelmachine's plugin

Wheelmachine's MCP server, `https://api.wheelmachine.ai/mcp`, and skills for its tools: make, fork and run computers in the
cloud, open their apps, see and work their desktops and work with your repositories, from your agent.

You sign in through your browser: there is no key to paste. Where no browser can open, an API key works too: see
[With a key instead](#with-a-key-instead).

## Install

In a terminal, start `claude`, then type these, one at a time.

    /plugin marketplace add Antelligen/wheelmachine-plugin
    /plugin install wheelmachine@wheelmachine
    /reload-plugins

Then type `/mcp`, choose the server and **Authenticate**: your browser opens, and you choose **Allow**. The VS Code panel does
not take `/plugin`: use a terminal.

Codex: the last line opens your browser to sign in.

    codex plugin marketplace add Antelligen/wheelmachine-plugin
    codex plugin add wheelmachine@wheelmachine
    codex mcp login wheelmachine

Gemini CLI: restart it after this, then type `/mcp auth wheelmachine` to sign in.

    gemini extensions install https://github.com/Antelligen/wheelmachine-plugin

Cursor: add the server with the one-click link at https://docs.wheelmachine.ai/mcp.html#plugin-cursor, or put this in
`~/.cursor/mcp.json`. Cursor then shows **Needs authentication** beside the server: choose **Authenticate**.

    {
      "mcpServers": {
        "wheelmachine": {
          "url": "https://api.wheelmachine.ai/mcp"
        }
      }
    }

The skills alone, for any agent that takes them:

    npx skills add Antelligen/wheelmachine-plugin

Any other agent, or setting it up by hand: https://docs.wheelmachine.ai/mcp.html

## With a key instead

For CI, or anywhere no browser can open. Make a key on the dashboard's **Agents** page or with `wm keys create`, keep it as
`WHEELMACHINE_API_KEY` where the agent runs, and add the server yourself, with the key's header: each agent's lines are at
https://docs.wheelmachine.ai/mcp.html#give-it-a-key.

## Ask your agent

    Make a Wheelmachine machine, run uname -a in it, then delete it.
    Make a machine, clone my repository in it, run its tests and tell me what failed.
    Fork my machine, try the upgrade on the fork, and keep the original as it was.

## Skills

| Skill | For |
|---|---|
| `make-machines` | Make a machine, and choose its size, team, region or GPU |
| `run-commands` | Run commands, and read and write files |
| `fork-and-back-up` | Try a change on a copy, or keep a machine's files |
| `open-apps` | Give a person a desktop or a code editor in their browser |
| `desktop` | See a machine's desktop as a picture, and work it |
| `secrets-and-internet` | What a machine's commands get, and what it may reach |
| `repositories` | Clone and push with no token in the machine |
| `pull-requests` | Open a pull request or merge request from a machine |
| `clean-up` | Pause, stop or delete what is not in use |
| `when-a-tool-fails` | Read a failed call and act on it |

## What it runs and sends

The plugin is settings and text: it runs nothing on your computer. When your agent uses one of its tools, the tool's arguments
and your sign-in, or your key, go to `https://api.wheelmachine.ai`, and what comes back goes to your agent and its model.
Machines are charged by the second while they run, from your Wheelmachine account.

## Licence and privacy

Apache License 2.0: see `LICENSE`. Privacy policy: https://wheelmachine.ai/privacy/
