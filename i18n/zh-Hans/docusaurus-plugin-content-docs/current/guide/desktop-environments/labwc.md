---
id: use-labwc-on-openruyi
title: 如何在 openRuyi 上使用 labwc
description: 这篇文章教学如何在 openRuyi 上安装、登录并自定义 labwc 桌面会话。
slug: /guide/desktop-environments/labwc
---

# 如何在 openRuyi 上使用 labwc

本文章介绍了如何在 openRuyi 上安装、登录并自定义 labwc 桌面会话。labwc 是一个轻量级的 Wayland 合成器，openRuyi 通过 `openruyi-desktop-setup-labwc` 软件包为其提供了预配置以及 Waybar 状态栏。

## 安装

如果您使用的是未预装相关环境的镜像，请执行以下命令安装：

```bash
sudo dnf install sddm openruyi-desktop-setup-labwc
```

然后重启显示管理器，使SDDM启动：

```bash
sudo systemctl restart sddm
```


## 登录

在 SDDM 中选择 `labwc` 会话并登录即可。

## 自定义

### labwc

labwc 的系统预配配置文件位于 `/etc/xdg/labwc/` 目录下。

如果您想进行自定义，可以在 `~/.config/labwc/` 目录中创建对应的配置文件。

:::warning 注意

用户目录下的配置文件优先级高于系统预配配置文件，因此会优先生效。

:::

`/etc/xdg/labwc/` 目录下通常包含以下文件：

* `autostart`

  用于定义会话启动时自动执行的程序或脚本。例如启动 Waybar、输入法、通知服务或设置壁纸等，通常都在这里配置。

* `menu.xml`

  用于定义 labwc 的菜单内容，一般对应右键菜单或应用菜单。您可以在这里添加、删除或调整菜单项，例如终端、文件管理器、注销和关机等功能。

* `rc.xml`

  用于定义 labwc 的核心行为配置，包括窗口管理、主题、键盘快捷键、鼠标操作以及工作区设置等。大多数与桌面交互行为相关的自定义，通常都在这个文件中完成。

### Waybar

Waybar 的系统预配配置文件位于 `/etc/xdg/waybar/` 目录下，主要包括以下文件：

* `config.jsonc`

  用于定义 Waybar 的整体布局和模块配置，例如显示哪些模块、模块排列顺序、位置以及各模块的行为设置。

* `style.css`

  用于定义 Waybar 的外观样式，例如字体、颜色、边距、背景、悬停效果等界面样式。

* `power_menu.xml`

  用于定义电源按钮菜单的内容，例如注销、重启、关机等操作项及其显示方式。

如果您想自定义 Waybar 配置，请在 `~/.config/waybar/` 目录下放置自己的配置文件。

:::warning 注意

该目录下的配置同样会优先覆盖系统预配配置。

:::

## 延伸阅读

* [labwc 配置手册](https://labwc.github.io/labwc-config.5)
