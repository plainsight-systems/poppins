# Source layout

This is a destination map. Create a directory when its responsibility has real
source or supporting content; do not create empty scaffolding or one directory
per class. Refine ownership as concrete contracts are established.

```text
app/                      # bundled browser configuration and monitoring interface

src/
  serving/                # app assets, management/inference APIs, access checks
  runtime/
    models/               # model metadata, loading lifecycle, availability
    memory/               # budgets, residency, movement policy
    scheduling/           # admission, queues, batching, fairness
    execution/            # execution coordination and backend contracts
  backends/               # concrete execution integrations and implementations
  platform/               # OS services and hardware discovery
  hosts/                  # persistent configuration, entry points, composition

tests/
  unit/                   # isolated public contracts, grouped by owner
  integration/            # real subsystem and platform boundaries
  end-to-end/             # requests through the running server
  fixtures/               # small redistributable test inputs

benchmarks/
  workloads/              # repeatable serving workload definitions
  configurations/         # model and runtime settings for those workloads
tools/                    # development utilities and benchmark runners
configs/                  # usable server examples and hardware profiles

docs/
  product.md
  architecture/           # contracts, ownership, dependencies, flows

.agents/skills/architect/ # coordinating workflow
.codex/agents/           # bounded role instructions and model choices
local/                   # ignored plans, research, machine configuration
out/                     # ignored generated output
```

Keep closely related public contracts and their implementations with their owner.
Tests mirror ownership. Build configuration should express actual dependencies
once the language and build system are selected.

The distributed server includes the built `app/` assets. The browser consumes
management APIs; it owns no inference, scheduling, or memory policy. Frontend
technology and asset packaging are implementation choices. See
[application architecture](application.md) for configuration and monitoring flows.

Hardware profiles describe capabilities and reproducible settings. Hostnames,
credentials, absolute model paths, downloaded weights, and large traces belong
in local or external storage.
