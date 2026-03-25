# AGENT.md

## 项目定位

这个仓库当前只服务一个目标：

- 维护并优化 `BTC MA169` 的趋势回踩做多策略

唯一策略文件：

- [`btc_ma169_trend_pullback_long_strategy.pine`](C:\D\workspace\github\tradingview\btc_ma169_trend_pullback_long_strategy.pine)

## 对代理/协作者的硬规则

1. 不要新建额外的 `.pine` 策略分叉文件，除非用户明确要求。
2. 默认只在现有的 [`btc_ma169_trend_pullback_long_strategy.pine`](C:\D\workspace\github\tradingview\btc_ma169_trend_pullback_long_strategy.pine) 上迭代。
3. 不要把做空、突破做多、验证脚本等旧实验逻辑重新混回仓库，除非用户明确要求恢复。
4. Pine 版本保持 `//@version=6`。
5. 参数名和注释默认使用中文，便于用户直接在 TradingView 中阅读。
6. 修改前优先保持策略逻辑简洁，避免为了覆盖少量特殊形态加入过多状态机。
7. 优先面向 `4小时` 周期优化，不默认针对 `15分钟/30分钟` 设计。
8. 任何新增过滤器都应回答一个明确问题：
   - 是为了减少震荡误入场？
   - 还是为了更稳地抓住主升浪？
9. 不要重复插入同样的说明注释或调试日志。
10. 删除文件、重命名文件、恢复旧策略前，要先确认用户意图。

## 策略方向偏好

后续优化默认遵循这些方向：

- 顺趋势做多优先
- 少做逆势抄底
- 少做震荡区来回交易
- 尽量让收益来自少数高质量趋势单
- 接受错过，不为增加交易次数而放宽到失真

## 代码风格

- 保持分段清晰：
  - 参数
  - 指标
  - 市场状态
  - 信号
  - 仓位管理
  - 图形标记
- 只添加简短、信息密度高的注释
- 不要保留无用变量、废弃实验参数或死代码
- 调试日志默认关闭，且保持最小必要

## 提交原则

- 提交信息默认遵循 Conventional Commits 规范，优先使用：
  - `feat:`
  - `fix:`
  - `docs:`
  - 需要时再使用 `refactor:`、`test:`、`chore:` 等类型
- 推荐格式：`type(scope): summary`
- 示例：
  - `feat(strategy): improve MA169 pullback entry filter`
  - `fix(exit): correct runner stop breach handling`
  - `docs(repo): update README and AGENT guidance`
- 如果一次修改同时影响“入场”和“出场”，提交说明里要把两点都写清楚
- 如果没有经过 TradingView 实际编译验证，要在交付时明确说明
