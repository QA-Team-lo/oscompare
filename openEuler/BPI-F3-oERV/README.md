# openEuler/oERV SIG BPI-F3 版本测试报告

TL;DR: 未能启动。

## 测试环境

### 操作系统信息

- 系统版本：openEuler RISC-V 20241231
- 下载链接：https://mirror.iscas.ac.cn/openeuler-sig-riscv/openEuler-RISC-V/testing/20241231/v0.5/k1/
- 参考安装文档：https://docs.banana-pi.org/en/BPI-F3/GettingStarted_BPI-F3

### 硬件信息

- BPI-F3 (4G RAM + 16GB eMMC)
- 电源适配器
- USB to UART 调试器一个

## 安装步骤

### 刷写镜像

使用 dd 工具将镜像刷入储存卡中。

```bash
tar -xvf openEuler-Mega24.03SP1-V1-xfce-k1-testing.img.zst
sudo dd if=openEuler-Mega24.03SP1-V1-xfce-k1-testing.img of=/dev/sda bs=4M status=progress
```

### 登录系统

通过串口或图形界面登录系统。

默认用户名：`root` 或 `openeuler`
默认密码：`openEuler12#$`

## 预期结果

系统正常启动，能够通过串口登录，HDMI 正常输出，能够登录进桌面。

## 实际结果

插入存储卡，对开发板上电后串口无输出，HDMI 无输出，无法进入系统。