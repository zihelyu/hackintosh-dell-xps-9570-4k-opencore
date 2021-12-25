# XPS15-9570-Monterey

### 2021-12-25
1. 更新`OpenCore`至0.7.6； Update `OpenCore` to 0.7.6
2. 更新所有`内核扩展`到最新版 Update All `Kernel Extensions` to the latest version;
3. 支持Monterry 12.0.1


## 配置

- CPU：Intel I7 8750H
- 内存：16G(8G\*2) 2666MHz DDR4
- 硬盘：海力士 NVMe 512G
- WIFI 网卡：已更换为博通 DW1560
- 屏幕分辨率：4K 触控屏

## 特性

- CPU: I7-8750H，已启用原生电源管理；多档变频正常。
- 声卡: ALC298, 注入 ID：32，声音正常。耳机切换采用 ALCPluginFix。
- 触摸板: 使用`VoodooI2C`,支持 Mac 原生手势，缺点就是没有防误触。
- 触摸屏: 感觉实际用到次数不多，已使用SSDT禁用。
- WIFI: 原配 Killer 1535 无法驱动，更换 DW1560。
- 蓝牙: 驱动正常，极少数情况下会设备丢失，handoff 也正常。
- ACPI： 使用 hotpatch 进行热修复，亮度快捷键映射正常。
- USB: USB3 端口均正常使用。
- 雷电3: 无法热插拔使用，已使用SSDT禁用。
- 显卡：集显 HD630 注入`3E9B0000`正常驱动；独显 GTX 1050Ti 无解。
- 读卡器：驱动正常。
- DRM：可以播放，但TV应用中DRM硬解目前WEG的进度来看仍旧需要独显，不能完美支持

## 当前问题
1. HDMI2.0接口无法工作，因为我没有显示器可供测试，但是注入缓冲帧后应该可以正常驱动。
2. 3.5mm耳机唤醒后可能无声，因为我只有Airpods Pro，没有有线耳机可供测试，但使用AL298PlugFix应该可以解决。

## 提示

1. 不要开启`文件保险箱加密(FileValue)`，不要开启`文件保险箱加密(FileValue)`，不要开启`文件保险箱加密(FileValue)`！！！
2. 使用OC前，请务必保证你已经解锁了`CFGlock`!如果你没有解锁`CFGLock`，则必须修改配置中`AppleXcpmCfgLock`以及`IgnoreInvalidFlexRatio`两项为`True`否则将启动失败。

## 其他配置（1080P）说明
如果你是1080P用户，请注意以下几点：
1. （非必须）使用[xzhih/one-key-hidpi](https://github.com/xzhih/one-key-hidpi)项目提供的方式开启HiDPI；
2. 使用`ProperTree`或者`OpenCore Configurator`修改`OC\Config.plist`中`NVRAM\4D1EDE05-38C7-4A6A-9CC6-4BCCA8B38C14`部分`UIScale`值设置为`1`或用`其他文本编辑器（如记事本等）`修改`UIScale`部分如下：

```
<key>4D1EDE05-38C7-4A6A-9CC6-4BCCA8B38C14</key>
<dict>
	<key>UIScale</key>
	<data>AQ==</data>
</dict>
```

## 小问题处理方式

#### 1. 字体细、发虚

终端执行`defaults write -g CGFontRenderingFontSmoothingDisabled -bool NO`，注销再登录即可

#### 2. 安卓 USB 网络共享

下载`HoRNDIS.kext`放入`OC/kexts/`中，并使用文本编辑器在`Kernel/Add`项下添加以下内容。
```
<dict>
	<key>BundlePath</key>
	<string>HoRNDIS.kext</string>
	<key>Comment</key>
	<string>Android Hotpot</string>
	<key>Enabled</key>
	<true/>
	<key>ExecutablePath</key>
	<string>Contents/MacOS/HoRNDIS</string>
	<key>MaxKernel</key>
	<string></string>
	<key>MinKernel</key>
	<string></string>
	<key>PlistPath</key>
	<string>Contents/Info.plist</string>
</dict>
```

## 贡献者
[zihelyu](https://github.com/zihelyu)

## 鸣谢

[RehabMan](https://github.com/RehabMan)、[Acidanthera](https://github.com/acidanthera)、[PMheart](https://github.com/PMheart)、[alexandred](https://github.com/alexandred)等

注：排名不分先后；如有遗漏，请勿见怪，感谢您的付出；
