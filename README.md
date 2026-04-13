# xell-builder

Automated build pipeline for XeLL Reloaded, a custom bootloader for the Xbox 360. Triggered via `workflow_dispatch`, it compiles XeLL with configurable colors and ASCII art, then commits the resulting release archive to this repository organized by date and build ID.

## How it works

1. **build**: Checks out `barrenechea/xell-reloaded`, applies the color and ASCII art customizations, runs `make dist` inside the `ghcr.io/barrenechea/libxenon` toolchain container, and uploads the resulting `tar.gz` as a workflow artifact.
2. **commit**: Always runs, even if **build** fails. Downloads the artifact (if any) and fetches the build job logs via the GitHub API, then commits both to `YYYY/MMDD/{id}/` in this repository.
