# TODO: Change Init System to dinit

**Total progress: 70%**

Currently eweOS uses S6 for /sbin/init, and it will be replaced with dinit.

Some services must be rewritten before S6 is formally replaced:

- ~~`tty1` and `ttyS0` must be launched.~~ (Finished)
- ~~`syslogd` must be launched.~~ (Finished)
- `utmps` services must be launched.
  - `s6-ipcserver` is required, try `ucspi-unix` for alternative.

`dinit` must be compiled to support `utmps`.

For every newly added package, s6 service file is not needed anymore while dinit service file is required.