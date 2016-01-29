# GSSundheit

## What's that?

Currently, a mostly-empty Git repo.

When I have time, I will write a simple [GSSAPI] provider that lets users on
trusted servers acquire session tickets and authenticate against remote services
transparently.

[GSSAPI]: https://en.wikipedia.org/wiki/GSS-API


## How does it work?

A `gssundheit` deamon runs on the trusted server (as an unprivileged user), and
  listens to a well-known UNIX socket (say, `/var/run/gssundheit.sock`).

When a user connects to the socket, the deamon authenticates them using
  `SO_PEERCRED` (basically, asking the kernel for which UID is at the other end
  of the socket) and sends a signed authentication ticket with auxiliary
  metadata used to support GSSAPI features (such as channel bindings).


## Goals

1. The two primary goals are simplicity and security:
   GSSundheit should be simple to use and simple to audit.

2. The main usecase for GSSundheit is through a SASL authentication service,
   like [auth](https://github.com/whawty/auth), but GSSAPI is a generic API
   and any other kind of service may leverage it.

3. Some optional features of GSSAPI are considered especially desireable:
   - [ ] channel binding, see [RFC 5056].

[RFC 5056]: https://tools.ietf.org/html/rfc5056
