# Product

Poppins serves the largest practical models on hardware people can obtain or
already own. It is intended for a household, a small group of developers, or one
enthusiast running multiple agents.

## Hardware envelope

Design for consumer hardware, including NVIDIA RTX 30-series GPUs, Intel CPUs,
and AMD Strix Halo systems, with at most 64 GB system RAM. Include MacBook Pro
models with 64 GB unified memory, targeting the M3 generation first because
M3 hardware is available for direct testing.

Treat discrete GPU memory and unified memory according to the actual machine's
topology and available budget. On unified-memory systems, CPU and GPU allocations
share the same physical memory budget. Hardware targets are requirements, not
claims of tested support.

## Serving requirements

- Load and execute models within the available resources.
- Handle concurrent clients and agent workloads with explicit scheduling and
  resource limits.
- Stream output and handle cancellation and failures predictably.
- Make configuration and operation practical for the intended users.

Model capacity is evaluated together with output quality, context length,
responsiveness, and concurrent serving behavior. Merely loading weights does
not demonstrate useful serving. Concrete supported configurations and performance
claims require verification on the hardware concerned.

Research and existing implementations inform engineering choices. Backend reuse,
custom execution, offload mechanisms, protocols, and implementation languages are
chosen to meet these requirements; this document does not select them.

## Configuration and monitoring

Distribute the server and its browser interface together. A user starts Poppins,
opens its localhost address, chooses a model, and copies the inference endpoint
and a client key into their applications or agents. Running a distributed build
does not require a separate frontend process, Node, or Python installation.

First launch detects hardware and offers sensible defaults. The interface has
four areas:

| Area | User capabilities |
| --- | --- |
| Overview | Server readiness, loaded model, memory usage, active and queued requests, throughput, and recent errors |
| Models | Add local models, inspect requirements, configure serving settings, and load or unload models |
| Requests | Inspect client activity, progress, queue time, generation speed, and failures; cancel requests |
| Settings | Model storage, memory budgets, concurrency, network access, and client API keys |

Advanced controls expose supported placement, offload, context, and scheduling
options with their practical consequences. Model download management is outside
the initial interface scope.

Settings persist on the server and work in headless operation. The interface
distinguishes configured settings from effective settings and identifies changes
requiring a model reload or server restart. Closing the browser does not stop
serving, and reconnecting restores the current view.

Administration is local by default. Users can explicitly enable inference access
for a household or team without granting administrative access to those clients.
Remote administration initially uses SSH forwarding. Request monitoring shows
operational metadata; retaining prompts and responses requires an explicit
diagnostic option.

See [the application architecture](architecture/application.md) for ownership
and data flow. These are product requirements, not delivered capabilities.
