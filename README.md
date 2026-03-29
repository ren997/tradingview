# TradingView BTC MA169 Trend Pullback

这个仓库当前只保留一个策略文件：

- [`btc_ma169_trend_pullback_long_strategy.pine`](C:\D\workspace\github\tradingview\btc_ma169_trend_pullback_long_strategy.pine)

项目目标很简单：

- 只研究 `BTC` 的 `MA169` 趋势回踩做多
- 优先面向 `4 小时` 周期
- 不再混入突破做多、二次洗盘、做空等旁支实验

## 当前策略思路

这份 Pine 策略的核心逻辑是：

- 用 `MA169` 和 `MA200` 判断大方向
- 要求 `close > MA169`、`MA169 > MA200`，且 `MA169` 本身保持上行
- 先等待价格明显拉离 `MA169`
- 只做这段离均之后的第一次高质量回踩
- 高质量的意思是：第一次回踩事件成立，且信号 K 收盘位置足够强
- 回踩时要求价格重新收回 `MA169` 上方
- 不再用 `ADX` 和震荡过滤去拦截信号，优先减少错过主升浪，同时尽量避免后期晚回踩

## 风控与出场

当前版本的风控结构：

- 初始止损：`信号 K 线低点 - ATR * signalStopAtrBuffer`
- 开仓后不做分批止盈
- 价格先再次拉离 `MA169` 之后，只要下一次重新触碰 `MA169`，就直接离场
- 这版更强调“抓离均后的第一次回踩”，而不是长时间拿 runner

补充：

- 仓库里现在还有一份单独的新文件 [`btc_ma169_base_breakout_long_strategy.pine`](C:\D\workspace\github\tradingview\btc_ma169_base_breakout_long_strategy.pine)
- 它专门做“MA169 上方/附近震荡后带量突破”
- 这份突破策略当前使用：
  - `突破K低点下方止损`
  - `后续若K线实体完全收在MA169下方则离场`

这版更偏向：

- 少做
- 只做结构相对干净、位置更早的趋势回踩
- 尽量避开已经拖很久的晚回踩

## 使用方式

1. 打开 TradingView Pine Editor
2. 粘贴 [`btc_ma169_trend_pullback_long_strategy.pine`](C:\D\workspace\github\tradingview\btc_ma169_trend_pullback_long_strategy.pine)
3. 添加到图表
4. 优先测试 `4小时`

建议先关注：

- 总交易次数
- 盈利因子
- 最大回撤
- 主升浪是否能拿住
- 低质量回踩是否还太多

## 仓库约束

当前仓库刻意保持极简：

- 只保留一个 `.pine` 策略文件
- 其余实验脚本已移除
- 后续优化默认都基于这一份文件进行

如果要继续迭代，优先方向建议是：

- 提高回踩质量
- 减少震荡期误入场
- 更早识别趋势失效
- 保持代码可读，不重新长出多个分叉策略
