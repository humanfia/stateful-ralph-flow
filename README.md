# stateful_ralph _(stateful-ralph-flow)_

The Ralph loop with memory, as an hmz flow: the task again and again in one session that remembers every round.

One agent is given the task again and again in one session, so every round remembers the rounds
before it. It is the `stateful_ralph` that [FlowBench](https://humanfia.ai/flowbench/) scores;
[ralph_loop](https://github.com/humanfia/ralph-loop-flow) is the same loop with a fresh session
every round.

## Table of Contents

- [Install](#install)
- [Usage](#usage)
  - [What ends it](#what-ends-it)
  - [Picking it up](#picking-it-up)
- [Maintainers](#maintainers)
- [Contributing](#contributing)
- [License](#license)

## Install

You need [hmz](https://github.com/humanfia/humanize). In hmz, open `/flow`, go to
**Flowverses → official → stateful_ralph** and **Install** it.

To run a release without installing it, name it by its git ref:

```sh
hmz exec -f git+https://github.com/humanfia/stateful-ralph-flow@v0.1.0#stateful_ralph ...
```

## Usage

```text
❯ $stateful_ralph the task
```

```sh
hmz exec -f stateful_ralph -a agent=claude/claude-opus-5:high \
    -p budget.cost=5 "the task"
```

| Role | Needs | |
| --- | --- | --- |
| `agent` | nothing | Takes every round, in one session. |

The flow takes no params of its own.

### What ends it

The budget: the turn that finds it spent ends the run. A turn that fails ends the run with that
failure, once hmz has retried what could be retried.

### Picking it up

The session is kept after every round, so `--resume` carries the conversation on from the last
round that finished.

Another flow can call it by ref, `load("stateful_ralph")`; see
[A flow that calls a flow](https://humanfia.ai/humanize/weaver/calling-flows).

## Maintainers

[@futrime](https://github.com/futrime), as listed in [`.github/CODEOWNERS`](.github/CODEOWNERS).

## Contributing

Issues and pull requests are welcome. The flow is the `stateful_ralph/` directory; its tests are in
`tests/`. With [uv](https://docs.astral.sh/uv/):

```sh
uv sync
uv run ruff check
uv run ruff format --check
uv run pytest
```

CI runs the same on every pull request. A release is a `vX.Y.Z` tag on `main`; it reaches hmz
users once a `flows/stateful_ralph/X.Y.Z/flow.yaml` pointing at it is merged into
[humanfia/flowverse](https://github.com/humanfia/flowverse).

## License

[Apache-2.0](LICENSE) © Humanfia
