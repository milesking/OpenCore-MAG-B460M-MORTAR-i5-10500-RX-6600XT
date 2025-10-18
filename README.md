# OpenCore-MAG-B460M-MORTAR-i5-10500-RX-5700XT
微星B460M 迫击炮 ，i5-10500，RX 6600XT 8G 黑苹果macos 26 Tahoe。

⚠️config.plist随机生成了三码，仅供调试仍需自行替换三码。

### 更新
- 2025/10/18 基于OpenCore 1.0.5，macOS Tahoe 26.0


### 硬件配置

|  配置|  型号|
|---|---|
|  CPU| I5 10500 |
|  主板| 微星B460M MORTAR |
|  内存|  16G x2 |
|  板载网卡|  RTL8125B|
|  网卡+蓝牙|  博通943602CS|
|  显卡|  核显UHD630+ RX 6600XT |

### Works
- 睡眠
- 独显+核显
- 蓝牙
- DP+HDMI
- USB定制
### 已知问题
- WIFI（修复 kext 已添加但未注入，影响睡眠，刚需参考[AppleBCMWLANCompanion](https://github.com/0xFireWolf/AppleBCMWLANCompanion)）
- 隔空投送+接力
- 音频

### BIOS 设置
- Settings -> 安全 -> 安全引导 -> 安全启动：关闭
- Settings -> 唤醒设置 -> USB设备从S3/S4/S5唤醒：允许
- Settings -> 唤醒设置 -> PS/2鼠标从S3/S4/S5唤醒：允许
- Settings -> 唤醒设置 -> USB键盘从S3/S4/S5唤醒：任意键
- Settings -> 高级 -> 内建显示器配置 -> 集成显卡多显示器：允许（否则核显硬件解码失效，只使用核显的可以忽略）
- Settings -> 高级 -> PCIe -> PCI子系统设置 -> Re-Size BAR Support ：禁止
- OC -> CPU 特征 -> Intel 虚拟化技术：允许
- OC -> CPU 特征 -> Intel VT-D 技术：禁止（驱动 WIFI 需开启）
- OC -> CPU 特征 -> CFG锁定：禁止

### 使用的SSDT
- SSDT-AWAC
- SSDT-EC-USBX-DESKTOP
- SSDT-MSI-B460M-Devices
- SSDT-GPRW
- SSDT-PLUG
- SSDT-PM
  
#### 说明
SSDT-AWAC、SSDT-PLUG、SSDT-EC-USBX-DESKTOP这三个为推荐添加的

SSDT-MSI-B460M-Devices，运行稳定且没有遇到以上问题，你可能不需要这个 SSDT 文件。但如果遇到设备识别、音频、USB、睡眠等问题可以添加

SSDT-GPRW修复睡眠即醒或者休眠问题，遇到问题可以添加

SSDT-PM，加载节能第五项（断电后自动重启生效，PC基本通用的补丁）

### 关于Mac序列号的问题
- 下载 OpenCore Configurator for Mac，打开 PlatformInfo -> Model Lookup | Check Coverage 右侧选择 iMac20,1 机型（生成你的唯一硬件UUID），然后 Save as (另存为) config.plist
- 在config.plist文件中找到如下代码，记录MLB、SystemSerialNumber和SystemUUID的值并记住它，更新EFI时，用你记录的值替换 /OC/config.plist 下对应的值即可
  
PS: 还可使用 Hackintool 工具（系统 -> 序列号生成器）来获取三码

```
<key>PlatformInfo</key>
<dict>
    <key>Generic</key>
    <dict>
        <key>AdviseWindows</key>
        <false/>
        <key>MLB</key>
        <string>C02047501CDPHCDAD</string>
        <key>ProcessorType</key>
        <integer>4105</integer>
        <key>ROM</key>
        <data>ESIzRFVm</data>
        <key>SpoofVendor</key>
        <true/>
        <key>SystemMemoryStatus</key>
        <string>Auto</string>
        <key>SystemProductName</key>
        <string>iMac20,1</string>
        <key>SystemSerialNumber</key>
        <string>C02DQSZFPN5T</string>
        <key>SystemUUID</key>
        <string>C567A1A9-9233-4D4D-B021-E1F38B112F33</string>
    </dict>

```


### Win+Mac双系统解决Win系统时间时差问题

在Windows下运行
```
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
```

### 设置默认启动项
在启动选择界面，先选中要启动的项，然后按键盘的 Ctrl + Enter (回车键) 进入系统，下次重启后默认就选中该项了
