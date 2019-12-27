---
title: mac 配置
top: true
cover: false
comment: true
tags:
  - 配置
date: 2019-07-23 16:19:46
img:
coverImg:
summary:
password:
categories: mac
---

### 初始化配置
1. 可安装任何来源的软件 `sudo spctl --master-disable`

2. Launchpad 图标默认排，苹果自带应用显示在第一屏，自己安装应用显示在第二屏
  `defaults write com.apple.dock ResetLaunchPad -bool true; killall Dock`

3. Launchpad 每行每列展示数量设置

  1. 每行数量设置`defaults write com.apple.dock springboard-columns -int 7`  

  2. 每列数量设置`defaults write com.apple.dock springboard-rows -int 7`  

  3. 修改后需要重启 Launchpad

    `defaults write com.apple.dock ResetLaunchPad -bool TRUE;killall Dock`

  4. 重置 Launchpad

     ```shell
     defaults write com.apple.dock springboard-rows Default
     defaults write com.apple.dock springboard-columns Default
     defaults write com.apple.dock ResetLaunchPad -bool TRUE
     killall Dock
     ```

     

4. Mac Dock栏自动显示和隐藏没有延迟：
    - 设置无延迟`defaults write com.apple.Dock autohide-delay -float 0 && killall Dock`
    - 恢复`defaults delete com.apple.Dock autohide-delay && killall Dock`

### 软件
#### Homebrew
包管理工具，官方称之为The missing package manager for OS X.
官网：https://brew.sh

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

