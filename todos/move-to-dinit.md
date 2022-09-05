# TODO: Change Init System to dinit

Currently eweOS uses S6 for /sbin/init, and it will be replaced with dinit.

Some services must be rewritten before S6 is formally replaced:

- `tty1` and `ttyS0` must be launched.
- `syslogd` must be launched.
- `utmps` services must be launched.

For every newly added package, s6 service file is not needed anymore while dinit service file is required.