---
id: use-labwc-on-openruyi
title: How to use labwc on openRuyi
description: This section provides guide on how to install, log in to, and customize the labwc desktop session on openRuyi.
slug: /guide/desktop-environments/labwc
---

# How to use labwc on openRuyi

This article explains how to install, log in to, and customize the labwc desktop session on openRuyi. labwc is a lightweight Wayland compositor. On openRuyi it is shipped together with a preset configuration and a Waybar status bar, provided by the `openruyi-desktop-setup-labwc` package.

## Installation

If you are using an image that does not come with the desktop environment preinstalled, run the following command to install it:

```bash
sudo dnf install sddm openruyi-desktop-setup-labwc
```

Then restart the display manager to start SDDM:

```bash
sudo systemctl restart sddm
```

## Log In

Select the `labwc` session in SDDM and log in.

## Customization

### labwc

The system-wide preset configuration files for labwc are located in the `/etc/xdg/labwc/` directory.

To customize the session, create the corresponding configuration files in the `~/.config/labwc/` directory.

:::warning Note

Configuration files in the user directory take precedence over the system-wide preset files, so they are the ones that take effect.

:::

The `/etc/xdg/labwc/` directory usually contains the following files:

* `autostart`

  Defines the programs or scripts that are executed automatically when the session starts. Launching Waybar, an input method, a notification service, or setting the wallpaper is normally configured here.

* `menu.xml`

  Defines the contents of the labwc menu, which generally corresponds to the right-click menu or the application menu. You can add, remove, or reorder menu entries here, such as the terminal, the file manager, log out, and shut down.

* `rc.xml`

  Defines the core behavior of labwc, including window management, themes, keyboard shortcuts, mouse actions, and workspace settings. Most customization related to desktop interaction behavior is done in this file.

### Waybar

The system-wide preset configuration files for Waybar are located in the `/etc/xdg/waybar/` directory, and mainly include the following files:

* `config.jsonc`

  Defines the overall layout and module configuration of Waybar, such as which modules are displayed, the order and position of the modules, and the behavior of each module.

* `style.css`

  Defines the appearance of Waybar, such as fonts, colors, margins, backgrounds, and hover effects.

* `power_menu.xml`

  Defines the contents of the power button menu, such as the log out, reboot, and shut down entries and how they are displayed.

To customize Waybar, place your own configuration files in the `~/.config/waybar/` directory.

:::warning Note

Configuration in this directory also overrides the system-wide preset configuration.

:::

## Further Reading

* [labwc configuration manual](https://labwc.github.io/labwc-config.5)
