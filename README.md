### 关于我的仓库的一些分类和补充

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

- [E7G/Classpaper-v2](https://github.com/E7G/Classpaper-v2/tree/old)：version 2 of my work Classpaper

在一代失败后，我决定潜心解决网页兼容问题，最终选定 [zserge/lorca](https://github.com/zserge/lorca) 作为 miniblink 的替代，其通过调用系统自带的 chrome 浏览器，实现了网页的兼容，且体积较小，于是我开始使用 go 对 classpaper 进行重新实现。

> 再次失败：go 缺乏桌面穿透的库实现，纯 go 无法实现桌面穿透，于是再次失败。

### 三代

- [E7G/Classpaper-v3](https://github.com/E7G/Classpaper-v3)：仿照 v2 的思路使用 c++ 重构

为了解决二代留下的无法实现桌面穿透的问题，我采用了 c++ 对二代进行了重新实现，使用 [webui-dev/webui](https://github.com/webui-dev/webui) 来替代 lorca，二者功能差不多，只要浏览器支持 kiosk 模式等功能就行。

> 遇到问题：浏览器虽然实现了桌面穿透，但是任务栏图标并没有隐藏，导致网页显示端容易被误删。通过查阅资料，我调用 winapi 解决了这一问题，但其容易复发，需要用多线程实现任务栏图标的循环删除，而当时的 c++ 并未找到合适的多线程实现库，于是我需要另想办法。

### 回头

由于二代采用的 go 语言具有原生多线程支持的优势，于是我使用 cgo 移植了三代中桌面穿透及任务栏图标删除部分的代码，实现了具有完整功能的 classpaper，并最终稳定使用。

### 相关工具

- [E7G/lessonlistchanger](https://github.com/E7G/lessonlistchanger)：课表制作/课表转换器
- [Classpaper-v2/reflash_wallpaperlist.vbs at 2](https://github.com/E7G/Classpaper-v2/blob/2/reflash_wallpaperlist.vbs)：壁纸列表自动刷新脚本
- [Classpaper-v2/setting.exe at 2](https://github.com/E7G/Classpaper-v2/blob/2/setting.exe)：从一代中提取并完善的适配 classpaper 兼容层的设置程序

### 翻新

应 [Candlest](https://github.com/Candlest) 制作新版 [ClassBoardSharp](https://github.com/Candlest/ClassBoardSharp) 的邀请和个人对功能未完全实现的遗憾的补偿，我对 classpaper 进行了翻新，使其更加完善，拥有更好的设置界面，以及更多的自定义选项。

#### 改良后的classpaper兼容层

在新版的 classpaper 中，我对兼容层进行了改良，把分散的多个配置文件合并为一个 `config.js` 文件，使其看起来不那么凌乱，同时使用内置的js代码对旧的配置格式做了兼容，并保留了可以直接浏览器调试的特性。

> 可读性降低，配置可自定义程度提高。

#### 更改程序配置文件格式

由原来的ini改为toml。

> 使用起来几乎无变化。

### 改良后的classpaper-v2

根据改良后的新前端，我更新了旧的 [E7G/Classpaper-v2](https://github.com/E7G/Classpaper-v2/tree/clean)，并对其进行了一些改进，实现了新的网页版的设置界面，对触摸屏更友好，功能更完善，纯go实现，体积更小，适配win24h2,更多功能请自行体验。

### 四代

- [E7G/Classpaper-v4](https://github.com/E7G/Classpaper-v4)：version 4 of my work classpaper , using rust

根据新版的v2使用rust重新实现，使用alcro库作为lorca库的替代实现，编译后体积更小，兼容v2的前端文件，可无缝迁移。

### 改良后的三代

- [E7G/Classpaper-v3](https://github.com/E7G/Classpaper-v3)：version 3 of my work classpaper , using c++ and webui

通过webui多开窗口实现了网页版设置兼容，设置与主界面相对独立，耦合度更低，兼容v2上的功能，支持更多浏览器，但相对的不兼容v2的前端文件，需要微调，未经完整测试。

### 五代

- [Classpaper-v5](https://github.com/E7G/Classpaper-v5)：一次对极致性能和空间占用的追求

<details open>
<summary>💡 点击切换显示模式（简洁版/美化版）</summary>

<div align="left">

## 🎨 美化版

> **极致的终点** - [Classpaper-v5](https://github.com/E7G/Classpaper-v5)

---

> 一次对极致性能和空间占用的追求

**反思**

前几代都是作为classboard的后端底层的替代，延续了classboard的一些我认为并不太好的设计，而2、3、4代只是对底层的换语言换方案实现。

也许，我们并不需要一个硕大的浏览器为我们渲染界面，我们也无需考虑跨平台，而winapi的依赖已然引入，为什么不对其加以更多的利用？

**理念**

我需要一个极致的东西：

- 不需要其他花里胡哨的我用不到的功能，全都可以忽略掉，去掉
- 只需要它在那里运作着，默默地提供它的功能，起着它的作用
- 它无需耀眼，无需宣传，它本身足够好，完成了它应尽的责任
- 在我们不需要它的时候它也会悄然消失，就像它不曾存在过一样，像风一般逝去，仅此而已

---

**实现**

> 就这样了，我就这样做了

- **图形渲染**：依赖win自带的gdi实现图形窗口的绘制
- **零依赖**：完全不依赖其他的库，只使用windows提供的api
- **极致轻巧**：一个极小的程序

**性能数据**

```
体积:     40+ KB
CPU:      < 1%
内存:     < 1.5 MB
磁盘写入: 0.1 MB (稳定)
```

<div align="center">

![Classpaper-v5 实际运行效果](screenshots/v5.png)

*40KB的极致：零依赖、零闪烁、零设置*

</div>

**特性**

- ✨ 无闪烁
- ⚙️ 无设置
- 🗂️ 托盘便是控制中心
- 🔍 查找式实现json的解析
- 📦 无依赖，实则轻巧

---

**收官**

就这样吧，作为classpaper的收官之作，为其画上了完美的句号。

实现了其立项以来的我所有的想法：

- 极致的轻巧，而不笨拙
- 优美的界面
- 极高的可定制性（暂未完成）

虽然还不稳定，但正如其classpaper的实际含义：

> **all about a class，light like a paper, and draw like a paper.**

</div>

</details>

---

<details closed>
<summary>📄 原始版</summary>

![Classpaper-v5 实际运行效果](screenshots/v5.png)

*40KB的极致：零依赖、零闪烁、零设置*

仔细想想，前几代都是作为classboard的后端底层的替代，延续了classboard的一些我认为并不太好的设计，而2、3、4代只是对底层的换语言换方案实现，也许，我们并不需要一个硕大的浏览器为我们渲染界面，我们也无需考虑跨平台，而winapi的依赖已然引入，为什么不对其加以更多的利用，我需要一个极致的东西，不需要其他花里胡哨的我用不到的功能，全都可以忽略掉，去掉，我只需要它在那里运作着，默默地提供它的功能，起着它的作用，它无需耀眼，无需宣传，它本身足够好，完成了它应尽的责任，在我们不需要它的时候它也会悄然消失，就像它不曾存在过一样，像风一般逝去，仅此而已。

也许吧，就这样了，我就这样做了，它依赖win自带的gdi实现图形窗口的绘制，完全不依赖其他的库，只使用windows提供的api，一个极小的程序，体积只有40多kb，cpu占用不超1%，内存占用不到1.5mb，磁盘写入稳定0.1mb，无闪烁，无设置，托盘便是控制中心，查找式实现json的解析，不稳定，实则极致，无依赖，实则轻巧。就这样吧，作为classpaper的收官之作，为其画上了完美的句号，实现了其立项以来的我所有的想法，极致的轻巧，而不笨拙，优美的界面，极高的可定制性（暂未完成），虽然还不稳定，但正如其classpaper的实际含义，all about a class，light like a paper, and draw like a paper.

</details>

---

## 其他

暂无
