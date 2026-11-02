# Architecture boundaries

The ownership boundaries below guide implementation. They do not describe
implemented modules or select an execution backend.

| Owner | Responsibility |
| --- | --- |
| Application | Browser configuration and monitoring interface |
| Serving | Bundled application delivery, management and inference APIs, access checks, streaming, and external errors |
| Runtime | Model lifecycle, resource policy, scheduling, and execution coordination |
| Backends | Concrete execution capabilities behind explicit runtime contracts |
| Platform | OS services and hardware discovery |
| Hosts | Persistent configuration, startup, shutdown, and composition |

Serving translates client requests and cancellation into runtime operations.
The runtime owns scheduling and memory policy. Backends implement execution
capabilities and report their constraints and failures. Hosts compose these
parts into a running server.

The bundled browser application is a client of the management API. Hosts own
persistent configuration and coordinate changes with the affected runtime owners.
Runtime owners publish monitoring state; serving transports it to the browser.
Serving continues independently of browser connections. Administration defaults
to loopback and remains separate from explicitly enabled network inference access.
See [application architecture](application.md) for these contracts and flows.

Protocol details do not determine runtime ownership. Backend-specific types stay
behind their boundary unless a public contract requires them. Platform services
do not depend on serving protocols. Tools and benchmarks exercise production
modules rather than maintaining alternate inference implementations.

The [source layout](source-layout.md) maps these responsibilities to directories.
Subsystem documents describe their contracts and flows as those are established.
