---
name: wheelmachine-when-a-tool-fails
description: Read and act on a failed Wheelmachine tool call - forbidden, not_found, rate_limited, payment_required, invalid_request, a timeout. Use it when a wheelmachine tool answers an error, or a call was cut off and may still have done its work.
---

# When a Wheelmachine tool fails

A failed tool answers a result marked as an error, holding the API's `code` and `detail`, and `retry_after_s` when the API
asked for a wait. Read them and act. A non-zero `exit_code` from `run_command` is not one of these: it is the command's own
answer.

- `forbidden`: the key does not allow it. Say which scope is missing; do not look for a way around it. `whoami` names the
  key's scopes.
- `not_found`: no such machine, file or app here. Check the name with `list_machines` or `list_apps`.
- `rate_limited`: too many calls at once. Wait `retry_after_s` seconds, then try again.
- `timeout`, or a call cut off: it may still have done its work, a command may still be running, and tool calls carry no
  `Idempotency-Key`. Before calling `create_machine` or `fork_machine` again, look with `list_machines`, or you can make a
  second machine.
- `payment_required`: the account cannot spend now - its credit is used up, or its monthly limit is reached. Tell the
  person.
- `invalid_request`: the arguments are not right. `detail` says what to change.
