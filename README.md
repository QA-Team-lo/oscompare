# oscompare

openEuler/openKylin/openAnolis/deepin 在部分 RISC-V 开发板或 QEMU 上的运行情况对比。

主要针对常见的桌面使用场景，包括但不限于：

- 浏览器
    - 在线视频播放
        - bilibili
        - YouTube
    - 性能基准测试
        - Speedometer 3.0
        - Basemark Web 3.0
- 视频播放
    - 视频硬件解码
        - mpv
        - VLC
- 办公软件
    - LibreOffice
- 桌面环境体验
    - DDE
    - GNOME
    - UKUI
    - Xfce

## 系统支持情况

| Board/OS   | Lichee Pi 4A | Milk-V Meles    | BPI-F3    | Milk-V Jupiter  | SiFive HiFive Unmatched | Milk-V Pioneer | QEMU |
|------------|--------------|-----------------|-----------|-----------------|-------------------------|----------------|------|
| openEuler  | ✅            | ❌无法启动       | ❌无法启动 | ❌无法启动       | ✅非主线支持             | ✅              | ✅    |
| openKylin  | ✅            | ❔非官方支持设备 | ✅         | ❔非官方支持设备 | ✅/❔仅 1.0               | ✅              | ❌    |
| deepin     | ✅            | ✅非官方支持设备 | ✅         | ❔               | ❌已终止支持（2022）       | ✅              | ✅    |
| openAnolis | ❌            | ❌               | ❌         | ❌               | ❌                       | ❌              | ✅    |

- ✅：有官方支持
- ❌：无支持/已放弃支持（EOL）
- ❔：暂未测试，可能有以下几种情况
    - 有同 SoC 的其他开发板支持，但未针对当前设备适配
    - 非主线支持（如 openEuler RISC-V SIG 的第三方发版）
    - 仅支持上一个版本（但未明确表示 EOL）

## License

此项目使用 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 授权。

## Credits

此仓库的测试报告由丁丑小队的以下成员完成：

- BPI-F3: @Sharelter
- LPi4A 16G + 128G: @stydxm & @panglars
- LPi4A 8G + 32G: @wychlw
- Milk-V Meles: @KevinMX
- Milk-V Pioneer: @aisuneko & @KevinMX
- QEMU: @255doesnotexist & @aisuneko
- SiFive HiFive Unmatched: @KevinMX