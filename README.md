# Wheelmachine's plugin

Wheelmachine's MCP server, `https://api.wheelmachine.ai/mcp`, and skills for its tools: make, fork and run computers in the
cloud, open their apps, see and work their desktops and work with your repositories, from your agent.

It needs an API key: make one on the dashboard's **Agents** page or with `wm keys create`. The key is sent to
`https://api.wheelmachine.ai` alone.

## Install

In a terminal, start `claude`, then type these, one at a time. The second asks for your key.

    /plugin marketplace add Antelligen/wheelmachine-plugin
    /plugin install wheelmachine@wheelmachine
    /reload-plugins

The VS Code panel does not take `/plugin`: use a terminal.

Codex reads your key from `WHEELMACHINE_API_KEY`: set it before you start Codex.

    codex plugin marketplace add Antelligen/wheelmachine-plugin
    codex plugin add wheelmachine@wheelmachine

Gemini CLI asks for your key.

    gemini extensions install https://github.com/Antelligen/wheelmachine-plugin

Cursor reads your key from `WHEELMACHINE_API_KEY`: set it, then start Cursor from that terminal. Add the server with the
one-click link at https://docs.wheelmachine.ai/mcp.html#plugin-cursor, or put this in `~/.cursor/mcp.json`:

    {
      "mcpServers": {
        "wheelmachine": {
          "url": "https://api.wheelmachine.ai/mcp",
          "headers": { "Authorization": "Bearer ${env:WHEELMACHINE_API_KEY}" }
        }
      }
    }

The skills alone, for any agent that takes them:

    npx skills add Antelligen/wheelmachine-plugin

Any other agent, or setting it up by hand: https://docs.wheelmachine.ai/mcp.html

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
| `clean-up` | Pause, stop or delete what is not in use |
| `when-a-tool-fails` | Read a failed call and act on it |

## What it runs and sends

The plugin is settings and text: it runs nothing on your computer. When your agent uses one of its tools, the tool's arguments
and your key go to `https://api.wheelmachine.ai`, and what comes back goes to your agent and its model. Machines are charged by
the second while they run, from your Wheelmachine account.

## Licence and privacy

Apache License 2.0: see `LICENSE`. Privacy policy: https://wheelmachine.ai/privacy/
