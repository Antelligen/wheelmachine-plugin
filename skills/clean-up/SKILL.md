---
name: wheelmachine-clean-up
description: Pause, stop, start or delete Wheelmachine machines, so that nothing is charged for running while it is not in use. Use it when work in a machine is done or waits, or when a person asks to stop paying for a machine.
---

# Clean up machines

Running time is charged by the second while a machine runs.

- `pause_machine` keeps its memory, and nothing runs. `start_machine` brings it back where it was.
- `stop_machine` keeps its files, not its memory or what was running. `start_machine` runs it again.
- `delete_machine` deletes it, all its files and its backups, for good. It cannot be undone: use it only when the work is
  done and nothing of it is needed. Push what matters first (the wheelmachine-repositories skill).

A machine also pauses by itself once it is idle, unless it was made with `sleep_when_idle` false, and wakes for the next
command.

`list_machines` with `state` `running` shows what is running now.
