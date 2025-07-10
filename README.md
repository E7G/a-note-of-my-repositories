# 关于我的仓库的一些分类和补充

> 也可以作为 **awesome-e7g** 使用

---

## 目录

- [waterctl_auto 系列](#waterctl_auto-系列)
- [网课助手系列](#网课助手系列)
- [Classpaper 及其相关系列](#classpaper及其相关系列)
- [其他](#其他)

---

## waterctl_auto 系列

### 起因

因为热水器 7 分钟自动断连停热水的问题，我需要每 7 分钟重新操作一次手机，这让我感到十分不爽。由此，我在网上查找到了 waterctl 项目，并基于此项目实现了本系列的作品。

本系列基本上都是基于 [celesWuff/waterctl](https://github.com/celesWuff/waterctl) 修改而产生的仓库 [E7G/waterctl_auto](https://github.com/E7G/waterctl_auto) 的分支的独立衍生作品。按时间先后顺序排列：

- [E7G/Waterctl_Electron](https://github.com/E7G/Waterctl_Electron)：使用 vite-plugin-electron 进行功能增强，可以自动连接指定水控器，自动重连，解决 7 分钟断一次的问题。
- [E7G/Waterctl_Tauri](https://github.com/E7G/Waterctl_Tauri)：使用 tauri 进行功能增强，可以自动连接指定水控器，自动重连，解决 7 分钟断一次的问题。
- [E7G/waterctlrn](https://github.com/E7G/waterctlrn)：react native build of waterctl, like waterctlTauri

#### Final：最终方案

- **硬件**：二手红米 3 手机 + 防水手机袋 + microusb 数据线 + 插头
- **软件**：waterctlrn + macrodroid（执行 sh，实现接入巴法云，从而接入米家）

实现了较稳定的热水供应。

---

## 网课助手系列

### 起因

为了方便我上网课，由此诞生。

- [E7G/ocsjs-with-uxy](https://github.com/E7G/ocsjs-with-uxy)：OCS 网课助手，在原脚本基础上加入对优学院自动答题的初步支持（只测试过判断题），此外还对默认设置进行了更改，默认设置了 tikuadapter 为搜题来源，详情请看 readme。
  - 搭配 Tampermonkey 作为网页端支持。
- [E7G/tikulocal](https://github.com/E7G/tikulocal)：一个简易的本地题库程序，为一些脚本提供本地的题库 api 替代。
  - 代替 [NUnzOSz/tikuAdapter](https://github.com/NUnzOSz/tikuAdapter)：大学生网课题库接口适配器：将不同的题库整合为一个 API 接口。
- 答案导入来自 [E7G/chaoxing_ulearning_Answer_to_Word](https://github.com/E7G/chaoxing_ulearning_Answer_to_Word)：超星优学院答案保存为 word

形成了完整的工具链。

---

## Classpaper 及其相关系列

### 起因

班内引进了 [Candlest/ClassBoard](https://github.com/Candlest/ClassBoard)，其侧栏存在一些 bug，迭代为 [Candlest/ClassBoardSharp](https://github.com/Candlest/ClassBoardSharp) 后，由于其未能正确置为桌面壁纸层，导致遮挡桌面应用图标问题频发，暂未有很好的修补方案，且软件体积膨胀巨大。我决定自制一个软件作为替代，classpaper 系列由此应运而生。

### 一代

- [E7G/ClassPaper](https://github.com/E7G/ClassPaper)：v1 成品备份

在一代中，我决定复用 ClassBoardSharp 的网页部分代码，采用网页 + 本地软件支持显示的方式实现，使用体积较小的 miniblink + 无需搭建编译环境的易语言实现。

#### classpaper 兼容层

ClassBoardSharp 的网页端依赖其提供的 api 来读取本地储存的课表等文件，但我认为让网页端拥有读取本地文件的能力是一种不安全的行为，且并没有这种必要。于是，我使用单 js 文件储值来替代读取本地文件的功能，并修改 index.html 使其能读取 js 文件中包含的值。对文件内容的修改则改为对 js 内容的修改，由此我制作了一个设置程序，使用户习惯无缝迁徙。这种将文件的文本重定向为单 js 文件存储的值的功能的实现称为 **classpaper 兼容层**。

> 失败：由于 ClassBoardSharp 的网页端使用了 miniblink 并不支持的浏览器新特性，导致网页未能在一代的界面上正确渲染，重写网页端的工程巨大，最后导致失败。

### 二代

- [E7G/Classpaper-v2](https://github.com/E7G/Classpaper-v2)：version 2 of my work Classpaper

在一代失败后，我决定潜心解决网页兼容问题，最终选定 [zserge/lorca](https://github.com/zserge/lorca) 作为 miniblink 的替代，其通过调用系统自带的 chrome 浏览器，实现了网页的兼容，且体积较小，于是我开始使用 go 对 classpaper 进行重新实现。

> 再次失败：go 缺乏桌面穿透的库实现，纯 go 无法实现桌面穿透，于是再次失败。

### 三代

- [E7G/Classpaper-v3](https://github.com/E7G/Classpaper-v3)：仿照 v2 的思路使用 c++ 重构

为了解决二代留下的无法实现桌面穿透的问题，我采用了 c++ 对二代进行了重新实现，使用 [webui-dev/webui](https://github.com/webui-dev/webui) 来替代 lorca，二者功能差不多，只要浏览器支持 kiosk 模式等功能就行。

> 遇到问题：浏览器虽然实现了桌面穿透，但是任务栏图标并没有隐藏，导致网页显示端容易被误删。通过查阅资料，我调用 winapi 解决了这一问题，但其容易复发，需要用多线程实现任务栏图标的循环删除，而当时的 c++ 并未找到合适的多线程实现库，于是我需要另想办法。

#### 回头

由于二代采用的 go 语言具有原生多线程支持的优势，于是我使用 cgo 移植了三代中桌面穿透及任务栏图标删除部分的代码，实现了具有完整功能的 classpaper，并最终稳定使用。

### 相关工具

- [E7G/lessonlistchanger](https://github.com/E7G/lessonlistchanger)：课表制作/课表转换器
- [Classpaper-v2/reflash_wallpaperlist.vbs at 2](https://github.com/E7G/Classpaper-v2/blob/2/reflash_wallpaperlist.vbs)：壁纸列表自动刷新脚本
- [Classpaper-v2/setting.exe at 2](https://github.com/E7G/Classpaper-v2/blob/2/setting.exe)：从一代中提取并完善的适配 classpaper 兼容层的设置程序

---

## 其他

暂无
