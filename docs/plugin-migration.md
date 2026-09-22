# NewsFlow 源码迁移

2026-09-22，核心与 AstrBot 适配层已合并为完整插件 2.0，新的唯一维护与分发仓库为：

[Miraco33/astrbot_plugin_newsflow](https://github.com/Miraco33/astrbot_plugin_newsflow)

旧的 Shuyuxu211 仓库地址会重定向至当前账户；插件元数据和 Git 远端已使用规范地址。本仓库没有被删除或执行 GitHub 归档，只保留原源码、历史和迁移前回退材料，不再双边维护业务实现。

## 目录对应

| 原核心位置 | 完整插件位置 |
| --- | --- |
| `src/collector`、`src/filter`、`src/storage`、`src/newsletter`、`src/notifier`、`src/config` | `core/` 下同名目录 |
| `src/cli`、`src/scheduler`、`src/web` | `standalone/` 下同名目录 |
| 独立 `main.py` | `python -m astrbot_plugin_newsflow.standalone` |
| AstrBot 适配层 `main.py`、`bridge/`、`pages/` | 保持插件入口与页面结构，增加 `rendering/` 和后台任务管理 |

所有运行模块以插件命名空间导入，不再注入 `src`、`bridge` 或外部源码路径。配置、原生产数据库、推送目标和 Cron 身份保持不变；HTML 输出改到插件数据目录。独立运行能力保留但生产不启用，避免第二套数据库和调度器。

## 更新与边界

在插件控制台「系统」先点击「准备更新」，等待任务结束，再通过 AstrBot 的仓库源更新。代码更新后只重载插件，系统依赖或镜像变更仍另行维护；首次从旧模块结构迁移已做受控重启。

GitHub 推送不会自动更新生产，仓库源下载默认分支源码。原 `/NewsFlow` 挂载暂留回退，后续容器维护再移除。

候选已通过 48 项云端测试、实际模块清理验证及中文本地渲染检查。没有重跑 AI 流水线或发送测试消息；真实内容效果与客户端送达仍按后续定时运行验收。

源码基线、迁入文件哈希与详细审计见新仓库的 `docs/migration-source.json` 和 `docs/migration-2.0.md`。当前本机唯一源码目录为 `F:/AstrBot/data/plugins/astrbot_plugin_newsflow`。
