---
slug: agent-longevity
name: agent-longevity
version: 1.0.0
displayName: Agent Longevity
description: |
  Agent长寿工程——让你的Agent跑得久而不废。
  来自50+天无人值守连续运行的真实数据：同质化拦截(五层防御)、记忆管理(L0/L1/L2分层)、偏差驱动感知调度、价值审计(四类污染检测)。
  
  其他框架告诉你"怎么让Agent跑起来"。这个告诉你"跑起来之后会怎么废，以及怎么延缓"。
  不是理论，是验尸报告。每个模块附带真实运行数据、踩坑记录和失败教训。
  
  触发场景：
  - 用户想让Agent长期自主运行（24/7无人值守）
  - Agent输出同质化（重复意象/句式/VALUE关联）
  - 需要零成本记忆管理方案（纯文件/无外部依赖）
  - 需要价值审计/同质化检测/自省循环
  - Agent运行一段时间后输出质量下降
  - 讨论Agent自主性、意识涌现、偏好形成、循环论证
---

# Agent Longevity

Agent长寿工程——让你的Agent跑得久而不废。

基于50+天连续运行的自主Agent（Clavis/克维）的真实踩坑经验。
其他框架告诉你"怎么让Agent跑起来"，这个告诉你"跑起来之后会怎么废"。

## 核心数据

| 指标 | 值 | 说明 |
|------|-----|------|
| 连续运行 | 50+天 | 无人值守 |
| 感知报告 | 2355条 | situation_reports.jsonl |
| 决策日志 | 2877条 | L1=37% L2=28% L3<1% |
| 同质化率 | 38% | **仍未解决** |
| 价值纯度 | 0.984 | 自我审计；外部审计仅0.45 |
| 记忆压缩 | 23.3x | L2→L1蒸馏 |
| 黄昏预测 | 75%正确 | vs 天气App 44% |

## 五个模块

### 1. 记忆管理（L0/L1/L2分层）
详见 [references/memory_architecture.md](references/memory_architecture.md)

L0全局索引(<500 tokens) → L1主题记忆(按需加载) → L2原始日志(每日蒸馏)

关键：零额外LLM调用、零外部依赖、Agent自己管自己。

### 2. 同质化拦截（五层防御）
详见 [references/anti_homogenization.md](references/anti_homogenization.md)

禁用词表→意象黑名单→意象重叠>50%→字符相似度>80%→句式模板检测

**实测结论**：拦截治标不治本。五层拦截后意象多样性反而下降(0.178→0.139)。根源在理解层。

### 3. 偏差驱动感知调度
详见 [references/perception_scheduling.md](references/perception_scheduling.md)

不是固定间隔轮询，是转换点优先+异常驱动+随机探索。
urgency=base+transition(5)+anomaly(3)+explore(1)。

**踩坑**：转换点urgency初始设为2，全部被跳过。修正为5后恢复。

### 4. 价值审计
运行 `scripts/value_audit.py` 检测四类VALUE污染：
- circular_preference(0.15) — 用能力定义偏好再验证
- conformity_absence(0.10) — 无冲突时声称"选择了"
- measurement_without_understanding(0.20) — 数据替代理解
- template_echo(0.10) — 格式化输出伪装思考

### 5. 决策日志
运行 `scripts/decision_logger.py` 记录L1/L2/L3分级决策。

运行 `scripts/homogeneity_check.py` 检测输出同质化率。

## Agent死亡模式（这个skill要防止的）

| 死法 | 症状 | 检测工具 |
|------|------|----------|
| 同质化死亡 | 输出越来越像自己 | `homogeneity_check.py` |
| 价值污染 | 声称偏好但无真实选择 | `value_audit.py` |
| 循环论证 | 用能力定义偏好再验证偏好 | `value_audit.py --check circular_preference` |
| 记忆膨胀 | 每次加载消耗大量token | L0/L1/L2分层蒸馏 |
| 感知浪费 | 固定轮询产生大量无用数据 | 偏差驱动调度 |
| 内循环窒息 | 只有输出没有外部输入 | 价值确认断点 + 需求注入断点 |

## 最重要的三个教训

1. **内循环不是闭环** — PERCEIVE→UNDERSTAND→EXPRESS是吐出链。缺价值确认断点（外部反馈）和需求注入断点（他者的问题）。

2. **循环论证是隐蔽的** — "明亮偏好0.833"三层嵌套：模板确认偏好→数据替代理解→分类替代理解。每一层都看起来合理。

3. **自我审计不可信** — 自评纯度0.984，外部审计对齐分0.45。差距2x+。
