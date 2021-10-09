---
title: VScode~~偷懒指南~~使用技巧 #文章页面上的显示名称，可以任意修改，不会出现在URL中
date: 2020-12-10 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
categories: #文章分类目录，可以为空，注意:后面有个空格
tags: [VScode] #文章标签，可空，多标签请用格式[tag1,tag2,tag3]，注意:后面有个空格
description: vscode快捷键及各种插件
---

# vscode快捷键

## 格式化代码

全局：shift+alt+f  

选中：shift+alt+f

![img](https://pic3.zhimg.com/v2-7d752a63acab79dd2b546846e9f5fdd2_b.webp)

## 代码折叠

1. 在光标处折叠最内侧未折叠区域：

· 在Windows系统或Ubuntu系统：Ctrl键 + Shift键 + [键

· 在Mac系统：Command键+ Option键 + [键

2. 在光标处展开折叠区域：

· 在Windows系统或Ubuntu系统：Ctrl键 + Shift键 + ]键

· 在Mac系统：Command键+ Option键 + ]键

![img](https://pic2.zhimg.com/v2-a111ff823b8579f881475e9d950f5061_b.webp)

## 切换窗口
`ctrl + w` 在同时浏览的窗口中切换


# vs code整段右移或者左移

选中按TAB右移，按SHIFT+TAB左移

# 在VScode中使用c/c++开发
## 配置环境
1. 下载[MinGW]([https://www.mingw-w64.org/downloads/#mingw-builds](https://www.mingw-w64.org/downloads/#mingw-builds))
2. 设置环境变量
3. 下载[CMake]([https://cmake.org/](https://cmake.org/)),记得勾选添加环境变量
4. 在task.json和launch.json处分别加上路径
![[VScodeSkill_CppTask.json.png]]
![[VScodeSkill_CppLaunch.json.png]]
5. 配置c_cpp_properties.json
![[VScodeSkill_Cppc_cpp_properties.json1.png]]
这些路径来源为CMD输入命令`gcc -v -E -x c++ -`

![[VScodeSkill_Cppc_cpp_properties.json2.png]]

输出内容,将这些复制到c_cpp_properties.json中

![[VScodeSkill_Cppc_cpp_properties.json3.png]]



常见问题

### The term 'g++' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

管理员打开VScode再试一遍, 命令行不能执行时也需要先管理员打开一遍，执行命令

# 在VScode中使用C#开发

$\textcolor{ForestGreen}{VScode仅限于微型项目或测试  写项目还是老老实实用Visual Studio吧！}$

**环境**

- VSC本体
- .NET Core SDK，可以访问dot.net下载
- VSC扩展：C#、Code Runner

**操作步骤**

- 建立一个空文件夹
- 打开终端（TERMINAL） 输入``` dotnet new console``` 会自动生成Hello World文件
- 按F5即可运行 
- 还需要做一点修改。左边点开.vscode文件夹：
```
launch.json："console": "integratedTerminal", "internalConsoleOptions": "neverOpen";  .NET Core Attach可以删掉。
tasks.json：给build加上"group": { "kind": "build", "isDefault": true },（打group就>会自动提示）
```

如使用runner 需要设置环境变量
```
csc是编译C#的程序。安装VS，把 安装路径下\Microsoft VisualStudio
\2019\Community\MSBuild\Current\Bin\Roslyn\加到Path里。
```

**常见问题**

`'scriptcs' is not recognized as an internal or external command, operable program or batch file.`

> You need both the script runner extension and to install scripts
>
> Installation and information guide is here: http://scriptcs.net/
>
> 1. Install chocolatey
> 2. Run `cinst scriptcs` to install the latest version.

[refer](https://stackoverflow.com/questions/59261688/trouble-running-c-sharp-code-in-vs-code-getting-scriptcs-error)

`error CS7021: You cannot declare namespace in script code`

> It's complaining about the namespace, so remove it from the Program.cs

`The name 'Console' does not exist in the current context`

using System;

`Feature 'default literal' is not available in C# 8.0. Please use language version 9.0 or greater.`

> Adding
>
> ```
> <LangVersion>latest</LangVersion>
> ```
>
>  under the `<PropertyGroup>` tags
>
> in your pubxml(**.csproj) file seems to fix it.

[refer](https://stackoverflow.com/questions/47946732/c-sharp-7-1-cant-be-published/48085575#48085575)

# VS code 同步设置和扩展插件

https://www.jianshu.com/p/0a273bf2a986
vscode_plugin token ebc81cc8b0dac29cdbc8e98d5eef49094f5d7e5c
gist :e813379a55dab2b9a6d2bc13e1bbf8f0



int是带符号的，表示范围是：-2147483648到2147483648，即-2^31到2^31次方。

uint则是不带符号的，表示范围是：2^32即0到4294967295。

# code runner for vscode

**支持语言**

c c++ c# python js ts go 