---
title: "manjaro使用小记"
date: 2023-05-28T14:18:37+08:00
tags: ["manjaro"]
categories: [""]
toc:
  enable: true
description: 
draft: true


---

<!--more-->

# pacman

## 常用命令

https://blog.csdn.net/qq_38202733/article/details/118893984

## 配置源

```
sudo vim /etc/pacman.conf
```

加在最后

```
[archlinuxcn]
SigLevel = Optional TrustAll
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
//或者使用清华的镜像源
[archlinuxcn]
SigLevel = Optional TrustAll
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
```

更新软件仓库

```
sudo pacman -Sy
```

安装`key-ring`

```
sudo pacman -S archlinuxcn-keyring
```

如果报错注释掉`/etc/pacman.conf`中的SigLevel

# paru

## 安装

更新源

```
sudo pacman -Syy
```

```
sudo pacman -S pkg-config 
```

安装git

```
sudo pacman -S git
```

将PARU安装包克隆到主机

```
git clone https://aur.archlinux.org/paru.git
```

切换到PARU安装包目录

```
cd paru/
```

 找到#MAKEFLAGS="-j2",去注释，并修改为MAKEFLAGS="-j$(nproc)"

可省略这一步

```
sudo vim /etc/makepkg.conf

MAKEFLAGS="-j$(nproc)" 
```

构建并安装PARU

```
makepkg -si
```

懂得都懂

```
alias yay=paru
```

# 常用软件安装

## 安装vscode 

```
paru -Ss vscode

paru -Sy visual-studio-code-bin
```

## 搜狗输入法

[原文](https://www.cnblogs.com/tonyc/p/8231667.html)

### 安装

#### 安装Fcitx

由于搜狗拼音输入法依赖于Fcitx，在安装搜狗拼音输入法之前，需要先行安装Fcitx，在终端窗口下直接输入：

```ruby
sudo pacman -S fcitx
```

即可完成安装，需要注意的是，仅仅安装这一项是不够的，这样在安装完成之后，Fcitx基本上是处于不可用的状态，我们还需要安装以下几个包：

```ruby
sudo pacman -S fcitx-configtool
sudo pacman -S fcitx-gtk2 fcitx-gtk3 fcitx-qt5
```

目前在Archlinux的源中，fcitx-im包组已经取消了fcitx-qt4包，但是搜狗输入法需要这个包，可以用AUR获取：

```ruby
sudo pacman -S yay
paru -S fcitx-qt4
```

#### 安装搜狗拼音

在前一步中我们已经正确的配置了源，这里直接输入：

```shell
$ sudo pacman -S fcitx-sogoupinyin
// 安装配置工具
$ sudo pacman -S fcitx-configtool
```

### 配置

安装完之后我们还不可以直接使用，还需要进行一定的配置，用文本编辑器打开~/.xprofile，没有就新建，在其末尾添加以下几行：

```bash
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```

或者直接执行

```bash
$ echo "export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx" >> ~/.xprofile
```

wiki建议使用`~/.pam_environment`设置环境变量，可以一并加上：

```bash
$ echo "GTK_IM_MODULE DEFAULT=fcitx
QT_IM_MODULE  DEFAULT=fcitx
XMODIFIERS    DEFAULT=@im=fcitx" >> ~/.pam_environment
```

然后注销后重新登录，或者重启后重新登录。

#### 可能的问题

如果遇到登录之后输入法fcitx没有启动的问题，可以将fcitx设置为自动启动，deepin桌面下右键fcitx的图片就能做到，gnome桌面可以用gnome-tweaks，也可以就简单的在.xprofile里面加一句fcitx。
或者使用wiki上给出的方式

```shell
$ cp /etc/xdg/autostart/fcitx-autostart.desktop ~/.config/autostart/
```