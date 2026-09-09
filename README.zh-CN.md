# Context-First

> 让 Coding Agent 在存量项目中更快产出正确改动。

`Context-First Agent Workflows` 是一套与具体工具无关的 Skill 包和方法论，目标是提高 Coding Agent 在存量项目中的**正确改动交付速度**（time-to-correct-change）。

Coding Agent 通常不慢在生成代码，而是慢在生成**正确改动之前**。在写代码前，它需要支付一笔**上下文税**（Context Tax）：找到需求所属的业务模块、追踪当前生效的主链路、排除相似但无关的实现，并确定必须如何验证。

Context-First 通过三层机制降低这笔上下文税：

1. **结构**：用 `app + modules + tools` 让业务上下文局部化；
2. **导航**：用精炼的 `PROJECT-MAP.md` 降低进入陌生仓库时的冷启动成本；
3. **执行**：由人作目标与取舍决策，AI 在最小真实上下文中完成最小、可验证的正确改动。

目标不是让模型吐出 token 更快，而是让 Agent 读取**更少无关代码**、减少无关改动和返工回合，并更快到达能提供真实证据的验证环境。

## 三层模型

```text
用户目标
  -> PROJECT-MAP.md 选择源码入口和业务模块
  -> app + modules + tools 确定局部代码边界
  -> 最小上下文执行产生最小正确改动
  -> 真实环境验证为下一轮修复提供证据
```

| 层次 | 对应产物 | 提速目标 |
| --- | --- | --- |
| 结构层 | `skills/ai-friendly-refactor/` | 通过业务上下文局部化，降低长期代码检索成本。 |
| 导航层 | `skills/project-map/` | 缩短 Agent 初次找到相关文件前的冷启动时间。 |
| 执行层 | `skills/context-first-code/` | 在找到上下文后，减少无关改动与返工回合。 |

## 快速开始

1. 将 `skills/` 中的目录复制到你的 Coding Agent 所使用的 Skill 目录。对于兼容 Claude Code 的项目：

```bash
mkdir -p .claude/skills
cp -R skills/* .claude/skills/
```

2. 显式要求 Agent 调用 `project-map` 创建 `PROJECT-MAP.md`。例如：

```text
使用 project-map 为当前仓库生成一份精炼的 PROJECT-MAP.md。
```

该 Skill 会执行最小导航扫描并写入地图。`templates/PROJECT-MAP.md` 只用于你希望手工起草或维护地图时。

3. 将生成的地图作为项目任务的首轮导航上下文；只有模块、入口或核心链路等高价值导航事实变化时，才再次调用 `project-map` 增量更新。

4. 当仓库需要模块迁移、目录治理或跨文件重构时，调用 `ai-friendly-refactor`。它会先分析、给出迁移计划，并在得到明确批准后才编辑实现文件。

详见 [Skill 说明](skills/README.md)、[落地指南](docs/adoption.md) 和[脱敏示例](examples/task-management-web/README.md)。

## 不是要做什么

- 不替代测试、代码评审或真实环境验证；
- 不要求所有项目使用相同源码根路径或相同模块内部目录；
- 不建立泛化的 `shared/`、`common/`、`utils/` 目录；
- 不要求 AI 在没有人类决策的情况下自主重设计系统。

## 仓库结构

```text
skills/       可安装的 Agent 工作流
templates/    可直接复制的模板
docs/         方法论文与落地指南
examples/     脱敏的前后对照材料
benchmarks/   案例研究与报告协议
```

## 讨论与证据

本项目的设计主张应被案例与数据检验，而不是停留在目录命名偏好。建议记录：首次找到相关文件的时间、首轮读取文件数、从需求到正确改动所需的时间（须说明任务与环境限制）、用户澄清与返工轮次、变更文件数、遗漏依赖导致的验证失败，以及维护者与 Agent 的定性反馈。

请在 GitHub Discussions 讨论方法与反例，在 Issues 提交具体问题或兼容性诉求。参见[案例协议](benchmarks/task-protocol.md)，以不暴露私有代码的方式发表可比较案例。

## 文档

- [三层方法论](docs/methodology.md)
- [AI 友好代码组织](docs/ai-friendly-code-organization.md)
- [项目地图与代码心智模型](docs/project-map-and-ai-codebase-mental-model.md)
- [最小上下文的人机协同执行](docs/minimal-context-human-ai-coding.md)
- [落地指南](docs/adoption.md)

## 许可证

采用 [Apache License 2.0](LICENSE)。
