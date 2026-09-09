# Context-First Agent Workflows

> 先帮助 Coding Agent 找到正确上下文，再让它修改代码。

这是一个面向存量项目的、与具体工具无关的 AI Coding Agent 工作流与 Skill 包。它将 AI 提效拆为三个相互配合的问题：

1. **结构**：用 `app + modules + tools` 让业务代码具备可预测的归属；
2. **导航**：用精炼的 `PROJECT-MAP.md` 降低 AI 进入陌生仓库时的冷启动成本；
3. **执行**：由人作目标与取舍决策，AI 在最小真实上下文中完成最小正确改动。

目标不是让 AI 更快读完整个仓库，而是让它读取**更少的无关代码**、产生更小的变更面，并将验证交给能提供真实证据的环境。

## 三层模型

```text
用户目标
  -> PROJECT-MAP.md 选择源码入口和业务模块
  -> app + modules + tools 确定局部代码边界
  -> 最小上下文执行产生最小正确改动
  -> 真实环境验证为下一轮修复提供证据
```

| 层次 | 对应产物 | 解决的问题 |
| --- | --- | --- |
| 结构层 | `skills/ai-friendly-refactor/` | 业务请求的代码应如何局部化？ |
| 导航层 | `skills/project-map/` | AI 初次进入陌生项目时应从哪里开始阅读？ |
| 执行层 | `skills/context-first-code/` | 人与 AI 如何划分决策、执行和验证？ |

## 快速开始

1. 将 `skills/` 中的目录复制到你的 Coding Agent 所使用的 Skill 目录。对于兼容 Claude Code 的项目：

```bash
mkdir -p .claude/skills
cp -R skills/* .claude/skills/
```

2. 从模板创建项目地图：

```bash
cp templates/PROJECT-MAP.md ./PROJECT-MAP.md
```

3. 显式要求 Agent 创建或增量更新项目地图；之后将地图作为项目任务的首轮导航上下文。

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

本项目的设计主张应被案例与数据检验，而不是停留在目录命名偏好。建议记录：首次找到相关文件的时间、首轮读取文件数、用户澄清轮次、变更文件数、遗漏依赖导致的验证失败，以及维护者与 Agent 的定性反馈。

请在 GitHub Discussions 讨论方法与反例，在 Issues 提交具体问题或兼容性诉求。参见[案例协议](benchmarks/task-protocol.md)，以不暴露私有代码的方式发表可比较案例。

## 文档

- [三层方法论](docs/methodology.md)
- [AI 友好代码组织](docs/ai-friendly-code-organization.md)
- [项目地图与代码心智模型](docs/project-map-and-ai-codebase-mental-model.md)
- [最小上下文的人机协同执行](docs/minimal-context-human-ai-coding.md)
- [落地指南](docs/adoption.md)

## 许可证

采用 [Apache License 2.0](LICENSE)。
