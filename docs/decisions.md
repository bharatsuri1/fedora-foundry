# Project decisions

## Scope

Fedora Foundry will build custom Fedora live ISOs. The first implementation
will target Linux x86_64 with Docker. Other hosts, architectures, disk cloning,
and USB writing are outside the initial scope.

This repository begins with structure and documentation only. No image build
has been attempted and no backend compatibility has been established.

## Application

Use Rust for the application, with Ratatui and Crossterm for the planned TUI.
The interface should offer a short guided flow, keyboard navigation, readable
progress, and actionable errors. Dependencies will be added with the UI
implementation; the skeleton has no third-party Rust dependencies.

## Build backend

Use Docker to package Fedora, Lorax, Kickstart tools, and related dependencies.
Use `livemedia-creator` from Lorax to produce the live ISO. Begin from official
Fedora live Kickstarts matched to the selected release rather than inventing
live-boot configuration.

Evaluate QEMU-backed image installation before using `--no-virt`. Container
isolation alone is not sufficient justification for privileged Anaconda builds.
The supported mode, device access, SELinux handling, and required permissions
remain open until an actual build is validated. Do not disable host SELinux
or automatically run privileged containers as a workaround.

## Setup and outputs

The intended user prerequisite is Docker installed and running. Foundry should
prepare its own image and tooling; users should not need to install Lorax or
edit Kickstart files for the guided flow. Distribution of the application
binary will be decided when a usable implementation exists.

Keep each build in a separate output directory. Preserve the generated
Kickstart, source provenance, logs, final ISO, and SHA-256 checksum for recovery
and reproducibility. Refuse collisions; failed builds must retain useful logs.
Cancellation must stop the builder and clean up temporary resources without
removing completed output or unrelated containers.

## Validation before release

Verify a complete build, live boot, and installation in a disposable VM.
Document measured resource requirements and the supported Fedora release
matrix. Resolve container permissions and Fedora Kickstart source selection
before calling the workflow supported.
