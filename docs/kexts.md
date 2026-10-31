# 第三方 kext 清单

全部取自各项目官方 release，未做二进制修改（`WhateverXe.kext` 除外——那份是补丁版，
见 [fork 的 `edp-panel-handoff` 分支](https://github.com/<your-name>/WhateverXe/tree/edp-panel-handoff)）。

| # | kext | 版本 | Bundle ID | 用途 | 上游 |
| --- | --- | --- | --- | --- | --- |
| 1 | `Lilu.kext` | 1.7.3 | `as.vit9696.Lilu` | 补丁引擎（所有插件的宿主） | [acidanthera/Lilu](https://github.com/acidanthera/Lilu) |
| 2 | `AppleALC.kext` | 1.9.9 | `as.vit9696.AppleALC` | 音频（**本机未确认可用**） | [acidanthera/AppleALC](https://github.com/acidanthera/AppleALC) |
| 3 | `AMFIPass.kext` | 1.4.1 | `com.dhinakg.AMFIPass` | 免改系统卷通过 AMFI 校验 | [dhinakg/AMFIPass](https://github.com/dhinakg/AMFIPass) |
| 4 | `WhateverXe.kext` | 0.6.1 **（补丁版）** | `org.b00t0x.WhateverXe` | Iris Xe 加速 + eDP 内屏 boot handoff | [b00t0x/WhateverXe](https://github.com/b00t0x/WhateverXe) |
| 5 | `VirtualSMC.kext` | 1.3.9 | `as.vit9696.VirtualSMC` | SMC 模拟 | [acidanthera/VirtualSMC](https://github.com/acidanthera/VirtualSMC) |
| 6 | `RestrictEvents.kext` | 1.1.7 | `as.vit9696.RestrictEvents` | 屏蔽机型相关的功能限制/弹窗 | [acidanthera/RestrictEvents](https://github.com/acidanthera/RestrictEvents) |
| 7 | `CpuTopologyRebuild.kext` | 2.0.2 | `org.b00t0x.CpuTopologyRebuild` | 异构核拓扑伪装成同构（4P+8E） | [b00t0x/CpuTopologyRebuild](https://github.com/b00t0x/CpuTopologyRebuild) |
| 8 | `NVMeFix.kext` | 1.1.4 | `org.acidanthera.NVMeFix` | NVMe 电源管理与兼容性 | [acidanthera/NVMeFix](https://github.com/acidanthera/NVMeFix) |
| 9 | `XHCI-unsupported.kext` | 0.9.2 | `org.rehabman.injector.XHCI.unsupported` | 非原生 XHCI 控制器占位 | RehabMan |
| 10 | `ECEnabler.kext` | 1.0.6 | `com.1Revenger1.ECEnabler` | 读取 >8bit 的 EC 字段（电池） | [1Revenger1/ECEnabler](https://github.com/1Revenger1/ECEnabler) |
| 11 | `USBToolBox.kext` | 1.2.0 | `com.dhinakg.USBToolBox.kext` | USB 端口注入框架 | [USBToolBox/kext](https://github.com/USBToolBox/kext) |
| 12 | `UTBMap.kext` | 1.1 | `com.dhinakg.USBToolBox.map` | **本机**端口映射表 | 本机生成 |
| 13 | `BlueToolFixup.kext` | 2.7.3 | `as.acidanthera.BlueToolFixup` | 蓝牙协议栈修复 | [acidanthera/BrcmPatchRAM](https://github.com/acidanthera/BrcmPatchRAM) |
| 14 | `IntelBluetoothFirmware.kext` | 2.5.1 | `com.zxystd.IntelBluetoothFirmware` | Intel 蓝牙固件加载 | [OpenIntelWireless/IntelBluetoothFirmware](https://github.com/OpenIntelWireless/IntelBluetoothFirmware) |
| 15 | `IntelBTPatcher.kext` | 2.5.1 | `com.zxystd.IntelBTPatcher` | 同上（补丁辅助） | 同上 |
| 16 | `VoodooI2C.kext` | 2.9.1 | `com.alexandred.VoodooI2C` | I2C 触控板/触摸屏主驱动 | [VoodooI2C/VoodooI2C](https://github.com/VoodooI2C/VoodooI2C) |
| 17 | `VoodooI2CHID.kext` | 1.0 | `com.alexandred.VoodooI2CHID` | HID 协议层 | 同上 |
| 18 | `VoodooPS2Controller.kext` | 2.3.8 | `as.acidanthera.voodoo.driver.PS2Controller` | 内置键盘 / PS2 触摸板兜底 | [acidanthera/VoodooPS2](https://github.com/acidanthera/VoodooPS2) |
| 19 | `AirportItlwm.kext` | 2.4.0 | `com.zxystd.AirportItlwm` | Intel 无线网卡（原生 AirPort 接口） | [OpenIntelWireless/itlwm](https://github.com/OpenIntelWireless/itlwm) |

## 内嵌 PlugIn 的说明

`VoodooI2C.kext` 与 `VoodooPS2Controller.kext` 都自带 PlugIn，OpenCore 需要逐个在
`Kernel → Add` 里显式列出：

| 父 kext | PlugIn | 启用 |
| --- | --- | --- |
| `VoodooI2C.kext` | `VoodooI2CServices.kext` / `VoodooGPIO.kext` / `VoodooInput.kext` | ✅ 全部启用 |
| `VoodooPS2Controller.kext` | `VoodooPS2Keyboard.kext` / `VoodooPS2Mouse.kext` / `VoodooPS2Trackpad.kext` | ✅ 启用 |
| `VoodooPS2Controller.kext` | `VoodooInput.kext` | ❌ **禁用**（与 VoodooI2C 的那份冲突） |

## 尚未加入（电池，待修复）

电池检测目前不可用，缺的是两样东西，其中一样**不在**这份清单里：

| 项 | 状态 | 说明 |
| --- | --- | --- |
| `SMCBatteryManager.kext` | ❌ 未加入 | VirtualSMC 的电池插件。本 EFI 里的 `VirtualSMC.kext` 是精简运行时包，`Contents/PlugIns` 为空，所以电池驱动链根本没接上 |
| 电池 ACPI（`SSDT-BATT` 等） | ❌ 未加入 | EC 里的 16-bit 电池字段需要拆分 + `_BST`/`_BIF` 重建，详见主 README §7.1 |

`ECEnabler.kext`（#10）已在用，但它只解决「>8bit 字段读不出来」，
**不生成电池设备**，替代不了上面两项。

补齐时 `SMCBatteryManager.kext` 要排在 `VirtualSMC.kext` 之后，
不要单独放在 `Lilu` 之前。

## 许可证

- **BSD-3-Clause**：Lilu、VirtualSMC、AppleALC、RestrictEvents、NVMeFix、VoodooPS2Controller、
  BlueToolFixup、WhateverXe
- **GPL-2.1**：VoodooI2C、VoodooI2CHID
- **GPL-2.0**：AirportItlwm、IntelBluetoothFirmware、IntelBTPatcher
- 其余（AMFIPass、ECEnabler、USBToolBox、XHCI-unsupported、CpuTopologyRebuild）见各自仓库

二次分发时请保留每个 bundle 内的原始 `Info.plist` 与版权声明。
