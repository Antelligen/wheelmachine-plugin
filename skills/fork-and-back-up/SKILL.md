---
name: wheelmachine-fork-and-back-up
description: Fork a Wheelmachine machine, or back up its files and make a new machine from them later. Use it to try a risky change on a copy and keep the original as it was, to run the same work several ways, or to keep a machine's files before changing them.
---

# Fork and back up a machine

## Fork

`fork_machine` makes a new machine of its own from one as it is now. It has the original's size and, where it can, carries
on from where the original is. Try the risky change on the fork. Its name is the original's with `-fork` after it, and its
labels the original's, unless you give others.

In an organisation, a member's fork waits for an OK: the answer is a request (`rq_...`), not a machine, and its `note` says
whose OK it waits for. Tell the person. `list_machines` shows the fork once it is made.

Before you fork again after a call that timed out, look with `list_machines`: it may have made one already.

## Back up

`backup_machine` keeps a machine's files as they are now, not what runs in it, with a `note` to know it by.
`list_backups` names a machine's backups, or with no `machine`, those of every machine the key reaches.

`fork_machine` with `backup` - a backup's id, or `latest` for the newest - makes a new machine from them, starting afresh
from its files, at the original's size or the one `cpus` asks.

`delete_machine` deletes a machine's backups with it.
