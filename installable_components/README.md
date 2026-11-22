# Installable components and upstream source catalog

This directory contains runtime archives only when they have been built for WinMali's Android environment and validated against the app's installer.

The following component folders currently contain **source metadata only**, not installable runtime archives:

- `box86/` — upstream Box86 source; requires an Android-compatible ARM32 runtime build.
- `proton/` — Valve Proton source; upstream is a Steam Play/Linux compatibility tool, not an Android-ready WinMali bundle.
- `fex-emu/` — upstream FEX-Emu source; Linux AArch64 builds are not automatically Android/Bionic compatible.
- `mesa-virgl/` — Mesa and VirGL upstream project references; a compatible Android graphics build and matching renderer integration are required.
- `wine/` — Wine source; WinMali needs a build matching its root filesystem, ABI, and runtime layout.

Each folder's `component.json` records the canonical upstream project and the current packaging status.

## Packaging rules

1. Do not add source tarballs to the runtime version indexes.
2. Do not label a source checkout or Linux binary as an Android runtime bundle.
3. Build for the exact Android ABI and WinMali rootfs/runtime layout.
4. Validate archive structure, required executables/libraries, licensing notices, and checksums.
5. Test installation and launch in a disposable container before marking a component installable.
6. Keep GPU requirements explicit. Turnip is for supported Qualcomm Adreno GPUs, not Mali GPUs.

A component should only be promoted to an installable runtime after these checks pass.
