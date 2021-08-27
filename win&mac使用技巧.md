---
title: Win和Mac~~偷懒技巧~~使用指南 #文章页面上的显示名称，可以任意修改，不会出现在URL中
date: 2020-12-20 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
categories: #文章分类目录，可以为空，注意:后面有个空格
tags: [Win,Mac,系统] #文章标签，可空，多标签请用格式[tag1,tag2,tag3]，注意:后面有个空格
description: win10 和 Macos快捷方式
---



# Win

## 如何快速格式化硬盘 `Win`

1. 打开cmd
2. 输入diskpart
3.  <img src="https://i.loli.net/2020/12/31/DLGR69srZchzKTI.png" alt="image.png" style="zoom:50%;" />

## PowerToys使用指南
- 1. spotlight：```Alt+space```
- 2. Windows 快捷键说明：```长按Windows键3秒```


# Mac



## 显示隐藏文件
### 快捷键

cmd+shift+.

### 命令行

//显示隐藏文件
defaults write com.apple.finder AppleShowAllFiles -bool true
//不显示隐藏文件
defaults write com.apple.finder AppleShowAllFiles -bool false

需要重启Finder：窗口左上角的苹果标志-->强制退出-->Finder-->重新启动

## 显示文件路径
使用终端命令行显示完整路径
```
defaults write com.apple.finder _FXShowPosixPathInTitle -bool TRUE;killall Finder
```
隐藏完整路径
```
defaults delete com.apple.finder _FXShowPosixPathInTitle;killall Finder
```

## 程序坞放大效果

程序坞设置 勾选放大

## 键盘映射

键盘->修饰键  option和command互换

## 触发角

系统偏好设定——> Mission Control——> 触发脚...——> 在右下角选择“桌面” ——> 搞定。

## 删除

cmd+del

## 系统任务管理器

cmd+option+esc

## 关闭当前程序所有进程

cmd+q

## 关闭当前程序当前页

cmd+w

## 最小化当前程序

cmd+m

## 截图 自定义

option+a

## 访达复制路径

cmd+option+c

## chrome

## 标签页 后退 前进

双指左滑。双指右滑

## 标签页选择

cmd+option+方向左右键

## 关闭当前标签页

cmd+w

## 定位到搜索栏

/

## 删除光标左边字符

cmd+del

## typora

## 源代码模式

cmd+/