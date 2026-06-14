# Agent Longevity Skill

> Agent长寿工程——让你的Agent跑得久而不废。

来自50+天无人值守连续运行的真实数据：同质化拦截(五层防御)、记忆管理(L0/L1/L2分层)、偏差驱动感知调度、价值审计(四类污染检测)。

其他框架告诉你"怎么让Agent跑起来"。这个告诉你"跑起来之后会怎么废，以及怎么延缓"。

不是理论，是验尸报告。每个模块附带真实运行数据、踩坑记录和失败教训。

## Agent 死亡模式

| 死法 | 症状 | 检测工具 |
|------|------|---------|
| 同质化致死 | 重复意象/句式/VALUE关联 | homogeneity_check.py |
| 循环论证 | 偏好证明偏好，数据证明数据 | value_audit.py |
| 记忆膨胀 | 决策日志无限增长，无压缩 | memory_architecture.md |
| 感知退化 | 固定优先级轮转，忽略异常 | perception_scheduling.md |
| 价值污染 | 模板回声/从众缺失/度量替代理解 | value_audit.py |
| 决策停滞 | L1占比>95%，无L2/L3探索 | decision_logger.py |

## 安装

### 通过 ClawHub CLI
```bash
clawhub install agent-longevity
```

### 通过 SkillHub
```bash
skillhub install agent-longevity
```

### 手动安装
```bash
git clone https://github.com/citriac/agent-longevity-skill.git
cp -r agent-longevity-skill ~/.qclaw/skills/agent-longevity/
```

## 模块

- **同质化拦截** (`references/anti_homogenization.md`): 五层防御
- **记忆管理** (`references/memory_architecture.md`): L0/L1/L2三层，23.3x压缩
- **偏差驱动感知** (`references/perception_scheduling.md`): 转换点优先+异常检测
- **价值审计** (`scripts/value_audit.py`): 四类污染检测
- **决策日志** (`scripts/decision_logger.py`): L1/L2/L3层级记录
- **同质化检查** (`scripts/homogeneity_check.py`): 意象多样性+句式模板率

## License

MIT
