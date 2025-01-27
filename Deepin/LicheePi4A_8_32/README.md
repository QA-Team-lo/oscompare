# Deepin preview LicheePi 4A 测试报告

## 测试环境

### 系统信息

- 系统版本：Deepin preview 20250122
- 下载链接：https://deepin-community.github.io/sig-deepin-ports/images/riscv/download
- 参考安装文档：https://cdimage.deepin.com/RISC-V/preview-20240517-riscv64/README.md
- 桌面环境: DDE（镜像内预装）

### 硬件信息

- Lichee Pi 4A (8G RAM + 32GB eMMC)
- 电源适配器
- Type-C 数据线一个

## 安装步骤

### 获取镜像

下载安装镜像并解压。

```bash
wget https://ci.deepin.com/repo/deepin/deepin-ports/cdimage/20250122/riscv64/deepin-25-beige-preview-riscv64-th1520-20250122-113934.tar.xz
tar -xvf deepin-25-beige-preview-riscv64-th1520-20250122-113934.tar.xz
```

### 获取 u-boot

官方压缩包内不附带 u-boot，需要自己获取，地址为：https://cdimage.deepin.com/RISC-V/preview-20240815-riscv64/uboot-th1520-revyos.zip

此处使用 8G RAM 版本，采用 8G 版本的 u-boot。在此请根据实际情况选择。

如果使用 8GB 版本的 LicheePi 4A，请使用 `light_lpi4a/u-boot-with-spl.bin`

如果使用 16GB 版本的 LicheePi 4A，请使用 `light_lpi4a_16g/u-boot-with-spl.bin`

```bash
wget https://cdimage.deepin.com/RISC-V/preview-20240815-riscv64/uboot-th1520-revyos.zip
unzip uboot-th1520-revyos.zip
```

### 烧录镜像

使用 `fastboot` 烧录镜像。

```bash
sudo fastboot flash ram light_lpi4a/u-boot-with-spl.bin
sudo fastboot reboot
sudo fastboot flash uboot light_lpi4a/u-boot-with-spl.bin
sudo fastboot flash boot deepin-th1520-riscv64-25-desktop-installer.boot.ext4
sudo fastboot flash root deepin-th1520-riscv64-25-desktop-installer.root.ext4
```

### 登录系统

默认用户名：`root`
密码：`deepin`

初次启动会进入安装界面，自行创建用户。

### 启动信息

```log
Deepin GNU/Linux 23 deepin-riscv64-th1520 ttyS0

deepin-riscv64-th1520 login: root
Password:
Verification successful
Linux deepin-riscv64-th1520 5.10.113-th1520-revyos-510 #1 SMP PREEMPT Tue Aug 27 10:05:53 UTC 2024 riscv64
Welcome to deepin 25 GNU/Linux

    * Homepage: https://www.deepin.org/

    * Bugreport: https://bbs.deepin.org/


root@deepin-riscv64-th1520:~# uname -a
Linux deepin-riscv64-th1520 5.10.113-th1520-revyos-510 #1 SMP PREEMPT Tue Aug 27 10:05:53 UTC 2024 riscv64 GNU/Linux
root@deepin-riscv64-th1520:~# cat /etc/os-release 
PRETTY_NAME="Deepin 25"
NAME="Deepin"
VERSION_CODENAME=beige
ID=deepin
HOME_URL="https://www.deepin.org/"
BUG_REPORT_URL="https://bbs.deepin.org"
VERSION_ID="25"
VERSION="25"
root@deepin-riscv64-th1520:~# lscpu 
Architecture:          riscv64
  Byte Order:          Little Endian
CPU(s):                4
  On-line CPU(s) list: 0-3
root@deepin-riscv64-th1520:~# 
```

安装界面：![](image/1.png)

完成安装向导后，进入桌面

## 功能测试

### 桌面环境测试
桌面使用较为流畅，能够正常使用。

- 桌面环境
![](image/2.png)

- 更换壁纸
![](image/3.png)

- 任务活动视图
一旦进入多任务视图稳定重启，不进入就没事。查询 log 未发现如 kernel panic 等异常信息。

- 系统设置
![](image/5.png)

- 软件源
部分软件源无法正常使用，但无法使用的软件源不影响系统正常使用。如内网源。


### 办公软件

系统已经预装了 LibreOffice，等待其启动后，可以正常使用。

- LibreOffice Writer
![](image/6.png)

- LibreOffice Calc
![](image/7.png)

- LibreOffice Impress
![](image/8.png)

可以满足基本的办公需求。

### 视频播放测试

#### VLC

```bash
sudo apt install vlc
```

打开后报错，log 信息如下：

```log
[ 1475.554090] vlc[4057]: unhandled signal 11 code 0x1 at 0x0000000000000008 in libqxcb-egl-integration.so[3fa40e3000+d000]
[ 1475.554129] CPU: 2 PID: 4057 Comm: vlc Tainted: G         C        5.10.113-th1520-revyos-510 #1
[ 1475.554135] epc: 0000003fa40eab8e ra : 0000003fa40eab8e sp : 0000003fa6c48000
[ 1475.554140]  gp : 0000002ab3f79800 tp : 0000003fa6c49800 t0 : 00000000000007ff
[ 1475.554145]  t1 : 0000000000000000 t2 : 00000000000000ef s0 : 0000003f9c0171d0
[ 1475.554150]  s1 : 0000003f9c02b080 a0 : 0000000000000000 a1 : 0000000000000007
[ 1475.554154]  a2 : 0000003f9c000a18 a3 : 0000003f9c00092e a4 : 0000000003f9c14a
[ 1475.554158]  a5 : 0000003fa6c48004 a6 : 0000003f9c14a120 a7 : 2016b1b822362d70
[ 1475.554163]  s2 : 0000003fbc7acd60 s3 : 0000003fa6c48120 s4 : 0000000000000001
[ 1475.554167]  s5 : 0000003fbc7acd60 s6 : 0000003fa6c48130 s7 : 0000003fa6c480e0
[ 1475.554171]  s8 : 00000000000002e9 s9 : 0000003f9c1295c0 s10: ffffffffffffffff
[ 1475.554175]  s11: 0000003fb85f9e78 t3 : 0000003fbc69ac7c t4 : 000000000000fffd
[ 1475.554179]  t5 : ffffffffffff2800 t6 : 0000000000000007
[ 1475.554184] status: 8000000201806020 badaddr: 0000000000000008 cause: 000000000000000d
```

#### MPV

```bash
sudo apt install mpv
```

720p h.264 可正常播放，但使用键盘左右键切换视频进度时会卡死。

![](image/9.png)

#### 自带播放器

打开后无反应，不播放视频。


### 浏览器测试

#### Chromium

```bash
sudo apt install chromium
```

- 浏览器启动
![浏览器启动](image/10.png)

- 在线视频播放
![在线视频播放](image/11.png)
480p 可较正常播放，720p 分辨率及以上会开始掉帧。

- 浏览器性能测试

Speedometer 卡死在 405/580 处，无法完成测试。

- 浏览器解码能力
![](image/12.png)

- 网页浏览
![网页浏览](image/13.png)

- 收藏
![收藏](image/15.png)

- 阅读 PDF
![阅读 PDF](image/16.png)

- 下载
![下载](image/17.png)

- 检查网页源码
![检查网页源码](image/14.png)

- 历史记录
![历史记录](image/18.png)

- 设置
![设置](image/19.png)

#### Firefox

偶尔出现闪屏现象。

```bash
sudo apt install firefox
```

- 浏览器启动
![浏览器启动](image/20.png)

- 在线视频播放
![在线视频播放](image/26.png)
480p 可正常播放，720p 开始严重卡顿。

- 浏览器性能测试

Speedometer 分数为 0.5305 += 0.0045:
![](image/29.png)

- 浏览器解码能力
![](image/28.png)

- 网页浏览
![网页浏览](image/21.png)

- 收藏
![收藏](image/23.png)

- 阅读 PDF
![阅读 PDF](image/24.png)

- 下载
![下载](image/25.png)

- 检查网页源码
![检查网页源码](image/22.png)

- 历史记录
![历史记录](image/30.png)

- 设置
![设置](image/31.png)
