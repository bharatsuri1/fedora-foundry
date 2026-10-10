# Builder boundary

This directory is reserved for the release-matched Fedora Dockerfile and Lorax
entrypoint. Neither is implemented yet.

The builder will accept a validated Kickstart and a dedicated build directory,
stream its logs, and return the ISO plus diagnostics. It must not require access
to host disks or the Docker socket. Determine the minimum container permissions
with a disposable build environment before defining the production entrypoint.

See [decisions](../docs/decisions.md) for the installation-mode decision and
[workflow](../docs/iso-workflow.md) for the intended sequence.
