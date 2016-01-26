# Generic Organisation-wide Authentication Security Service

## What's that?

Currently, a mostly-empty Git repo.

When I have time, I will write a simple [GSSAPI] provider that lets users on
trusted servers acquire session tickets and authenticate against remote services
transparently.

[GSSAPI]: https://en.wikipedia.org/wiki/GSS-API

## How does it work?

A `goatssed` deamon runs on the trusted server (as an unprivileged user), and
  listens to a well-known UNIX socket (say, `/var/run/goatsse.sock`).

When a user connects to the socket, the deamon authenticates them using
  `SO_PEERCRED` (basically, asking the kernel for which UID is at the other end
  of the socket) and sends a signed ticket containing the uid (or username?),
  the origin server and the current time.
