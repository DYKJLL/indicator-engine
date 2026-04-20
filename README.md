# 🦞 指标引擎 (Indicator Engine)

> 加密货币量化指标研发与优化引擎
> 支持：缠论 · 价格行为 · 做市商逻辑 · Pine Script v6 / Python / MQL5

---

## ⚡ 一句话定位

一个专注于**零重绘、无未来函数、强制审核闭环**的加密货币量化指标 Agent，支持缠论体系、经典指标开发、参数优化与 Walk-Forward 验证。

---

## 🎯 核心能力

| 模块 | 功能 |
|---|---|
| **缠论体系** | 分型检测 / 笔构建 / 中枢 / 背驰 / 三买卖点 |
| **价格行为** | 市场结构(HH/HL/LH/LL) / 订单块 / 量价背离 |
| **做市商逻辑** | 订单簿 / 价差分析 / 库存对冲 / 资金费率映射 |
| **指标开发** | RSI / MACD / Squeeze Bollinger / 自定义指标 |
| **参数优化** | 网格搜索 / Walk-Forward / ±15% 扰动测试 |
| **风控框架** | 凯利公式 / 熔断机制 / 信号冲突裁决 |

---

## 🔧 安装（SkillHub / OpenClaw）

### 方式一：通过 npx 安装（推荐）

```bash
npx skills add DYKJLL/indicator-engine@indicator-engine
```

### 方式二：克隆后本地安装

```bash
git clone https://github.com/DYKJLL/indicator-engine.git
cd indicator-engine
npx skills add ./ --yes
```

### 方式三：导入到 OpenClaw / ClawHub

```bash
clawhub install DYKJLL/indicator-engine
```

---

## 🚀 使用示例

安装后，在支持 OpenClaw Agent 的对话中直接发送需求：

```
帮我写一个缠论第三买点的 Pine Script v6
```

```
把 RSI 改写成防重绘 Python 版本
```

```
设计一个缠论 + MACD 的综合策略，要求胜率 > 50%
```

---

## 📐 核心设计原则

### 铁律
- 🚫 **零重绘**：只使用已闭合 K 线
- 🚫 **无未来函数**：不使用前瞻数据
- ✅ **强制审核闭环**：需求 → 架构 → 生成 → 审核 → 测试 → 输出
- ✅ **正向优化**：仅接受提升夏普/降低回撤的修改

### 验证门槛
| 指标 | 要求 |
|---|---|
| 胜率 | ≥ 50% |
| 盈亏比 | ≥ 1.5 |
| 最大回撤 | ≤ 20% |
| 夏普比率 | ≥ 1.0 |
| 参数鲁棒性 | ±15% 扰动下波动 < 20% |

---

## 📁 仓库结构

```
indicator-engine/
├── SKILL.md                     # Agent 系统提示词（完整工作流）
└── references/
    ├── chan_theory.md           # 缠论 Python 实现参考
    └── indicators.md            # 指标库代码参考（RSI/MACD/Squeeze）
```

---

## 🔄 版本历史

| 版本 | 日期 | 内容 |
|---|---|---|
| v1.0.0 | 2026-04-20 | 初始版本：缠论 + RSI/MACD/Squeeze + 做市商逻辑 + 风控框架 |

---

## 📖 了解更多

- [缠论完整算法说明](./references/chan_theory.md)
- [指标库代码参考](./references/indicators.md)

---

## ⚠️ 免责声明

本仓库仅供**研究学习**使用。任何实盘应用产生的盈亏由使用者自行承担，本项目不承担任何责任。
