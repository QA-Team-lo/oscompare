# openKylin 2.0 Jupiter 测试报告

## 测试环境

### 系统信息

- 系统版本：openKylin 2.0-SP1
- 下载链接：[https://www.openkylin.top/downloads/index-cn.html](https://www.openkylin.top/downloads/index-cn.html)
- 参考安装文档：[https://docs.openkylin.top/zh/01_%E5%AE%89%E8%A3%85%E5%8D%87%E7%BA%A7%E6%8C%87%E5%8D%97/%E5%9C%A8riscv%E4%B8%8A%E5%AE%89%E8%A3%85/%E5%9C%A8LicheePi4A%E4%B8%8A%E5%AE%89%E8%A3%85openKylin](https://docs.openkylin.top/zh/01_%E5%AE%89%E8%A3%85%E5%8D%87%E7%BA%A7%E6%8C%87%E5%8D%97/%E5%9C%A8riscv%E4%B8%8A%E5%AE%89%E8%A3%85/%E5%9C%A8LicheePi4A%E4%B8%8A%E5%AE%89%E8%A3%85openKylin)

### 硬件信息

- Milk-V Jupiter (M1, 16GB RAM)
- DC 12V 电源适配器，或 ATX 电源
- USB to UART 调试器一个（本次使用 CH343P）
- microSD 卡一张（本次使用 SanDisk Extreme Pro 64GB）

## 安装步骤

### 刷写镜像

将镜像刷入 microSD 中。

```bash
tar -xvf openKylin-Embedded-V2.0-SP1-spacemit-k1-riscv64.img.tar.xz
sudo dd if=openKylin-Embedded-V2.0-SP1-spacemit-k1-riscv64.img of=/dev/sda bs=4M status=progress
```

Windows 用户可使用 `Rufus`。

### 登录系统

通过串口登录系统。

默认用户名： `openkylin`
默认密码： `openkylin`

### 启动信息

启动失败。屏幕录像如下。

出现类似 bootloop 的情况，多次 bootloop 后自动进入 initramfs shell。

未能成功挂载 rootfs。

[![asciicast](https://asciinema.org/a/CzVNtF5admSUNFr177hLNFYTr.svg)](https://asciinema.org/a/CzVNtF5admSUNFr177hLNFYTr)