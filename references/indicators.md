# 核心指标库参考代码

> 来源：指标引擎内部实现 v1.0
> 语言：Python
> 状态：已验证

## 防重绘三定律

1. **只用已闭合K线**：当前K线 state='closed' 时才参与计算
2. **输出信号固定**：一旦确定不再改变
3. **repaint=false 声明**：所有输出前必须声明

```python
# 防重绘Indicator基类
class AntiRepaintIndicator:
    def __init__(self, source='close'):
        self.source = source
        self.confirmed_values = []
        self.pending_value = None

    def update(self, kline):
        if kline['state'] == 'closed':
            value = self._compute(kline)
            self.confirmed_values.append(value)
            self.pending_value = None
        else:
            self.pending_value = self._compute(kline)

    def get_value(self, confirmed_only=True):
        if confirmed_only:
            return self.confirmed_values[-1] if self.confirmed_values else None
        return self.pending_value if self.pending_value else self.confirmed_values[-1]
```

## RSI 关键参数

- period: 14（Wilder平滑，标准值）
- threshold_up: 70（超买）
- threshold_down: 30（超卖）
- 信号：>70 超买 | <30 超卖 | 背离检测

## MACD 关键参数

- fast: 12（快速EMA周期）
- slow: 26（慢速EMA周期）
- signal: 9（信号线EMA周期）
- 金叉：MACD线从下穿越信号线 → 买入
- 死叉：MACD线从上穿越信号线 → 卖出
- Histogram放大：趋势加速信号

## Squeeze 波幅压缩

- BB_period: 20，BB_std: 2.0（布林带）
- KC_period: 20，KC_mult: 1.5（Keltner通道）
- Squeeze ON：布林带宽度 < Keltner通道宽度
- Squeeze OFF + Histogram放大：趋势确认

## 已知陷阱（Error_Log 记录）

1. RSI 使用简单移动平均而非 Wilder 平滑 → 导致 RSI 数值偏误
2. MACD histogram 方向判断仅用当前值 vs 前值，未用移动平均确认 → 噪声过大
3. Squeeze 检测在低波动市场频繁切换 → 需配合波动率过滤器
