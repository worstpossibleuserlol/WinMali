<p align="center">
	<img src="logo.png" width="376" height="128" alt="WinMali Logo" />
</p>

<p align="center">
	<a href="https://github.com/worstpossibleuserlol/WinMali/releases">
		<img src="https://img.shields.io/github/v/release/worstpossibleuserlol/WinMali?style=flat-square&label=latest%20release" alt="Latest release" />
	</a>
	<a href="https://github.com/worstpossibleuserlol/WinMali/releases">
		<img src="https://img.shields.io/github/downloads/worstpossibleuserlol/WinMali/total.svg?style=flat-square&label=downloads" alt="Total downloads" />
	</a>
	<a href="https://github.com/worstpossibleuserlol/WinMali/stargazers">
		<img src="https://img.shields.io/github/stars/worstpossibleuserlol/WinMali?style=flat-square&logo=github&color=ffb300" alt="GitHub stars" />
	</a>
</p>

# WinMali

WinMali is an Android project based on [Winlator](https://github.com/brunodev85/winlator), designed to run compatible Windows (x86_64) applications with Wine and Box86/Box64.

The project focuses on graphics compatibility and usability on Mali-based Android devices. Actual compatibility and performance depend on the device, GPU driver, graphics backend, and WinMali build.

# Installation

**A public WinMali APK release has not been published yet.** When a build is available:

1. Download the APK from [WinMali GitHub Releases](https://github.com/worstpossibleuserlol/WinMali/releases).
2. Install the APK on your Android device.
3. Launch WinMali and wait for the initial setup to finish.

----

# Useful Tips

These tips are adapted from the Winlator project. Some options may differ or be unavailable depending on the WinMali build.

- If you experience instability, try changing the Box64 preset in **Container Settings → Advanced**.
- For applications that require .NET Framework, try installing `Wine Mono` from **Start Menu → System Tools → Installers**, if it is included in your build.
- For some older games on compatible Mesa-based graphics backends, try adding the environment variable `MESA_EXTENSION_MAX_YEAR=2003` in **Container Settings → Environment Variables**.
- Launch games using their shortcuts on the WinMali home screen when you need separate settings for individual games.
- To display some low-resolution games correctly, try enabling **Force Fullscreen** in the shortcut settings.
- For some Unity games, try the Box64 `Stability` preset or add the execution argument `-force-gfx-direct` in the shortcut settings.
- If you experience audio crackling, try increasing the average latency in the ALSA/PulseAudio configuration. The best value depends on the game and device.

# Graphics Compatibility

- Turnip is designed for supported Qualcomm Adreno GPUs. **Turnip is not a Mali graphics driver.**
- Zink, VirGL, Vulkan, and OpenGL ES support depends on the graphics components included in the build and on the device's drivers.
- Do not assume that a graphics option is supported just because it appears in another Winlator build.

# Credits and Third-party apps

- Winlator by [Bruno](https://github.com/brunodev85/winlator) — upstream project
- GLIBC patches by [Termux Pacman](https://github.com/termux-pacman/glibc-packages)
- Wine ([winehq.org](https://www.winehq.org/))
- Box86/Box64 by [ptitSeb](https://github.com/ptitSeb)
- Mesa ([mesa3d.org](https://www.mesa3d.org))
- DXVK ([github.com/doitsujin/dxvk](https://github.com/doitsujin/dxvk))
- VKD3D ([gitlab.winehq.org/wine/vkd3d](https://gitlab.winehq.org/wine/vkd3d))
- CNC DDraw ([github.com/FunkyFr3sh/cnc-ddraw](https://github.com/FunkyFr3sh/cnc-ddraw))

Special thanks to all the developers involved in these projects.  
Thank you to everyone supporting WinMali.
