# ESP32-S31 Function-CoreBoard-1 openvela 适配

## 一、作品简介

本项目面向 ESP32-S31 Function-CoreBoard-1，完成 openvela 的芯片、板级、存储、网络、音频、蓝牙和 xTS 适配工作，为后续队友复现、补测和提交验收提供统一基线。当前以 xTS 冲刺核验集为验收主线，保留每项测试的实测、开发验证和待人工核验边界。

## 二、选题方向

新硬件适配。目标是把 ESP32-S31 的 SMP/MMU、Wi-Fi、BLE、文件系统、音频、USB、SDMMC 和板级外设能力接入 openvela，并用官方 xTS 用例验证可复现结果。

## 三、仓库结构

- `board/contest_board/`：Function-CoreBoard-1 的专属提交说明、补丁索引和复现脚本。
- `board/contest_board/patches/`：针对 openvela 公共仓的可复现补丁快照。公共仓改动仍应按官方规则向对应 `dev-ai-contest-2026` 分支发起 PR。
- `docs/acceptance/`：xTS 清单、历史验收记录和当前剩余项目。
- `docs/acceptance/evidence/`：SD、USB、BLE、Camera 等新增项目的边界证据。
- `logs/`：按官方日志手册导出的 AI Coding 日志目录。没有导出的真实日志时，不使用模板示例冒充日志。

## 四、复现方式

1. 按本仓 `contest2026_497_nitelabu.xml` 使用官方 `repo init`/`repo sync` 获取同一 openvela 工作区。
2. 在 openvela 工作区根目录检查各公共仓版本与本仓补丁基线一致。
3. 根据 `board/contest_board/PATCHES.md`，将对应补丁应用到 `nuttx`、`apps`、`external` 和 `tests` 公共仓；补丁只用于复现，提交上游时仍按官方 PR 流程操作。
4. 使用 `nuttx/boards/risc-v/esp32s31/esp32s31-core-function-board/configs/` 下的目标配置编译。默认配置不启用实验性的 SDMMC Host、USB Host 或未完成的 Camera 实物路径。
5. 按 `docs/acceptance/比赛必须适配清单.md` 和 `docs/acceptance/remaining1665-no-repeat.md` 记录结果；绿色项目不要因换镜像重复测试，黄色/蓝色项目必须保留其人工或实物依赖。

## 五、当前重点边界

- xTS 原冲刺基线保持历史证据，新增 BLE 项目单独统计，不把相关能力误报为完整 xTS 通过。
- SD 卡项目目前有 slot 0 引脚/HAL 配置和 NuttX 桥接编译候选，尚未完成完整链接、外接卡识别、FAT 挂载或掉电恢复。
- USB 2.0 项目目前有 UTMI/PHY/Host 初始化候选，尚未完成 HCD、IRQ、root-hub 枚举和 class driver。
- Camera 目前只完成 OV2640 SCCB 探测源编译核验，没有 sensor 实物、DVP 捕获或帧输出证据。

完整状态以 `docs/acceptance/` 为准。

## 六、AI Coding 使用说明

开发过程遵循官方 AI Coding 日志归集手册。日志必须由官方采集器从真实会话导出到 `logs/<github_login>/` 后再提交；本仓不提交模板日志或伪造会话记录。
