# WinMali

WinMali is an Android project based on [Winlator](https://github.com/brunodev85/winlator). It aims to make running compatible Windows applications on Android more understandable and configurable, with particular attention to graphics compatibility on Mali-based devices.

WinMali builds on established open-source projects such as Wine, Box86/Box64, and Mesa-related graphics components. Compatibility depends on the Android device, GPU, available drivers, runtime components, application, and WinMali build. No single configuration can run every Windows application or game.

> **Project status:** WinMali is under development. There is currently no public WinMali APK release. Features described as planned below should not be treated as implemented or tested.

## Table of contents

- [About the project](#about-the-project)
- [Project goals](#project-goals)
- [Development status](#development-status)
- [Graphics and Mali compatibility](#graphics-and-mali-compatibility)
- [Compatibility and performance](#compatibility-and-performance)
- [Installation](#installation)
- [Building from source](#building-from-source)
- [Useful tips](#useful-tips)
- [Reporting bugs](#reporting-bugs)
- [Development standards](#development-standards)
- [Repository structure](#repository-structure)
- [Credits and third-party projects](#credits-and-third-party-projects)
- [License](#license)

## About the project

Winlator provides an environment for running supported Windows software on Android. It combines Wine with CPU translation components such as Box86 and Box64, alongside graphics and audio components that help connect Windows applications to Android hardware.

WinMali starts from that upstream project and is intended to develop a more device-aware experience for Mali-based Android devices. The aim is not to claim that every Mali GPU behaves the same, or that every graphics backend works on every device. The aim is to identify what the device actually supports, expose compatible options, and explain unavailable options instead of presenting misleading settings.

The project is community-driven and depends on the work of the upstream developers and third-party projects listed in the credits.

## Project goals

The WinMali development direction includes:

- **GPU awareness:** identify the available GPU, renderer, graphics APIs, and driver information where Android exposes them.
- **Honest graphics configuration:** show graphics backends only when their requirements are met, and explain unsupported or incompatible choices.
- **Container controls:** make it easier to create, duplicate, rename, back up, restore, import, and export containers without risking existing data.
- **Wine and Box64 configuration:** make runtime versions, architecture information, presets, and environment variables easier to inspect and configure.
- **Performance information:** provide useful CPU, memory, storage, frame-rate, and thermal information when the platform can report it reliably.
- **Input support:** improve controller detection and configuration, including Bluetooth controllers.
- **Diagnostics:** make startup failures, component problems, and process output easier to understand.
- **Compatibility layers:** investigate importing and managing additional Wine-based builds, including compatible Proton-family builds, with package validation and clear compatibility warnings.

These are development goals, not a claim that every item is already available. Support will be documented as each feature is implemented and verified.

## Development status

The current repository is based on the Winlator source tree. Its app, Vortek, and Gladio components are linked as Git submodules. The app submodule points to the WinMali application fork, while Vortek and Gladio remain linked to their upstream repositories:

- [WinMali app source](https://github.com/worstpossibleuserlol/winmali-app)
- [Vortek](https://github.com/brunodev85/vortek)
- [Gladio](https://github.com/brunodev85/gladio)

This means the main repository tracks specific revisions of separately maintained components. A change made in a submodule is not automatically part of WinMali; the corresponding submodule revision must also be updated in the main repository.

WinMali-specific application changes, release builds, and device compatibility results will be documented as they become available. Until an APK is published in the official Releases page, there is no official WinMali installer to download.

## Graphics and Mali compatibility

Graphics compatibility is one of the main areas that WinMali intends to make clearer. The correct graphics path depends on the GPU, Android driver, available APIs, and the components included in a particular build.

### Important driver notes

- **Turnip is for supported Qualcomm Adreno GPUs. It is not a Mali GPU driver.** Selecting or installing Turnip does not make it a suitable driver for Mali hardware.
- **Zink** translates OpenGL calls to Vulkan. It needs a working Vulkan implementation and compatible supporting components.
- **VirGL** uses a virtualized graphics approach. Its availability and performance depend on how it is packaged and integrated in a given build.
- **OpenGL ES and Vulkan** availability must be checked on the actual device. An Android device having one graphics API does not automatically mean every Wine graphics translation layer can use it.
- **DXVK and VKD3D** rely on a compatible Vulkan path. They should not be presented as usable when that requirement is missing.

A graphics option appearing in another Winlator-based application does not prove that it is suitable for a particular Mali device. WinMali should report compatibility based on actual detection and validation, not assumptions based only on a GPU brand.

## Compatibility and performance

Windows application compatibility varies. Some programs may work well, some may require individual configuration, and others may not work because of unsupported instructions, graphics features, dependencies, DRM, launchers, or other limitations.

Performance can be affected by:

- CPU architecture and performance.
- GPU model, driver quality, and graphics backend.
- Available RAM and background activity.
- Game resolution, rendering settings, and frame-rate targets.
- Wine and Box64 versions and configuration.
- Device temperature and power-management behavior.
- The application or game itself.

No universal FPS figure or compatibility guarantee is made for all devices. Results should be reported with the device model, Android version, GPU, WinMali build, graphics backend, and application settings used during the test.

## Installation

**There is currently no public WinMali APK release.**

When an official build is published, it will be listed on the [WinMali GitHub Releases page](https://github.com/worstpossibleuserlol/WinMali/releases).

For an official release:

1. Open the WinMali Releases page.
2. Download the APK attached to the relevant release.
3. Review that release's notes and known issues.
4. Install the APK on a compatible Android device.
5. Launch WinMali and allow its initial setup to complete.

Only treat builds published through the official WinMali repository as official releases. Do not assume that an APK from another project or an unofficial mirror is an identical WinMali build.

## Building from source

The top-level WinMali repository tracks the project and its dependencies. Several components are Git submodules, so a normal clone without submodules will not retrieve all of the source required for development.

Clone the repository with its submodules:

```bash
git clone --recurse-submodules https://github.com/worstpossibleuserlol/WinMali.git
cd WinMali
```

The Android application source is in the `app` submodule. The graphics components are maintained separately. Before building, make sure the submodules are initialized and checked out at the revisions recorded by the main repository.

A verified WinMali-specific build procedure will be added after the complete source and dependency setup has been validated end to end. Until then, the upstream build configuration should not be mistaken for a tested WinMali release process.

## Useful tips

The following guidance is adapted from the upstream Winlator project. Menu names and availability may differ between versions.

- If an application is unstable, try a different Box64 preset in **Container Settings → Advanced**, then test the same scenario again.
- For applications that require .NET Framework, check whether **Wine Mono** is available under **Start Menu → System Tools → Installers**.
- For certain older games on compatible Mesa-based graphics paths, the environment variable `MESA_EXTENSION_MAX_YEAR=2003` may help. It is not a universal fix and should only be used when relevant to the graphics stack.
- Use individual game shortcuts when you need settings that differ between applications.
- For some low-resolution games, the **Force Fullscreen** option may improve display scaling.
- For some Unity applications, changing the Box64 preset to `Stability` or trying the execution argument `-force-gfx-direct` may help. These options are application-dependent.
- If audio crackles, check the ALSA/PulseAudio configuration and experiment with latency settings supported by the build. Higher latency can reduce some audio problems but may add delay.

Change one setting at a time when troubleshooting. That makes it easier to identify which setting helped or caused a new problem.

## Reporting bugs

Useful bug reports make problems easier to reproduce and fix. When opening an issue, include as much of the following information as you can:

- Device model and chipset.
- GPU model and Android version.
- WinMali version or exact source commit.
- Windows application or game being launched.
- Container configuration and graphics backend.
- Steps that reproduce the issue.
- The exact error message and relevant WinMali, Wine, or Box64 logs.
- Whether the issue also occurs with the original configuration or only after a specific setting is changed.

Please remove personal information, account details, and private files from logs before posting them. Avoid reporting a problem as fixed until the same steps have been tested again on the affected setup.

## Development standards

WinMali development follows these standards:

1. **Inspect before changing.** Check the relevant source code, dependencies, build configuration, and call sites before proposing a code fix. Do not fill gaps with guesses.
2. **Fix confirmed bugs properly.** Investigate every confirmed bug, identify its cause, implement a suitable fix, and run relevant checks. If it cannot yet be verified, keep that limitation visible instead of calling it fixed.
3. **Test before claiming.** Do not claim that a build compiles, an APK installs, a feature works, or a device test passed unless that specific check was actually performed.
4. **Protect user data.** Container files, saves, settings, and imported components must be handled carefully. Destructive operations require validation and clear confirmation.
5. **Avoid fake features.** Do not add placeholder controls or describe planned features as working features. Unsupported options should be identified clearly.
6. **Check regressions.** After a fix, review related code paths and run relevant regression checks, not only the test that first exposed the problem.
7. **Keep repository changes traceable.** Code and documentation changes should be committed to the appropriate WinMali repository. Changes to submodules must be reflected by updating the relevant submodule reference in the main repository.
8. **Be transparent.** Document known issues, untested behavior, and device-specific limitations. Do not promise perfect compatibility or claim that a project is bug-free.
9. **Avoid destructive repository actions.** Do not delete, replace, or restructure repositories or important project files without explicit approval and a clear understanding of the impact.

These standards are intended to make releases more reliable and the project's status easier to trust.

## Repository structure

The main repository contains the following project areas:

| Path | Purpose |
| --- | --- |
| `app/` | Android application source, maintained as a Git submodule. |
| `vortek/` | Vortek graphics component, maintained as a Git submodule. |
| `gladio/` | Gladio graphics component, maintained as a Git submodule. |
| `android_alsa/` | Android ALSA-related source and configuration. |
| `glibc_patches/` | GLIBC compatibility patch resources. |
| `input_controls/` | Input-control resources. |
| `installable_components/` | Installable component resources. |
| `wine_addons/` | Wine add-on resources. |

The exact files and component revisions can change as the project develops.

## Credits and third-party projects

WinMali is possible because of the work of the original Winlator developers and the maintainers of the open-source components it builds upon.

- [Winlator](https://github.com/brunodev85/winlator) — upstream Android project.
- [WinMali app source](https://github.com/worstpossibleuserlol/winmali-app) — WinMali's Android application source fork.
- [Winlator app source](https://github.com/brunodev85/winlator-app) — upstream application source.
- [Termux Pacman GLIBC packages](https://github.com/termux-pacman/glibc-packages) — GLIBC patches.
- [Wine](https://www.winehq.org/) — Windows compatibility layer.
- [Box86 and Box64](https://github.com/ptitSeb) — x86 and x86-64 userspace translation.
- [Mesa](https://www.mesa3d.org/) — graphics drivers and supporting graphics components.
- [DXVK](https://github.com/doitsujin/dxvk) — Direct3D 9/10/11 to Vulkan translation.
- [VKD3D](https://gitlab.winehq.org/wine/vkd3d) — Direct3D 12 to Vulkan translation.
- [CNC DDraw](https://github.com/FunkyFr3sh/cnc-ddraw) — DirectDraw compatibility component.

All third-party projects remain the work of their respective authors and maintainers. Please consult their repositories for their own documentation, contribution rules, and license terms.

## License

The WinMali repository contains the **GNU Lesser General Public License v2.1 (LGPL-2.1)**. Some submodules and third-party components may have separate licenses or notices. Review the relevant license files before redistributing modified builds or individual components.

---

Thank you to everyone who contributes to the upstream projects, tests compatibility, reports issues, and helps improve WinMali.
