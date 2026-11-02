# Working on Poppins

## Goal

Build an inference serving harness that serves the largest practical models on
hardware people can obtain or already own: consumer GPUs, including NVIDIA RTX
30-series, Intel or Strix Halo systems with at most 64 GB system RAM, and
MacBook Pro models with 64 GB unified memory, targeting the M3 generation first.
Serve households, small developer groups, and individuals running multiple agents.

## Engineering

- Size the implementation by product needs. Research informs the design;
  delivery means working serving functionality.
- Make ownership, lifetimes, resource limits, and failure behavior explicit at
  subsystem boundaries. Do not hide incomplete functionality behind success.
- Distinguish proposed, implemented, and verified behavior. Cite technical
  sources where they explain a mechanism or constraint.
- Keep architecture docs concise: contracts, ownership, dependencies, and flows.
  Git history records their evolution. Plans and research stay in ignored
  `local/`; model weights, downloads, and generated output stay out of Git.
- Keep this file short and applicable to every agent. Procedures belong in
  skills; role instructions belong in agent definitions.

## Testing

- Test public contracts, including resource exhaustion, cancellation, and
  failure behavior where relevant. Name the contract before adding a test.
- Unit tests isolate behavior; integration tests exercise real boundaries;
  end-to-end tests send requests through the running server.
- Tests should survive implementation changes that preserve the contract.
  Do not test private structure or trivial forwarding to a dependency.
- Use the production execution path for serving benchmarks. Report hardware,
  model and quantization, workload, context length, concurrency, memory use,
  and timing alongside performance or capacity claims.
- Run checks appropriate to the change. Report commands actually run and any
  remaining verification gaps; a successful build alone does not verify behavior.

## Recurring problems

- **Turning delivery into a research project.** Research answers implementation
  questions; the end product is a serving harness.
- **Accumulating process documents.** Do not track plans, research journals,
  decision logs, or project memory. Update architecture and code instead.

## Start here

- [Product](docs/product.md)
- [Architecture](docs/architecture/overview.md) and [source layout](docs/architecture/source-layout.md)
- [Architect workflow](.agents/skills/architect/SKILL.md); roles in `.codex/agents/`
