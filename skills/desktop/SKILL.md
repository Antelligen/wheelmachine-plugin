---
name: wheelmachine-desktop
description: See and work a Wheelmachine machine's Linux desktop - take a picture of it, click, drag, scroll and type. Use it for what only the screen shows, such as a program with no command line or a page to check by eye, or when a person asks what a machine's screen shows.
---

# See and work a machine's desktop

Machines have Linux desktops, and you can see and work them. For work a program can do, `run_command` is faster and surer
than clicking: use the screen for what only the screen shows.

- `take_screenshot` answers a picture of the desktop, with its `width` and `height` in pixels. `scale` draws it down: 1, or
  one over a whole number up to 8. The default, 0.5, is 1440 x 900 of the desktop's 2880 x 1800. A model that draws a picture
  down further reads places wrongly, so ask for a `scale` that fits what your model takes. A `region` is a part of the screen.
  `format` is `png`, which is exact and what to read small text from, or `jpeg`, smaller for a screen of photographs.
- `use_screen` does `actions` in order - `click`, `move`, `drag`, `scroll`, `keys`, `type`, `wait` - and with
  `then_screenshot` answers a picture after `settle_ms`. `x` and `y` are pixels of a picture of the whole screen at the same
  `scale`: read a place off the picture, click it, and look again. A part you asked for begins at its own `x` and `y`: add
  them.

## Before you start

The desktop is off until something asks for it, and its first start can take up to a minute: give `desktop` true to
`create_machine` when you know you will want it. A paused machine is woken for a picture or a click, and runs and is charged
as for a command, so pause it again when you are done.

It needs a key that may run commands (`cloud:machines:exec`). In an organisation, only the person who holds a machine works it.
Someone who watches it gets pictures of the screen they watch, with nothing woken or turned on, and never its pointer or keys.

## What can go wrong

- One `use_screen` holds at most 64 actions, with 4096 characters typed and 25 seconds of waits, and has 30 seconds with the
  desktop once it is up. Split longer work into several calls.
- A key has at most 4 calls on screens going at once. Over that, or when many pictures are being taken, the answer is 429 with
  `retry_after_s`, and nothing was done: wait that long and ask again.
- Letters of every language and emoji can be typed. Characters that aren't on an English keyboard, such as accents, Russian,
  Chinese or emoji, can come out wrong. Take a picture after typing them to check; a password box can't be checked this way.
- A failed `use_screen` says how many of its actions were done: look at the screen before you try again.

## What your model sees

A picture shows whatever is on the screen and goes on to your model's provider. Do not leave a password or a private page
showing unless the person says so. We never keep or log what you type, but your model wrote it, so its provider has seen it.
