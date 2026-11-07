---
name: wheelmachine-run-commands
description: Run commands in a Wheelmachine machine, and read and write its files. Use it to build, test or run anything in a machine, to start work that takes longer than ten minutes, or when a command's output is long or was cut.
---

# Run work in a machine

`run_command` runs a program and its arguments (`command`, such as `["npm", "test"]`) or a line of shell (`shell`, such as
`"cd app && npm test 2>&1 | tail -50"`) - one of the two. It answers `exit_code`, `stdout` and `stderr`. A non-zero
`exit_code` is the command's own answer, not a failed tool. A paused machine is woken for it.

- `cwd` is where it starts, an absolute path; left out, the work folder.
- `env` gives it environment variables.
- `root` true runs it as root, inside the machine only.

## Work longer than ten minutes

A command may run 10 minutes. Start longer work in the background - `nohup make build > build.log 2>&1 &`, as commands
start inside `work/` - and read its log, `work/build.log`, with `read_file` as it goes. Work left running in the
background keeps the machine from pausing by itself.

## Long output

`max_output_bytes` is the most of each of `stdout` and `stderr` given back, 64 KiB by default. Long output is cut, and
`truncated` says so; past 8 MiB the rest is gone, so what you get may not reach the real end. Write big output to a file
and read the part you need. A command with huge output may be reported as failed though it ran: look at what it did
before you run it again.

## Files

File paths begin `home/` (the machine's home) or `work/` (where commands start).

- `write_file` puts text in a file, making the folders on the way. A file already there is replaced.
- `read_file` reads one back, text as it is and other bytes as base64. At most `max_bytes` come back, and `truncated`
  says when the file holds more.

A message to the tools is at most 8 MiB, so a file `write_file` writes is a little less. A person copies larger ones with
`wm cp`.
