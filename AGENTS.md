# Repository guidelines

Fedora Foundry is currently a skeleton. Do not describe unimplemented features
as working or validated.

Use Rust for the application and Bash for focused builder scripts. The planned
TUI stack is Ratatui with Crossterm. Keep UI, configuration, and build execution
separate when implementing them. Builder assets belong in `builder/`;
operational documentation belongs in `docs/`.

Run `cargo fmt --check` and `cargo check --locked` for Rust changes. Add meaningful
tests as behavior is introduced. Validate Bash with `bash -n` and ShellCheck.
A real ISO build and boot/install smoke test are needed to validate the backend.

Never overwrite existing outputs silently. Keep credentials, runtime state,
logs, images, and build artifacts out of Git. Avoid changing host SELinux or
mounting host disks into the builder. Document actual container permissions.

Use focused Conventional Commits. Track deferred work in GitHub Issues when
requested; do not maintain a parallel backlog in repository files.
