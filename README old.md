# 关于我的仓库的一些分类和补充

也可以作为 awsome-e7g 使用

//目录

### waterctl_auto系列



起因

因为热水器7分钟自动断连停热水的问题，我需要每7分钟要重新操作一次手机，这是我感到十分不爽，由此，我在网上查找到了这个waterctl项目，由此基于此项目实现了这个系列的作品。

本系列基本上都是基于[celesWuff/waterctl: 深圳市常工电子“蓝牙水控器”控制程序的开源实现。适用于国内各大高校宿舍热水器。](https://github.com/celesWuff/waterctl)修改而产生的仓库[E7G/waterctl\_auto: 深圳市常工电子“蓝牙水控器”控制程序的开源实现。适用于国内各大高校宿舍热水器。尝试加入7分钟自动续杯的相关代码](https://github.com/E7G/waterctl_auto)的分支的独立衍生作品。按时间先后顺序排列：

#### [E7G/Waterctl\_Electron: 深圳市常工电子“蓝牙水控器”控制程序的开源实现。适用于国内各大高校宿舍热水器。 使用 vite-plugin-electron进行功能增强，可以自动连接指定水控器，自动重连，解决7分钟断一次的问题。](https://github.com/E7G/Waterctl_Electron)

#### [E7G/Waterctl\_Tauri: 深圳市常工电子“蓝牙水控器”控制程序的开源实现。适用于国内各大高校宿舍热水器。 使用 tauri 进行功能增强，可以自动连接指定水控器，自动重连，解决7分钟断一次的问题。](https://github.com/E7G/Waterctl_Tauri)

#### [E7G/waterctlrn: react native build of waterctl, like waterctlTauri](https://github.com/E7G/waterctlrn)



Final：最终我个人采用的方案是

硬件方面：二手的红米3手机+防水手机袋+microusb数据线+插头 ，

软件：waterctlrn+macrodroid(执行sh，实现接入巴法云，从而接入米家)

实现了较稳定的热水供应


### 网课助手系列



起因

为了方便我上网课，由此诞生


由

#### [E7G/ocsjs-with-uxy: OCS 网课助手，在原脚本基础上加入对优学院自动答题的初步支持（只测试过判断题），此外还对默认设置进行了更改，默认设置了tikuadapter为搜题来源，详情请看readme](https://github.com/E7G/ocsjs-with-uxy)

搭配Tampermonkey作为网页端支持，

#### [E7G/tikulocal: 一个简易的本地题库程序，为一些脚本提供本地的题库api替代。](https://github.com/E7G/tikulocal)

代替

#### [NUnzOSz/tikuAdapter: 大学生网课题库接口适配器：将不同的题库整合为一个API接口。](https://github.com/NUnzOSz/tikuAdapter)

作为本地后端支持。

答案导入来自

#### [E7G/chaoxing\_ulearning\_Answer\_to\_Word: 超星优学院答案保存为word](https://github.com/E7G/chaoxing_ulearning_Answer_to_Word)

，形成了完整的工具链。


### Classpaper及其相关系列



起因

班内引进了[Candlest/ClassBoard: Class Board是一款使用Qt/C++开发的，针对SEEWO及其教学一体机设计的，用于显示教学信息的壁纸软件。](https://github.com/Candlest/ClassBoard)，其侧栏存在一些bug，迭代为[Candlest/ClassBoardSharp: 一款高自由度的，用于显示教学信息的壁纸软件，功能包括高考倒计时、公告栏、以及能够提示当前课程的课程表。](https://github.com/Candlest/ClassBoardSharp)后，由于其未能正确置为桌面壁纸层，导致的遮挡桌面应用图标问题频发，暂未有很好的修补方案，且其软件体积膨胀巨大。我决定自制一个软件作为替代，classpaper系列由此应运而生。


一代

#### [E7G/ClassPaper: v1成品备份](https://github.com/E7G/ClassPaper)

在一代中，我决定复用[Candlest/ClassBoardSharp: 一款高自由度的，用于显示教学信息的壁纸软件，功能包括高考倒计时、公告栏、以及能够提示当前课程的课程表。](https://github.com/Candlest/ClassBoardSharp)的网页部分代码，使用与其相同的 网页+本地软件支持显示 的方式实现，采用了 体积较小的miniblink+无需搭建编译环境的易语言 实现。

为了让[Candlest/ClassBoardSharp: 一款高自由度的，用于显示教学信息的壁纸软件，功能包括高考倒计时、公告栏、以及能够提示当前课程的课程表。](https://github.com/Candlest/ClassBoardSharp)的网页部分解耦合，我提出了classpaper兼容层概念。

##### classpaper兼容层

[Candlest/ClassBoardSharp: 一款高自由度的，用于显示教学信息的壁纸软件，功能包括高考倒计时、公告栏、以及能够提示当前课程的课程表。](https://github.com/Candlest/ClassBoardSharp)的网页端依赖其提供的api来读取本地储存的课表等文件，但我认为让网页端拥有读取本地文件的能力是一种不安全的行为，且认为并没有这种必要。于是，我使用单js文件储值来替代读取本地文件的功能，并修改index.html使其能读取js文件中包含的值。对文件内容的修改则改为对js内容的修改，由此我制作了一个设置程序，使用户习惯无缝迁徙。这种将文件的文本重定向为单js文件存储的值的功能的实现称为**classpaper兼容层**。

失败

由于[Candlest/ClassBoardSharp: 一款高自由度的，用于显示教学信息的壁纸软件，功能包括高考倒计时、公告栏、以及能够提示当前课程的课程表。](https://github.com/Candlest/ClassBoardSharp)的网页端使用了miniblink并不支持的浏览器新特性，导致网页未能在一代的界面上正确渲染，重写网页端的工程巨大，最后导致失败。


二代

#### [E7G/Classpaper-v2: version 2 of my work Classpaper](https://github.com/E7G/Classpaper-v2)

在一代失败后， 我决定潜心解决一代的网页兼容问题，经过多轮技术尝试，我最终选定了[zserge/lorca: Build cross-platform modern desktop apps in Go + HTML5](https://github.com/zserge/lorca)作为miniblink的替代，其通过调用系统自带的chrome浏览器，实现了网页的兼容，且体积较小，于是，我开始使用go对classpaper进行重新实现。

再次失败

go缺乏桌面穿透的库实现，纯go无法实现桌面穿透，于是再次失败。


三代

#### [E7G/Classpaper-v3: 仿照v2的思路使用c++重构](https://github.com/E7G/Classpaper-v3)

为了解决二代留下的无法实现桌面穿透的问题，我采用了c++对二代进行了重新实现，使用[webui-dev/webui: Use any web browser or WebView as GUI, with your preferred language in the backend and modern web technologies in the frontend, all in a lightweight portable library.](https://github.com/webui-dev/webui)来替代[zserge/lorca: Build cross-platform modern desktop apps in Go + HTML5](https://github.com/zserge/lorca)，二者功能差不多，但是通过修改后lorca可以指定调用的浏览器，而webui默认调用系统默认浏览器，但没有太大的差别，只要浏览器支持kiosk模式等功能就行。

遇到问题

浏览器虽然实现了桌面穿透，但是任务栏图标并没有隐藏，导致网页显示端容易被误删，所以要实现任务栏图标的删除才行，通过查阅资料，我调用winapi解决了这一问题，但其容易复发，需要用多线程实现其的任务栏图标的循环删除，而当时的c++并未找到合适的多线程实现的库，于是我需要另想办法。


回头

由于二代采用的go语言具有原生多线程支持的优势，于是我使用cgo移植了三代中桌面穿透及任务栏图标删除部分的代码，实现了具有完整功能的classpaper，并最终稳定使用。


相关工具

#### [E7G/lessonlistchanger: 课表制作](https://github.com/E7G/lessonlistchanger)

课表转换器

#### [Classpaper-v2/reflash\_wallpaperlist.vbs at 2 · E7G/Classpaper-v2](https://github.com/E7G/Classpaper-v2/blob/2/reflash_wallpaperlist.vbs)

壁纸列表自动刷新脚本

#### [Classpaper-v2/setting.exe at 2 · E7G/Classpaper-v2](https://github.com/E7G/Classpaper-v2/blob/2/setting.exe)

从一代中提取并完善的适配classpaper兼容层的设置程序


### 其他

暂无
