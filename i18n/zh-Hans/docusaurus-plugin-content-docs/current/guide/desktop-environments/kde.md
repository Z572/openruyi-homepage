---
id: use-kde-plasma-on-openruyi
title: 如何在 openRuyi 上使用 KDE Plasma
description: 这篇文章教学如何在 openRuyi 上安装、登录并自定义 KDE Plasma 桌面会话。
slug: /guide/desktop-environments/kde
---

# 如何在 openRuyi 上使用 KDE Plasma

本文章介绍了如何在 openRuyi 上安装、登录并自定义 KDE Plasma 桌面会话。KDE Plasma 是一个功能完整的桌面环境，openRuyi 通过 `openruyi-desktop-setup-kde` 软件包为其提供了完整的KDE Plasma 环境。

## 安装

如果您使用的是未预装相关环境的镜像，请执行以下命令安装：

```bash
sudo dnf install sddm openruyi-desktop-setup-kde
```

然后重启显示管理器，使新的会话可用：

```bash
sudo systemctl restart sddm
```

:::warning 注意

重启 SDDM 会关闭当前正在运行的图形会话。请在执行该命令前保存您的工作。

:::

安装 `openruyi-desktop-setup-kde` 会一并安装 Plasma 工作空间及其依赖的核心应用，包括：

* `plasma-workspace`、`plasma-desktop` 和 `plasma-session`，提供桌面服务、面板以及会话管理。

* `systemsettings`，Plasma 的配置程序。

* `konsole` 和 `dolphin`，即终端模拟器和文件管理器。

此外还有若干推荐（而非必需）的应用，例如 `discover`、`falkon` 和 `mpv`。它们默认会被一同安装，如果您希望安装体积更小，可以使用 `--setopt=install_weak_deps=False` 跳过它们。

## 登录

在 SDDM 中选择 `Plasma` 会话并登录即可。openRuyi 默认在 Wayland 上运行 Plasma。

## 自定义

### 系统设置

Plasma 桌面的绝大多数自定义都通过图形化的**系统设置**程序完成，您可以从应用启动器中打开它，或者执行 `systemsettings` 命令。外观、面板、窗口行为、键盘快捷键、显示器以及输入设备等都在这里配置，所做的更改会被写入下文介绍的配置文件中。

### 配置文件

Plasma 遵循 XDG 配置文件布局。系统预配配置文件位于 `/etc/xdg/` 目录下，用户配置文件位于 `~/.config/` 目录下。

:::warning 注意

用户目录下的配置文件优先级高于系统预配配置文件，因此会优先生效。

:::

`~/.config/` 目录下通常包含以下文件：

* `kdeglobals`

  用于定义所有 KDE 应用共用的设置，例如字体、配色方案、图标主题以及单击或双击的操作方式。

* `kwinrc`

  用于定义 Plasma 的窗口管理器与合成器 KWin 的行为，包括窗口装饰、虚拟桌面、平铺以及桌面特效等。

* `plasma-org.kde.plasma.desktop-appletsrc`

  用于定义桌面和面板的布局，例如包含哪些部件、面板的位置以及尺寸等。

* `plasmarc`

  用于定义 Plasma 主题以及外壳的整体外观风格。

* `kglobalshortcutsrc`

  用于定义全局键盘快捷键，例如启动应用或切换虚拟桌面所使用的快捷键。

您可以手动编辑这些文件，但正在运行的 Plasma 会话可能会在退出时覆盖它们。因此请在没有 Plasma 会话运行时修改，或者使用 `kwriteconfig6` 命令，这也是脚本化修改配置的推荐方式：

```bash
kwriteconfig6 --file kdeglobals --group General --key ColorScheme BreezeDark
```

与之对应的 `kreadconfig6` 命令用于读取配置值：

```bash
kreadconfig6 --file kdeglobals --group General --key ColorScheme
```

### 自启动

会话启动时需要自动执行的程序或脚本，可以在**系统设置 → 开机启动**中配置，对应的桌面条目会被写入 `~/.config/autostart/` 目录。

如果脚本需要在桌面外壳启动之前运行，例如为输入法设置环境变量，则应改为放置在 `~/.config/plasma-workspace/env/` 目录下。

### 壁纸

openRuyi 的壁纸安装在 `/usr/share/wallpapers/` 目录下，同时 `openruyi-desktop-setup-kde` 软件包会将默认壁纸 `Next` 的图片替换为 openRuyi 的图片。

如果您想更换壁纸，可以右键点击桌面并选择**配置桌面和壁纸**，或者打开**系统设置 → 壁纸**。

### 登录界面

SDDM 登录界面可以在**系统设置 → 登录屏幕 (SDDM)** 中配置。如果您想直接编辑配置，请在 `/etc/sddm.conf.d/` 目录下放置自己的配置文件。

## 延伸阅读

* [KDE Plasma 使用指南](https://userbase.kde.org/Plasma)

* [KDE 配置文件参考](https://userbase.kde.org/KDE_System_Administration/Configuration_Files)

* [KDE 文档](https://docs.kde.org/)
