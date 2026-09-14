# awesome-e7g / 我的仓库索引

> 对 [E7G](https://github.com/E7G) 公开仓库的分类、补充说明与项目脉络整理。
>
> 这里不追求把所有 fork 和一次性实验全部列出来，而是优先记录目前仍有使用价值、持续维护，或能够代表一段开发路线的项目。

**最近整理：2026-09-14**

---

## 目录

- [目前主要项目](#目前主要项目)
- [小米平板与 Linux / Droidspaces](#小米平板与-linux--droidspaces)
- [Android 增强与移动端工具](#android-增强与移动端工具)
- [课堂、学习与校园工具](#课堂学习与校园工具)
- [Classpaper 系列](#classpaper-系列)
- [OpenWrt、网络与 NAS](#openwrt网络与-nas)
- [Windows / 桌面工具](#windows--桌面工具)
- [waterctl 系列](#waterctl-系列)
- [其他项目与实验](#其他项目与实验)
- [历史说明](#历史说明)

---

## 目前主要项目

这些是当前最值得优先看的项目。

| 项目 | 方向 | 当前定位 |
| --- | --- | --- |
| [E7G/linux_latte](https://github.com/E7G/linux_latte) | 小米平板 2 / Linux 内核 | **重点维护**。基于 Linux 6.14 的 Mi Pad 2（latte）设备支持树，包含显示、触摸、Wi-Fi、蓝牙、音频、USB、传感器、摄像头等设备适配与测试工具。 |
| [E7G/xiaomi-latte-flash_tools](https://github.com/E7G/xiaomi-latte-flash_tools) | 小米平板 2 / 刷机工具 | 配套 latte Linux 的 GPT、EFI / fastboot 与系统镜像刷写工具。 |
| [E7G/Droidspaces-rootfs-KDE-builder](https://github.com/E7G/Droidspaces-rootfs-KDE-builder) | Android 上的桌面 Linux | **重点维护**。自动构建 Debian / Ubuntu / Fedora / Arch RootFS，支持 KDE、Plasma Mobile、Anland / Wayland、GPU、中文环境等；同时包含小米平板 4 专用构建路线。 |
| [E7G/BetterYAMF](https://github.com/E7G/BetterYAMF) | Android 小窗 | 面向性能和体验改良的 reYAMF 分支，重点完善 HyperOS 风格手势、小窗动画、回收机制与稳定性。 |
| [E7G/classhelper](https://github.com/E7G/classhelper) | AI 课堂助手 | ASR + LLM 课堂助手，正在继续完善语音识别、课程资源、课堂派 / 超星兼容与移动端体验。 |
| [E7G/winlator](https://github.com/E7G/winlator) | Android 运行 Windows 应用 | Winlator 分支，用于针对实际设备和游戏兼容性进行调整与测试。 |

---

## 小米平板与 Linux / Droidspaces

这是目前仓库中最主要的一条开发路线。

### 小米平板 2（latte）

#### [E7G/linux_latte](https://github.com/E7G/linux_latte)

Mi Pad 2 的 Linux 设备支持内核，目前以 **Linux 6.14** 为基础。

当前仓库已经不再只是一个“能启动”的实验内核，而是逐步向完整设备支持推进，包含：

- Intel i915 显示 / GPU
- LCD 背光
- FTSC1000 触摸屏
- 电容按键
- BCM4356 Wi-Fi / Bluetooth
- RT5659 + TFA9890 音频
- USB Host / Gadget / USB 串口调试
- 电池与充电
- IIO 传感器
- 指示灯与触摸键背光
- OV5693 前摄与 T4KA3 后摄的 AtomISP 实验支持
- CherryView VA-API 视频解码相关用户态说明
- 硬件 smoke test、恢复与辅助包

目前最不成熟的部分仍然是 **AtomISP 摄像头栈**，Suspend / Resume 后的设备恢复也仍需要持续回归测试。

#### [E7G/xiaomi-latte-flash_tools](https://github.com/E7G/xiaomi-latte-flash_tools)

Mi Pad 2 配套刷写工具，负责 GPT、boot/root 镜像以及 EFI / fastboot 相关流程。

它和 `linux_latte` 应视为一套完整的设备 Linux 方案，而不是两个孤立项目。

---

### 小米平板 4（clover / SDM660）

#### [E7G/Droidspaces-rootfs-KDE-builder](https://github.com/E7G/Droidspaces-rootfs-KDE-builder)

最初是 Droidspaces KDE RootFS 构建项目，现在已经扩展成较完整的 Android Linux 桌面实验平台。

目前包括：

- Debian 13
- Ubuntu 24.04 / 25.10 / 26.04
- Fedora 43 / 44
- Arch Linux ARM
- KDE Plasma / Plasma Mobile
- Termux:X11
- Anland / Wayland
- PulseAudio / PipeWire 兼容
- 中文环境与 Fcitx5
- Snapdragon GPU / KGSL 相关适配
- Droidspaces USB 管理
- GitHub Actions 自动构建与 Release

其中已经加入 **Mi Pad 4 专用 RootFS** 路线，包括 Ubuntu 26.04 / Arch、Plasma Mobile、Anland、KGSL、legacy ION shim，以及针对旧 4.4 内核环境的兼容处理。

相关仓库：

- [E7G/android_kernel_xiaomi_sdm660_clover_avium](https://github.com/E7G/android_kernel_xiaomi_sdm660_clover_avium)：Mi Pad 4 / SDM660 内核相关实验，当前包含 Droidspaces / ReKSU 方向分支。
- [E7G/mesa-for-android-container](https://github.com/E7G/mesa-for-android-container)：Android 容器环境中的 Mesa / Snapdragon GPU 相关工作。
- [E7G/anland](https://github.com/E7G/anland)：Anland 相关实验与修改。
- [E7G/wlroots-anland](https://github.com/E7G/wlroots-anland)：wlroots + Anland 方向实验。
- [E7G/labwc](https://github.com/E7G/labwc)：轻量 Wayland compositor 方向实验。
- [E7G/archlinuxarm-PKGBUILDs](https://github.com/E7G/archlinuxarm-PKGBUILDs)：Arch Linux ARM 软件包构建相关。
- [E7G/libva-v4l2-stateful](https://github.com/E7G/libva-v4l2-stateful)：V4L2 stateful / VA-API 相关实验。
- [E7G/avium-build](https://github.com/E7G/avium-build)：Avium / clover 构建相关辅助仓库。

---

## Android 增强与移动端工具

### [E7G/BetterYAMF](https://github.com/E7G/BetterYAMF)

基于 reYAMF 的增强分支，目标不是简单增加功能，而是让第三方小窗在实际使用中更接近系统原生体验。

目前主要改动包括：

- HyperOS 风格上滑进入小窗
- 跟手动画与边缘 handoff
- 横屏和非中心手势适配
- 减少 Overview / Recents 闪屏
- 被托管应用被杀后自动清理孤立小窗
- 小窗悬浮球图标与交互恢复
- 动态监听注册，降低无小窗时的额外开销

### [E7G/winlator](https://github.com/E7G/winlator)

Winlator 分支。主要用途是围绕 Android 平板实际运行 Windows x86/x64 程序和游戏进行兼容性、Wine / Proton、Box64 与图形栈测试。

### [E7G/c001apk-flutter](https://github.com/E7G/c001apk-flutter)

第三方酷安 Flutter 客户端分支，围绕中文界面、动态内容、图片显示和登录等功能继续修补。

### 其他 Android 相关

- [E7G/FakeDCBacklight](https://github.com/E7G/FakeDCBacklight)：屏幕背光 / 类 DC 调光方向实验。
- [E7G/ScreenshotTile-LSPosed](https://github.com/E7G/ScreenshotTile-LSPosed)：LSPosed / 系统截图快捷功能相关。
- [E7G/DouyinEasyGo-LSPosed-v1.5.20](https://github.com/E7G/DouyinEasyGo-LSPosed-v1.5.20)：抖音 LSPosed 模块相关分支。
- [E7G/douyinlowlikefilter](https://github.com/E7G/douyinlowlikefilter)：抖音内容过滤实验。

---

## 课堂、学习与校园工具

这一系列已经从早期的“网课自动化脚本”逐渐转向 **课程信息聚合 + 课堂辅助 + 本地工具链**。

### [E7G/classhelper](https://github.com/E7G/classhelper)

当前这一方向的主项目。

以 **ASR + LLM** 为核心，实现课堂实时语音识别、内容整理、问答和课程辅助，并继续加入课堂派 / 超星课程资源等功能。

目前持续处理的重点包括：

- 中文实时 ASR
- 短语音切分和课堂连续识别
- LLM 辅助理解与笔记
- 课堂派课程 / 资源浏览
- 超星资源预览兼容
- Android 平板高 DPI / 触摸界面适配

### [E7G/HomeworkInfoSync](https://github.com/E7G/HomeworkInfoSync)

多平台作业信息同步工具，目标是统一整理超星 / 学习通、课堂派、长江雨课堂等平台的作业截止时间和提交状态。

### 网课工具链

- [E7G/ocsjs-with-uxy](https://github.com/E7G/ocsjs-with-uxy)：OCS 网课助手分支，曾加入优学院支持及默认题库适配。
- [E7G/ocs-helper](https://github.com/E7G/ocs-helper)：超星学习平台辅助脚本，处理视频卡顿、自动课程导航、多级 iframe 等问题。
- [E7G/tikulocal](https://github.com/E7G/tikulocal)：本地题库服务，为脚本提供本地 API。
- [E7G/chaoxing_ulearning_Answer_to_Word](https://github.com/E7G/chaoxing_ulearning_Answer_to_Word)：将超星 / 优学院答案整理保存到 Word。
- [E7G/chaoxing-signin](https://github.com/E7G/chaoxing-signin)：超星签到相关工具。
- [E7G/ketangpai-downloader](https://github.com/E7G/ketangpai-downloader)：课堂派资源整理 / 下载工具。

### 校园环境

- [E7G/luci-app-campusportal](https://github.com/E7G/luci-app-campusportal)：将校园网认证脚本封装为 OpenWrt LuCI 应用。
- [E7G/cisco-pt-mcp](https://github.com/E7G/cisco-pt-mcp)：Cisco Packet Tracer / MCP 相关实验。

---

## Classpaper 系列

Classpaper 是较完整的一条历史项目路线：从替代 ClassBoard / ClassBoardSharp 开始，先后尝试 miniblink、Lorca、WebUI、Go、C++、Rust，最后走向原生 WinAPI / GDI 的极简实现。

### 一代：[E7G/ClassPaper](https://github.com/E7G/ClassPaper)

最初尝试复用 ClassBoardSharp 网页前端，以 miniblink + 本地程序承载。

这一阶段设计了早期的 **Classpaper 兼容层**：将原本多个本地配置文件的读取，改成由 JS 配置数据提供，从而减少网页端直接读写本地文件。

最终因为网页使用了 miniblink 不支持的新特性，方案停止。

### 二代：[E7G/Classpaper-v2](https://github.com/E7G/Classpaper-v2)

改用 Go + Lorca，借助系统 Chrome 解决网页兼容性问题。

后续通过 cgo 引入 WinAPI，使其拥有桌面层、任务栏图标处理等能力。之后又对前端与配置结构做过翻新，是整个系列中较重要的一代。

### 三代：[E7G/Classpaper-v3](https://github.com/E7G/Classpaper-v3)

使用 C++ + WebUI 重构，解决桌面穿透和浏览器承载问题，并尝试将设置界面与主显示界面解耦。

### 四代：[E7G/Classpaper-v4](https://github.com/E7G/Classpaper-v4)

Rust 实现，继续沿用兼容 v2 前端的路线，目标是进一步压缩体积并改善底层实现。

### 五代：[E7G/Classpaper-v5](https://github.com/E7G/Classpaper-v5)

Classpaper 的收官方向：不再围绕浏览器壳层继续迭代，而是直接使用 Windows API / GDI 完成核心显示。

核心追求：

- 尽量零依赖
- 极小体积
- 极低 CPU / 内存占用
- 无需复杂设置
- 托盘作为控制入口
- 回归“它只需要安静地完成自己的工作”这一设计理念

配套工具：

- [E7G/lessonlistchanger](https://github.com/E7G/lessonlistchanger)：课表制作 / 转换工具。

---

## OpenWrt、网络与 NAS

- [E7G/luci-app-campusportal](https://github.com/E7G/luci-app-campusportal)：校园网认证 LuCI 前端。
- [E7G/luci-app-adblock-lean](https://github.com/E7G/luci-app-adblock-lean)：adblock-lean 的 LuCI 管理界面。
- [E7G/OpenWrt-momo](https://github.com/E7G/OpenWrt-momo)：OpenWrt momo 相关分支 / 实验。
- [E7G/OpenWrt-nikki](https://github.com/E7G/OpenWrt-nikki)：OpenWrt Nikki 相关分支 / 实验。
- [E7G/cliproxyapi-fnos](https://github.com/E7G/cliproxyapi-fnos)：面向飞牛 OS / NAS 的 CLIProxyAPI 集成。
- [E7G/xiaoai-speaker](https://github.com/E7G/xiaoai-speaker)：小爱音箱相关控制 / TTS 实验。

---

## Windows / 桌面工具

- [E7G/wincleaner](https://github.com/E7G/wincleaner)：Rust + Freya GUI 的 Windows 清理工具，支持开发工具缓存、应用缓存、系统垃圾和自定义规则。
- [E7G/simpleRPA](https://github.com/E7G/simpleRPA)：Python RPA 自动化框架，包含录制、鼠标键盘操作、图像识别点击和循环执行等能力。
- [E7G/ShareX-RapidOCR](https://github.com/E7G/ShareX-RapidOCR)：ShareX 与 RapidOCR 结合方向的 OCR 实验。
- [E7G/MiMoCode-Desktop](https://github.com/E7G/MiMoCode-Desktop)：MiMoCode 桌面端相关项目。
- [E7G/wmpf-debugger-rust](https://github.com/E7G/wmpf-debugger-rust)：Rust 实现的调试工具实验。
- [E7G/Quickary](https://github.com/E7G/Quickary)：轻量工具类项目。

---

## waterctl 系列

> **历史项目。** 原方案受水控器固件 / 服务变化影响，已经不再作为当前主线维护。

起因是水控器约 7 分钟断连，需要频繁重新操作。最初基于 [celesWuff/waterctl](https://github.com/celesWuff/waterctl) 做自动连接和自动重连，后来尝试了多个技术栈。

主要仓库：

- [E7G/waterctl_auto](https://github.com/E7G/waterctl_auto)：系列基础分支。
- [E7G/Waterctl_Electron](https://github.com/E7G/Waterctl_Electron)：Electron 版本。
- [E7G/Waterctl_Tauri](https://github.com/E7G/Waterctl_Tauri)：Tauri 版本。
- [E7G/waterctlgo](https://github.com/E7G/waterctlgo)：Go 方向实验。
- [E7G/waterctlrn](https://github.com/E7G/waterctlrn)：React Native 版本，也是后期实际使用方案的重要组成部分。

当时最终使用过的组合是：

**二手红米 3 + 防水袋 + waterctlrn + MacroDroid + shell + 巴法云 / 米家联动**。

它已经完成了当时的实际需求，因此现在更适合作为一段完整项目历史保留。

---

## 其他项目与实验

这里列出一些值得保留入口，但目前不适合单独发展成大章节的公开仓库。

### 媒体 / 内容

- [E7G/PiliNara](https://github.com/E7G/PiliNara)
- [E7G/media-kit](https://github.com/E7G/media-kit)
- [E7G/MKOnlineMusicPlayer](https://github.com/E7G/MKOnlineMusicPlayer)
- [E7G/kuwo_flac_decrypt](https://github.com/E7G/kuwo_flac_decrypt)
- [E7G/my-iptv](https://github.com/E7G/my-iptv)

### Web / 开发实验

- [E7G/interactive-image-map](https://github.com/E7G/interactive-image-map)
- [E7G/appmaker](https://github.com/E7G/appmaker)
- [E7G/cptr_toolkits](https://github.com/E7G/cptr_toolkits)
- [E7G/esp32c3-things](https://github.com/E7G/esp32c3-things)
- [E7G/ts2c](https://github.com/E7G/ts2c)
- [E7G/pylib](https://github.com/E7G/pylib)

### 历史镜像 / fork / 资料保存

- [E7G/Some-collected-surface-rt-information-files](https://github.com/E7G/Some-collected-surface-rt-information-files)
- [E7G/Google-Mirrors](https://github.com/E7G/Google-Mirrors)
- [E7G/pandownload.com_Pages_Backup](https://github.com/E7G/pandownload.com_Pages_Backup)
- [E7G/pandownload-fake-server](https://github.com/E7G/pandownload-fake-server)
- [E7G/baidupan-rapidupload](https://github.com/E7G/baidupan-rapidupload)
- [E7G/baiduwp-php](https://github.com/E7G/baiduwp-php)

---

## 历史说明

这个账号里的仓库跨度较大，大致经历过以下几类方向：

1. **网页、资源站与脚本**：早期的 Web / 网盘 / 镜像类项目。
2. **Classpaper**：围绕班级桌面信息展示，从 Web 壳层一路做到 WinAPI / GDI。
3. **waterctl**：为真实生活问题制作的一整套自动化水控方案。
4. **网课 / 校园自动化**：从 OCS、题库和作业同步逐渐发展到 `classhelper`。
5. **系统与设备折腾**：OpenWrt、Android、LSPosed、Droidspaces。
6. **当前重点——旧设备 Linux 化与移动桌面 Linux**：Mi Pad 2 `linux_latte`、Mi Pad 4 / Droidspaces / Anland / Wayland 相关工作。

因此，这个仓库现在更适合作为 **项目地图（project map）**，而不是单纯的仓库列表。

如果某个项目已经有自己的完整 README，这里只保留定位和项目之间的关系，具体安装、构建、已知问题和使用方法以对应仓库为准。
