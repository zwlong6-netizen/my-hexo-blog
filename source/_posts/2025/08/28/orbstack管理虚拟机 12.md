---
title: orbstack管理虚拟机
description: orbstack相对于docker的优势？如何管理虚拟机呢？
date: 2025-08-28 22:57:23
updated: 2025-08-28 22:58:29
tags:
  - 虚拟机
  - ubuntu
  - linux
categories: orbstack
keywords:
top_img:
cover: http://www.98qy.com/sjbz/api.php?r=28225723
---
- orbstack运行虚拟机原理1111111112223
    
    OrbStack 的内核并不是独立的 Linux 内核，而是基于 **macOS 的 Virtualization Framework**，通过共享 macOS 宿主操作系统的内核来运行 Linux 虚拟机和 Docker 容器。以下是详细说明：
    
    - **核心机制**：OrbStack 利用 macOS 的 Virtualization Framework（自 macOS Big Sur 引入）创建轻量级虚拟机。它通过共享 macOS 内核运行 Linux 用户空间（user space），类似于 Windows 的 WSL（Windows Subsystem for Linux）。这意味着 OrbStack 不需要模拟完整的 Linux 内核，从而大幅减少资源占用。
    - **Docker 容器的内核支持**：对于 Docker 容器，OrbStack 在其虚拟机中运行一个精简的 Linux 环境（如 Ubuntu 或其他发行版）。这些容器共享虚拟机内的 Linux 用户空间，但底层仍然依赖 macOS 内核通过 Virtualization Framework 提供的虚拟化支持，而非独立的 Linux 内核。
    - **与传统虚拟化的区别**：相比 Docker Desktop（使用 HyperKit 或 QEMU 运行完整的 Linux 内核），OrbStack 的内核共享机制使其启动更快（2-3 秒）、内存占用更低（空闲时约 2GB），且磁盘占用极小（初始不到 10MB）。
    - **Apple Silicon 兼容性**：在 Apple Silicon（M1/M2 等）设备上，OrbStack 通过 macOS 的 Rosetta 技术支持 x86 架构的容器和虚拟机，进一步优化跨架构兼容性，但内核仍然是 macOS 内核。
    
    总结：OrbStack 的内核是 **macOS 宿主内核**，通过 Virtualization Framework 提供虚拟化支持，运行精简的 Linux 用户空间以支持虚拟机和 Docker 容器，而非独立的 Linux 内核或 Docker 内核。
    

## -1. orb启动/停止docker

```bash
 orb start/stop docker
```

## 0. 启动/停止orbstack(docker内核也会随着启停)

```bash
orb start
orb stop
orbctl start
orbctl stop
```

## 1. ubuntu设置用户密码

```bash
# ubuntu设置用户密码
passwd <username>
```

## 2. orb创建虚拟机

```bash
orb create ubuntu:24.04
# 指定用户名（默认当前用户）
orb create -u ubuntu
# 指定密码（回车后输入用户密码， sudo 时需要输入指定的密码，默是空密码）
orb create -p ubuntu:24.04
```

## 3. 启动/停止/重启虚拟机

```bash
# 启动/停止/重启虚拟机
orb start/stop/restart 虚拟机名称/ID
# 启动所有虚拟机和容器
orb start/stop/restart --all
```

## 4.进入虚拟机

```bash
# 进入虚拟机
# 进入默认虚拟机
orb
ssh orb
# 进入指定虚拟机
ssh 虚拟机名称/ID@orb
# 使用指定用户名进入指定虚拟机
ssh root@虚拟机名称/ID@orb
```

## 5. 设置默认虚拟机

```bash
# 设置默认虚拟机
orb default ubuntu
# 查看默认虚拟机
orb default
```

## 6. 删除虚拟机

```bash
# 删除虚拟机
orb delete ubuntu
# 删除所有虚拟机
orb delete --all
```

## 7. 重命名虚拟机

```bash
# 重命名虚拟机。ubuntu 是虚拟机名；my-ubuntu 是新虚拟机名
orb rename ubuntu my-ubuntu
```

## 8. 虚拟机列表

```bash
# 虚拟机列表
orb list
```

## 9. 虚拟机信息

```bash
# 虚拟机信息
orb info 虚拟机名称/ID

# 虚拟机日志
orb logs 虚拟机名称/ID
```

## 10. 文件传输命令，这里就不说了 之后再说