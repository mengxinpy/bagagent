# 📱 旧机助理 项目架构草案

## 📘 README（v1草稿）

---

# 🧠 什么是 旧机助理？

**旧机助理** 是一个将废旧手机等低功耗设备变成各种小工具的平台。
旧手机设备的性能对于我们日常使用可能已经非常吃力，但是对于一些边缘的子设备，其性能就是降维打击。

你是否有一两台吃灰的旧手机？旧机助理 能将它们变为你书包里的私人数字助手（Agent），提供：

* 📤 短信与通知转发
* 🔁 文件同步与备份（支持主设备与云端）
* 🎮 远程控制与指令执行（控屏、ADB）
* 🔧 常用小工具合集
* 🌐 网络加密代理、无线热点、安全隧道
* 🧪 安全沙箱，用于运行不可信的网络任务
* 🎵 音乐解析计算器（计划中）
* 游戏掌机

这一切都可用 **0 成本**实现 —— 只需安装我们的应用。

此外，旧机助理 还是一个开放的生态平台，专注于解决手机厂商的权限限制和系统调度优化难题，为开发者社区提供稳定可靠的底层基础设施，使旧手机真正成为适合边缘计算的硬件节点，让更多创新应用能够基于这个平台蓬勃发展。

---

# 🎯 我们要解决什么问题？

旧手机的设备和现有的手机设备的区别，我们的主要功能是做主设备的拓展、备份。

如果一个功能很简单，但是主设备可以做，那么我们是不需要开发的。但是如果一个功能即使很复杂，比如NAS和云盘功能，更加适合放在副设备上做，那么我们就还是要开发这个，而且把这个作为我们主要的开放方向。

另外我们更多的是想做一个平台和范式，让其他的旧手机利用的工具都按这个标准来提供服务：

- 我们的平台提供这些工具后台管理和防止被系统清理的统一管理以及系统资源和电量的监控，不用每个开发者独立的开发工具，做不同的后台管理和防杀
- 我们的规范要求不刷入新系统，就使用目前的系统直接安装APK，我们的APK负责和手机厂商battle权限，然后在我们的APK上面建立插件市场，鼓励大家开发

## 🆚 相比于独立功能模块的优势

- 比如短信转发器专注于短信转发、消息转发等
- Alist专注于NAS Web Server管理不同的云盘等等

我们专注于旧手机利用这个场景，比如将其放在书包里、家里、电脑桌面、工位的时候，可以用旧手机实现什么功能。我们的插件将这些前辈已经非常丰富的功能整合起来，让手机使用者不需要和各种技术细节battle，只需要选择自己需要的功能和插件就可以了。

一个旧手机的价格大概是100-500元左右，但是如果只是为了一个单一的功能来折腾这个的话，对于很多功能来说，都是一些爱好者的尝试，即使有一些开源的软件，折腾起来这些软件也是很费时费力的。所以我想，我们能不能开发一个开源项目，做一个专门的旧手机的助理，这个APP作为对旧手机废物利用的专门的工具。其他的人直接像应用市场直接下载这些工具，省下来折腾的时间，这样才能真正的变废为宝。

**旧机助理 提供一个全新的答案：**

以书包场景为例，废旧的手机设备可以做为一个agent：

> 📦 把旧手机放进书包，加上一个大充电宝，你就拥有了一个持续在线、低功耗、安全自治的随身计算节点。
>
> 🏠 同时接上电源之后还可以直接放在家里和桌面，配合我们提供的云服务，随时远程访问这个agent，提供本地的云盘功能。

---

# 🧩 当前功能模块（v0.1 MVP）


| 功能                 | 描述                                                                             | 状态                |
| ---------------------- | ---------------------------------------------------------------------------------- | --------------------- |
| 📤 短信和消息转发    | 使用 SmsForwarder 接管短信并通过 Telegram/HTTP 转发                              | ✅ 可用（推荐配置） |
| 🔁 文件同步          | 使用 Syncthing 在主设备与旧机之间同步目录                                        | ✅ 可用             |
| 💾 NAS 存储          | 提供网络附加存储服务，支持文件分享、媒体流、远程备份等功能                       | ✅ 可用             |
| 🎮 控屏与输入        | 使用 scrcpy + adb 实现主控手机远程访问，让手机变成完美虚拟机                     | ✅ 手动可用         |
| ⏰ Time Machine 服务 | 为Mac设备提供时间机器备份服务（SMB协议）                                         | ✅ 可用             |
| 📊 系统监控管理      | 所有模块运行状态监控、设备状态管理（电量/温度/连接）、常住后台保活、电池优化管理 | ⏳ 开发中           |
| 🔒 模块权限管理      | 控制哪些模块启用/关闭，统一权限中心                                              | ⏳ 规划中           |

**未来将支持：**

* 🌐 VPN/代理/网络加密
* 📡 蓝牙桥接、网络广播
* 🧪 沙箱任务自动执行器
* 🎛️ 其他的一些小工具，比如遥控、手柄、和时钟等等小功能，并开放工具市场

---

# 🛠 快速开始：一分钟部署

1. 取出一部 Android 手机（推荐 Android 8+）
2. 安装旧机助理APP，并设置为被控制端，授予APP相应的权限
3. 用充电宝或充电器持续供电，将手机放入书包
4. 下载同样下载旧机助理并设置为主设备端（支持安卓、Mac、Windows），访问控制界面，选择需要的插件即可
5. 如果是在局域网下可以达到更高的速度，如果是在广域网下网速更慢，连接更不稳定

**更多配置：**

* 📦 [docs/starter-configs/] 提供一键导入的配置文件
* 💻 控制台和调试脚本将陆续开放

---

# 🧠 项目愿景（旧机助理 是什么 + 为什么现在）

旧机助理 不只是一个工具，它是：

* 💡 一种数字生活的新结构（"个人计算的副心脏"）
* 🔄 旧设备的再激活路径（对抗硬件浪费）
* 🔐 一个自主、低功耗、可控的微计算生态
* 🌍 人-设备-网络三层结构中的"移动边缘节点"

📚 详细理念见：[docs/vision.md](./docs/vision.md)

---

# 🔭 路线图（Roadmap）


| 阶段 | 目标                                          |
| ------ | ----------------------------------------------- |
| v0.1 | MVP 初版上线，SMS + 文件同步 + 控屏集成启动器 |
| v0.2 | 简洁前端 UI，模块管理器，设备监控面板         |
| v0.3 | 网络功能模块（VPN/热点/代理）、插件机制       |
| v0.4 | 云同步、远程运维支持，模块商城雏形            |

---

# 🤝 如何参与？

* 🌱 使用旧设备部署，反馈问题
* 🧠 提功能建议（Issue 或 Discussions）
* 🔧 提交新模块（Termux 脚本、安卓插件）
* ✍️ 帮助撰写/翻译文档，绘图、UI 设计

📬 **联系方式：**

* Telegram 群组（Coming Soon）
* GitHub Discussions（开放后公布）

---

# 📦 项目结构（预设）

```
旧机助理（GitHub 项目名）
├── 由 旧机助理 团队开源维护
├── 致力于将废弃智能手机变为个人 Agent 节点
├── 主项目名：旧机助理
│   ├── 模块1：短信转发器
│   ├── 模块2：文件同步器
│   ├── 模块3：控制界面（未来）
│   └── ...
├── 部署场景：
│   ├── 🎒 旧机助理-Go（适用于书包随身部署）
│   ├── 🏠 HomeAgent（适用于家用 NAS 和监控器）
│   └── 💻 TableAgent（适用于桌面的工作台等场景、定时备份等场景）
```

---

# 🧭 状态声明

旧机助理 正处于启动阶段，预计 **2025年秋季** 形成初版闭环。现在是参与构建最好的时机。

欢迎关注、使用、分享、提出想法，一起构建属于个人的数字副心脏。

---

> 🛠️ powered by edge-thinking, DIY culture, and the right to compute on your own terms.
