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
- 要求 `MA169 > MA200`，且 `MA169` 在上行
- 用 `ADX`、均线间距、最近穿越次数过滤震荡区
- 只做趋势中的前几次回踩 `MA169`
- 回踩时要求价格重新收回 `MA169` 上方，且当前 K 线收阳
- 回踩前如果最近频繁跌破 `MA169`，或者之前已经离均线拉升过远，就过滤掉

## 风控与出场

当前版本的风控结构：

- 初始止损：`信号 K 线低点 - ATR * stopAtrMultTrend`
- 第一止盈：默认 `1R`
- 第一止盈后：可以把止损抬到保本
- 剩余仓位：沿 `MA169 - ATR * trailAtrAfterTp1` 跟踪
- 当 runner 止损被击穿时，平掉剩余仓位

这版更偏向：

- 少做
- 只做结构相对干净的趋势回踩
- 让利润主要来自少数真正的主升浪

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
