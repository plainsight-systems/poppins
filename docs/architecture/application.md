# Configuration and monitoring application

These contracts define the browser application's boundary with the server.
They do not select a frontend framework, event transport, or execution backend.

## One installed application

The Poppins distribution bundles the server and browser assets. The server
serves the interface at its local management address and also supports headless
operation. Opening or closing a browser has no effect on the server lifecycle
or on inference requests submitted by other clients.

The interface presents Overview, Models, Requests, and Settings as described in
the [product requirements](../product.md).

## Ownership

| Owner | Contract |
| --- | --- |
| `app/` | Displays server state, explains settings, and submits management commands |
| Serving | Serves bundled assets, validates and authorizes API requests, and transports state and events |
| Hosts | Own persistent configuration and coordinate its application with runtime owners |
| Runtime owners | Validate and apply domain operations, enforce budgets, and publish authoritative state |
| Platform | Supplies hardware discovery and application-data locations |

The browser never owns the effective configuration, resource accounting, or
request lifecycle. Management and inference operations use the same production
runtime contracts.

## Configuration flow

Settings are stored in a versioned configuration file in the user's
application-data directory. Browser management and headless operation use that
same configuration. API credentials remain server-side; the browser is not their
source of truth.

The management API passes a proposed change to the configuration owner, which
validates it with the affected runtime owners before accepting it. Rejected
changes preserve the previous saved and effective configuration and return a
specific error. Persist accepted changes atomically.

Each setting identifies when it takes effect: immediately, on model reload, or
on server restart. The interface shows saved and effective values separately
when they differ. A failed activation keeps the previous effective value and
reports the failure; a saved or pending value must not appear as successfully
applied. Resource changes respect active requests and runtime ownership.

Hardware discovery supplies first-run defaults. Advanced placement, offload,
context, and scheduling controls expose only supported capabilities and explain
their effect on available memory and concurrency.

## Monitoring flow

Runtime owners publish model loading, memory accounting, scheduling, execution,
and failure state. Serving exposes a current snapshot and a bounded event stream.
The browser renders those observations rather than estimating runtime state from
its own requests or timers.

A reconnect obtains a consistent current view. If retained events cannot cover
a gap, refresh from a snapshot. Slow or disconnected browsers cannot grow an
unbounded queue or block inference. Missing metrics appear as unavailable rather
than zero; failures and stale connections remain visible.

Request cancellation is an explicit, authorized command to the owning runtime.
Disconnecting the monitoring interface does not cancel work. Monitoring retains
operational metadata by default. Prompt and response retention is opt-in through
an explicit diagnostic setting.

## Access boundary

The management interface defaults to loopback. Access checks distinguish
administration from inference, and validate browser origins and hosts. An
inference client key cannot change configuration, manage models, or inspect and
cancel other clients' work through the management API.

Network inference access is enabled explicitly, with client keys for household
or team applications. Enabling it does not expose administrative routes or grant
administrative permissions. Remote administration initially uses SSH forwarding
to the loopback management interface. Exact ports, authentication mechanics, and
whether listeners share an implementation remain to be defined within these
boundaries.
