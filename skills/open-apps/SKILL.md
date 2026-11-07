---
name: wheelmachine-open-apps
description: Turn on and open the apps a Wheelmachine machine carries - a desktop, a code editor, an agent's own page, agents in its terminal. Use it to give a person a desktop or a code editor in their browser, or to show them something on the machine's screen.
---

# Open a machine's apps

1. `list_apps` names the apps a machine carries and whether each is on. A new machine runs them by default, but for the
   desktop and Gemini CLI, which stay off until turned on. The code editor is always on.
2. `turn_app_on` turns one on, which may take up to a minute. A web app answers a `link` that lets one browser in once,
   within five minutes. Give the link to the person, and do not keep it. An app with a token of its own answers it this
   once, in `token`.
3. `open_app` makes a fresh link to a web app that is on. Each call makes a new link. `access_s` is how long that browser
   may reach the app.

- `show_app` opens an app on the machine's own desktop, for a person who watches the machine's screen in the dashboard. It
  may take up to two minutes. To see and work that desktop yourself, see the wheelmachine-desktop skill.
- `turn_app_off` frees the machine's memory. An agent's session ends with it. The code editor cannot be turned off.
- An agent with `keys_changed` true began its session before the machine's AI keys changed: turn it off and on again to
  start it with them, in a new session.
