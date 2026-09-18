**1691范围更新：BLE仅要求版本5.4，正式测试为全部18项xTS BLE用例。与原88项去重后共105项，确认通过77项（73.3%）；新增17项先核验历史证据再补缺。LE Audio/Mesh1.1仍为专项适配要求，不自行增加全规范认证。完整清单见比赛必须适配清单.md。**

**1756离线审计：用户暂时无法人工干预期间，逐项核对主清单剩余项目；GPIO、BMI160、音频听验、Camera、SD、USB Host、BLE 对端/统计均缺实物或人工证据，文件系统速率按用户要求保留“自测完成、待验收”，Wi-Fi 低于参考按用户要求暂跳过。未刷机、未占用串口、未重复已通过项目。1757补充SD Host配置语法检查，1758修正BLE HCI采集前的存储目录准备；详见 [offline1756-no-manual-closure.md](offline1756-no-manual-closure.md)。**

**1694更新：5.1.7已在1690专用Flash工作线程镜像上完成同一原始读1000/写10用例；随机读0.58秒、随机写45.66秒，观察到`flash_io`线程，临时移出文件均已恢复并cmp一致。按社区性能口径仍记“自测完成、待验收”，不重复旧用例。**

**最新范围调整：用户已取消自添加第3项“完整演示”和第4项“RGB灯演示”的比赛必需要求，不再作为必做任务或完成门槛；历史证据保留；当前新增项已在主清单连续编号为第1～12项，其中第11项为SD卡协议、第12项为USB2.0。原88项冲刺及新增JPEG、Camera、RGB888/565、BLE 5.4/LE Audio/Mesh 1.1目标不变；当前BLE仅验证基础功能。**

# Sprint evidence handover1665

The selected milestone is77/88 acceptedPASS (common33/35, category44/53; RNG by explicit user acceptance1682). This is not full-project completion. No passed original case needs repetition merely because the result ledger was refreshed. Current category details are in sprint1682-current-cases.json; the1455 snapshot and all failures remain intact.

|Remaining item|Authoritative evidence / actual gap|Next necessary action|
|---|---|---|
|GPIO|External loopback absent|User fixture and original run|
|BMI160|Physical device measurement absent|User fixture and original run|
|FS5.1.7|1694 same original workload on1690 direct Flash worker:1000reads0.58s/10writes45.66s;`flash_io`observed; staged fixtures restored and compared;1689 prior 52.2s/1060.82s retained|Self-test complete, community performance acceptance pending; do not repeat identical workload|
|FS5.1.12 dd|SELF-TEST COMPLETE, ACCEPTANCE PENDING;1030 records|Submit existing records per user instruction; no rerun|
|FS5.1.11 performance_test|SELF-TEST COMPLETE, ACCEPTANCE PENDING;1030 records|Submit existing records per user instruction; no rerun|
|TCP Rx5.1.22|1679 candidate1676 original300s,both169MiB/4.70Mbit, PC300.62s/board300.60s; prior1659 baseline retained|Published numeric acceptance absent; do not repeat identical workload|
|TCP Tx5.1.23|1634 original300s,both56.6MiB/1.58Mbit, duration agrees|Published numeric acceptance absent|
|UDP Rx5.1.24|1662 old image:420MiB/11.7Mbit,24% loss;1696 current1676 image:620MiB/17.3Mbit,33% loss,2370 out-of-order,client final-ACK warning; full300s traffic retained|Rate/loss acceptance unresolved; not a PASS; target iperf leftovers cleaned by controlled reset|
|UDP Tx5.1.25|1673original300s complete:both125MiB/3.49Mbit,0.01%loss, finalServerReport matches; earlier1668ARP failure retained|Performance acceptance pending; proceed physical tests/demo|
|Audio4.2.15|1059 microphone confirmed byuser; external playback not heard|Speaker fixture/listening|
|Audio4.2.10|Original external-speaker playback missing|Speaker fixture/listening|
|SD card protocol|[1750 static audit](sd1750-protocol-audit.md)、[1752 NuttX boundary](sd1752-nuttx-candidate-boundary.md) and [1757 Host-init syntax candidate](sd1757-host-init-candidate.md): S31 SDK/HAL exposes two 4-bit/UHS-I slots; official board guide confirms external SDIO slot-0 signals on J2.26–31 (GPIO20–25), while the official component list does not list an onboard TF/SD socket; the slot-0 configuration candidate passes offline S31 cross-compiler syntax checking, but there is no external card, NuttX registration or card evidence; no xTS-specific SD protocol case|按 [1753 实物顺序](sd-usb1753-hardware-runbook.md)接入带 3.3 V/上拉的外接 SD 模块，桥接 SDMMC Host 到 NuttX 块设备，然后完成卡识别、读写、FAT 和掉电恢复|
|USB2.0 / xTS4.2.2|[1751 role audit](usb1751-role-audit.md), [1755 candidate](usb1755-host-register-candidate.md): official board guide defines Type-A as OTG High-Speed Host; `CONFIG_ESP32S31_USBHOST` now reuses the pinned UTMI/DWC LL for clock/PHY/core reset, host-mode preparation and VBUS request, with independent cross-compilation and S31 register offset checks, but still has no HCD, IRQ, root-hub enumeration or class-driver evidence; `xts-flat-usb-adb` remains Device/ADB BUILD ONLY|按 [1753 实物顺序](sd-usb1753-hardware-runbook.md)先确定 Host/Device 角色和 VBUS，再补齐 HCD 并接入 USB 设备记录枚举；只有真实外部主机 `adb shell` 会话才支持 xTS4.2.2|

Bluetooth1544/1551/1564 and later SIMD1566/1633/1654 evidence satisfy their recorded implementation/test scopes. Do not conflate SIMD arithmetic/context checks with a completeAI application. Additional audio integration remains deferred per1578/1579 priority correction; no new audio feature or repeat recording has been started.

No global route/proxy/firewall settings changed. Keep-awake is a host process, not protection against physical loss of power. User has resumed and prioritized UDP, physical tests, and demo. Fixture availability question is pending; do not assume any wiring is present.

RNG1.3.16 accepted by explicit user instruction1682; original undefined statistical outputs preserved, no rerun. See rng1682-user-acceptance.md.
