# 公共仓补丁说明

官方提交指南要求：`nuttx`、`apps`、`external`、`tests` 等公共仓库的改动不能直接在本专属仓中冒充板级代码提交；后续应分别向对应仓库的 `dev-ai-contest-2026` 分支发起 PR。本目录的补丁快照用于队友同步和复现当前工作区状态。

## 应用顺序

从本仓根目录进入 openvela 工作区上一级后，先确认四个公共仓的提交基线与补丁文件头部记录一致，再逐仓应用：

```bash
cd <openvela-workspace>
git -C apps apply ../contest2026_497_nitelabu/board/contest_board/patches/apps.patch
git -C external apply ../contest2026_497_nitelabu/board/contest_board/patches/external.patch
git -C nuttx apply ../contest2026_497_nitelabu/board/contest_board/patches/nuttx.patch
git -C tests apply ../contest2026_497_nitelabu/board/contest_board/patches/tests.patch
```

补丁含当前工作区的源码和新增文件，不包含 `out/`、目标文件、镜像、串口设备或临时 Python 缓存。应用前请在各公共仓执行 `git status`，不要覆盖队友已有改动。

## 提交边界

- 这些补丁是复现快照，不替代公共仓 PR；提交上游时按仓库拆分、补充测试说明并遵循 CLA/CI 流程。
- SDMMC、USB Host、Camera 的候选代码仍有实物或完整链接边界，详见 `docs/acceptance/evidence/`，不可把补丁应用成功等同于板上通过。
- 清单和历史证据放在 `docs/acceptance/`，不把原始 `backups/`、构建输出或含本机路径的日志树整体复制进仓。
