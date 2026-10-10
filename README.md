# Fedora Foundry

A planned terminal app for building custom Fedora live ISOs with Lorax and Docker.
Choose a Fedora release, desktop, extra packages, and output directory; Foundry
will prepare the build environment and guide you through producing an ISO.

**Status: repository skeleton. ISO building and the TUI are not implemented.**

## Intended experience

1. Start `fedora-foundry`.
2. Choose a release and desktop.
3. Add optional packages and choose an output folder.
4. Review the build plan and start the build.
5. Follow progress and receive an ISO with a SHA-256 checksum.

The intended host prerequisite is a running Docker engine on Linux. Foundry
will manage build dependencies inside its container. Actual requirements and
container permissions must be verified before this promise is considered supported.

## Development

With the Rust stable toolchain installed:

```sh
cargo run
cargo fmt --check
cargo check --locked
```

The current binary only reports the project status. Development setup is separate
from the intended Docker-only end-user setup.

## Project layout

- `src/`: Rust application; future Ratatui interface and build orchestration.
- `builder/`: future Docker build environment and Lorax entrypoint.
- `docs/`: decisions, build workflow, and operational documentation.
- `.github/workflows/`: skeleton validation.

See [decisions](docs/decisions.md) and the [ISO workflow](docs/iso-workflow.md).
