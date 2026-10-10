# ISO build workflow

This is the intended backend sequence, not an executable guide for the skeleton.

1. **Collect choices.** Select a supported Fedora release, desktop, additional
   package names, and a new output directory.
2. **Check prerequisites.** Verify Docker access, host architecture, available
   storage and memory, and the permissions required by the validated build mode.
3. **Prepare the builder.** Build or obtain a release-matched Fedora container
   containing Lorax, Kickstart tools, and the chosen installation backend.
4. **Prepare Kickstart.** Fetch official release-matched Fedora live Kickstarts,
   record the source revision, and add the user's package choices. Keep source
   includes available while flattening.
5. **Validate.** Resolve includes with `ksflatten`, validate the result with
   `ksvalidator`, and check that its repositories match the requested release.
6. **Review.** Show the resolved configuration, output destination, and required
   container permissions before starting the image build.
7. **Build.** Run `livemedia-creator --make-iso` with the validated Kickstart.
   Supply Anaconda installation media if using the QEMU backend. Stream stages
   and preserve full logs. Do not claim a percentage when Lorax provides none.
8. **Collect artifacts.** Verify the ISO exists and is nonempty, generate its
   SHA-256 checksum, and preserve the Kickstart, source provenance, and logs.
   Return artifacts with ownership usable by the invoking user.
9. **Verify the image.** Boot it in a disposable VM and test installation before
   treating the builder configuration as supported.

## Recovery requirements

A failed or cancelled build should leave diagnostics in its output directory.
A retry should use a fresh build directory. Cleanup must target only resources
created for that build. Never delete existing user files to make room for an ISO.

## Upstream references

- [Lorax livemedia-creator documentation](https://github.com/weldr/lorax/blob/master/docs/livemedia-creator.rst)
- [Fedora live image creation guide](https://fedoraproject.org/wiki/Livemedia-creator-_How_to_create_and_use_a_Live_CD)

These describe the underlying tools. Docker integration still requires validation.
