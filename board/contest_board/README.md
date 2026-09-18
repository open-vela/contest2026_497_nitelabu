# ESP32-S31 Function-CoreBoard-1 板级适配提交目录

本目录是专属仓的板级适配入口。当前 openvela 基线中的真实 ESP32-S31
板级路径位于 `nuttx/boards/risc-v/esp32s31/esp32s31-core-function-board/`；
由于官方要求公共仓改动通过公共仓 PR 提交，本目录保存复现说明、补丁索引和
不依赖实物的核验边界，不直接复制整个 openvela 工作区。

- `PATCHES.md`：公共仓补丁生成与应用说明。
- `patches/`：当前工作区生成的补丁快照。
- `tools/`：只读检查和补丁复现辅助脚本。

板上刷写、串口日志和外部 SD/USB/Camera 设备测试不在此目录伪造；对应证据
在 `docs/acceptance/` 中按“静态/编译/板上/人工”分层记录。
