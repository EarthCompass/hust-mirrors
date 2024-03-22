---
title: Raspbian 软件仓库镜像使用帮助
sidebar_label: raspbian
cname: raspbian
slug: /raspbian
upstream: raspbian
upstream_sha256: 11817d0e3e89c5d0d5a45783ec9664c2f3857e456852ba92a97e67cc653ae65f
mirrorz: true
---
:::tip 该文档来自MirrorZ Help
本文档于*2024年2月22日*自动生成，[点击查看原文](https://help.mirrors.cernet.edu.cn/raspbian)。  
其中可能存在失效链接或其他问题，如遇到问题请及时[反馈](https://gitee.com/dzm91_hust/hust-mirrors/issues)。
:::


### Raspbian 简介

Raspbian 是专门用于 ARM 卡片式计算机 Raspberry Pi® “树莓派”的操作系统，
其基于 Debian 开发，针对 Raspberry Pi 硬件优化。

Raspbian 并非由树莓派的开发与维护机构 The Raspberry Pi Foundation
“树莓派基金会”官方支持。其维护者是一群 Raspberry Pi 硬件和 Debian 项目的爱好者。

注：Raspbian 系统由于从诞生开始就基于（为了 armhf，也必须基于）当时还是
testing 版本的 7.0/wheezy，所以 Raspbian 不倾向于使用 stable/testing
表示版本。

### 使用说明

首先通过 `uname -m` 确定你使用的系统的架构。

编辑镜像站后，请使用`sudo apt-get update`命令，更新软件源列表，同时检查您的编辑是否正确。

#### armv7l

```properties varcode title="/etc/apt/sources.list"
[ ] (a) { 0:Debian 11 (bullseye), 1:Debian 10 (buster), 2:Debian 9 (stretch) } 选择你的 Raspbian 对应的 Debian 版本
[ ] (b) { 0:否, 1:是 } 启用源码镜像
[ ] (c) { 0:否, 1:是 } 启用 multi-arch aarch64
---
let release_name = ""
let enable_source = ""
let enable_aarch64 = ""
if(a === "0") { release_name = "bullseye"; }
if(a === "1") { release_name = "buster"; }
if(a === "2") { release_name = "stretch"; }
if(b === "0") { enable_source = "# "; }
if(b === "1") { enable_source = ""; }
if(c === "0") { enable_aarch64 = "# "; }
if(c === "1") { enable_aarch64 = ""; }
---
deb ${_http}://${_domain}/raspbian/raspbian/ ${release_name} main non-free contrib rpi
${enable_source}deb-src ${_http}://${_domain}/raspbian/raspbian/ ${release_name} main non-free contrib rpi

${enable_aarch64}deb [arch=arm64] ${_http}://${_domain}/raspbian/multiarch/ ${release_name} main
```

注意：网址末尾的`raspbian`重复两次是必须的。因为 Raspbian 的仓库中除了 APT 软件源还包含其他代码。APT 软件源不在仓库的根目录，而在`raspbian/`子目录下。

#### aarch64

aarch64 用户可直接参考 [Debian 帮助](/docs/debian/)

#### raspberry 镜像

对于两个架构，编辑 `/etc/apt/sources.list.d/raspi.list` 文件，这需要查看 [Raspberrypi 帮助](/docs/raspberrypi/)。


### 相关链接

#### Raspbian 链接

*  Raspbian 主页：[https://www.raspbian.org](https://www.raspbian.org)
*  文档：[https://www.raspbian.org/RaspbianDocumentation](https://www.raspbian.org/RaspbianDocumentation)
*  Bug 反馈：[https://www.raspbian.org/RaspbianBugs](https://www.raspbian.org/RaspbianBugs)
*  镜像列表: [https://www.raspbian.org/RaspbianMirrors](https://www.raspbian.org/RaspbianMirrors)

#### 树莓派链接

* 树莓派基金会主页：[https://www.raspberrypi.org/](https://www.raspberrypi.org/)
* 树莓派基金会论坛 Raspberry Pi OS 版块：[https://raspberrypi.org/forums/viewforum.php?f=66](https://raspberrypi.org/forums/viewforum.php?f=66)

### 关于本文档

本文档内容的原始版本由 Raspberry Pi
中文社区“树莓爱好者论坛”提供。按照 [知识共享署名 - 非商业性使用
3.0
中国大陆许可协议](http://creativecommons.org/licenses/by-nc/3.0/cn/) 授权清华大学镜像站使用。

TUNA 提供的修改版本同样使用 [知识共享署名 - 非商业性使用
3.0
中国大陆许可协议](http://creativecommons.org/licenses/by-nc/3.0/cn/)。