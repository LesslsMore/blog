### This application failed to start because it could not find or load the Qt platform plugin "windows"，Qt环境变量
将
`D:\Qt\Qt5.14.2\5.14.2\mingw73_64\plugins`
路径下的 platforms 整个文件夹放置在相应的build debug/release 文件夹下

但其实这是一种治标不治本的方法，真实原因是 Qt 没有加入系统环境变量。
将一下路径加入path
`D:\Qt\Qt5.14.2\Tools\QtCreator\bin`

这里其实其实涉及到exe安装的问题，大多数软件其实直接复制其安装后路径中所有文件即可使用，有些需要配置系统环境变量，更改注册表。
由于以上特性，建议即使在有固态硬盘的现在，分少部分空间（100G）为C盘，做系统。另外空间（D盘），装软件。这样遇到系统问题可以很便捷的重装系统，而不需要重新装软件。（之前我重装时，大多软件均可修复成功，除了office套件）
这大概是windows具有良好的软件无需安装即可使用的绿化特性。
鉴于此，用一个高速type C的移动固态硬盘，作win to go系统，这样系统环境文件都可随身携带，可以解决多电脑文件同步的繁琐问题。