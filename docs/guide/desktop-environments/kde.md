---
id: use-kde-plasma-on-openruyi
title: How to use KDE Plasma on openRuyi
description: This section provides guide on how to install, log in to, and customize the KDE Plasma desktop session on openRuyi.
slug: /guide/desktop-environments/kde
---

# How to use KDE Plasma on openRuyi

This article explains how to install, log in to, and customize the KDE Plasma desktop session on openRuyi. KDE Plasma is a full-featured desktop environment. On openRuyi, it is provided as a complete KDE Plasma environment by the `openruyi-desktop-setup-kde` package.

## Installation

If you are using an image that does not come with the desktop environment preinstalled, run the following command to install it:

```bash
sudo dnf install sddm openruyi-desktop-setup-kde
```

Then restart the display manager so that the new session becomes available:

```bash
sudo systemctl restart sddm
```

:::warning Warning

Restarting SDDM closes any graphical session that is currently running. Save your work before running the command.

:::

Installing `openruyi-desktop-setup-kde` brings in the Plasma workspace and the core applications it depends on, including:

* `plasma-workspace`, `plasma-desktop`, and `plasma-session`, which provide the desktop services, the panel, and the session management.

* `systemsettings`, the configuration application of Plasma.

* `konsole` and `dolphin`, the terminal emulator and the file manager.

A few additional applications, such as `discover`, `falkon`, and `mpv`, are recommended rather than required. They are installed by default, and you may skip them with `--setopt=install_weak_deps=False` if you prefer a smaller installation.

## Log In

Select the `Plasma` session in SDDM and log in. openRuyi runs Plasma on Wayland by default.

## Customization

### System Settings

Most of the Plasma desktop is customized through the graphical **System Settings** application, which you can launch from the application launcher or by running `systemsettings`. Appearance, panels, window behavior, keyboard shortcuts, displays, and input devices are all configured there, and the changes are written to the configuration files described below.

### Configuration files

Plasma follows the XDG configuration layout. The system-wide preset configuration files are located in the `/etc/xdg/` directory, and the per-user configuration files are located in the `~/.config/` directory.

:::warning Note

Configuration files in the user directory take precedence over the system-wide preset files, so they are the ones that take effect.

:::

The `~/.config/` directory usually contains the following files:

* `kdeglobals`

  Defines the settings shared by all KDE applications, such as fonts, the color scheme, the icon theme, and the single-click or double-click behavior.

* `kwinrc`

  Defines the behavior of KWin, the Plasma window manager and compositor, including window decorations, virtual desktops, tiling, and desktop effects.

* `plasma-org.kde.plasma.desktop-appletsrc`

  Defines the layout of the desktop and the panels, such as which widgets are present, where the panels are placed, and how they are sized.

* `plasmarc`

  Defines the Plasma theme and the general look and feel of the shell.

* `kglobalshortcutsrc`

  Defines the global keyboard shortcuts, such as the ones used to launch applications or to switch between virtual desktops.

Editing these files by hand is possible, but a running session may overwrite them when it exits. Change them either while no Plasma session is running, or with the `kwriteconfig6` command, which is the supported way to script configuration changes:

```bash
kwriteconfig6 --file kdeglobals --group General --key ColorScheme BreezeDark
```

The matching `kreadconfig6` command reads a value back:

```bash
kreadconfig6 --file kdeglobals --group General --key ColorScheme
```

### Autostart

Programs or scripts that should be executed automatically when the session starts are configured in **System Settings → Autostart**, which writes desktop entries to the `~/.config/autostart/` directory.

Scripts that need to run before the desktop shell starts, such as the ones setting environment variables for an input method, should be placed in the `~/.config/plasma-workspace/env/` directory instead.

### Wallpaper

The openRuyi wallpapers are installed in the `/usr/share/wallpapers/` directory, and the `openruyi-desktop-setup-kde` package replaces the images of the default `Next` wallpaper with the openRuyi artwork.

To choose a different wallpaper, right-click the desktop and select **Configure Desktop and Wallpaper**, or open **System Settings → Wallpaper**.

### Login screen

The SDDM login screen is configured in **System Settings → Login Screen (SDDM)**. If you prefer to edit the configuration directly, place your own configuration files in the `/etc/sddm.conf.d/` directory.

## Further Reading

* [KDE Plasma user guide](https://userbase.kde.org/Plasma)

* [KDE configuration files reference](https://userbase.kde.org/KDE_System_Administration/Configuration_Files)

* [KDE documentation](https://docs.kde.org/)
