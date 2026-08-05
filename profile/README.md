## TTSWAP

### Overview

TTSWAP (Token-Token Swap) is a decentralized market-making protocol (AMM) on EVM-compatible chains.
<sub><em>TTSWAP（Token-Token Swap）是运行在 EVM 兼容链上的去中心化做市协议（AMM）。</em></sub>

It introduces a Constant Value AMM (CV-AMM) with O(1) algebraic formulas that unify CPMM, weighted pools, and StableSwap behavior.
<sub><em>它引入恒定价值 AMM（CV-AMM），用一套 O(1) 代数公式统一 CPMM、加权池与 StableSwap 行为。</em></sub>

It routes swaps through a Singleton market architecture instead of pair fragmentation.
<sub><em>它通过 Singleton 市场架构完成交易路由，而不是把流动性碎片化到 pair。</em></sub>

---

### Core Mechanisms

Zero Impermanent Loss (Zero IL) returns token amounts based on the historic principal recorded in `proof`, independent of the pool's current price.
<sub><em>零无常损失（Zero IL）按 `proof` 记录的历史本金比例返还代币数量，且与池内当下价格无关。</em></sub>

Cross-token swaps are O(1) and complete in two steps via `buyGoodInput -> buyGoodOutput` (or `payGoodOutput -> payGoodInput`).
<sub><em>跨币互换为 O(1)，并通过 `buyGoodInput -> buyGoodOutput`（或 `payGoodOutput -> payGoodInput`）两步完成。</em></sub>

Assets are addressed by `T_GoodKey` under a single `TTSwap_Market` state, enabling Singleton one-token-one-pool.
<sub><em>所有资产由 `T_GoodKey` 在同一个 `TTSwap_Market` 状态下寻址，从而实现 Singleton 一币一池。</em></sub>

Protocol-native six-way fee split distributes fees to LP / Operator / Gate / Referral / Customer / Platform, with `checkGoodConfig` enforcing a 100% sum.
<sub><em>协议原生六方分佣将费用分配给 LP / Operator / Gate / Referral / Customer / Platform，并由 `checkGoodConfig` 强制六方占比之和为 100%。</em></sub>

EIP-1153 transient storage uses `L_Transient` to guard reentrancy and defines a transient lock boundary for `multicall`.
<sub><em>EIP-1153 瞬态存储使用 `L_Transient` 的瞬态锁来防重入，并为 `multicall` 定义安全边界。</em></sub>

X402 separates signing from execution so `buyGood` / `payGood` can verify EIP-712 and an Executor can pay gas for a fixed `executeFee`.
<sub><em>X402 将签名与执行分离，使得 `buyGood` / `payGood` 可以校验 EIP-712，并由 Executor 代付 gas 获取固定 `executeFee`。</em></sub>

TTS uses a price-doubling unlock mechanism and community treasury fees are used for 100% buyback-and-burn.
<sub><em>TTS 采用价格翻倍解锁机制，并将社区金库手续费用于 100% 回购并销毁。</em></sub>

---

### Entry Points & Docs

Think of TTSWAP as a supermarket checkout desk where each asset maps to its shelf (one good = one pool state).
<sub><em>可以把 TTSWAP 当成超市结算台，每个资产对应一条货架（一个 good 一份池状态）。</em></sub>

The whitepaper is at `ttswap-doc/index/v2相关文档/whitepaper.md`; core entrypoints are `TTSwap_Market_Proxy` / `TTSwap_Token_Proxy`.
<sub><em>白皮书位于 `ttswap-doc/index/v2相关文档/whitepaper.md`，核心入口合约为 `TTSwap_Market_Proxy` / `TTSwap_Token_Proxy`。</em></sub>

---

### Typical Use Cases

Launchpad / IDO: `initGood` + `investGood` + `isPromised` + `refreshPromise`.
<sub><em>Launchpad / IDO 流程使用 `initGood` + `investGood` + `isPromised` + `refreshPromise`。</em></sub>

Single-sided zero-IL market making: `investGood` + `disinvestProof`.
<sub><em>单边零无常做市使用 `investGood` + `disinvestProof`。</em></sub>

Cross-token swap / payment: `buyGood` / `payGood`.
<sub><em>跨币 swap 与支付使用 `buyGood` / `payGood`。</em></sub>

Aggregation & operations commission: six-way fee split + `setReferral`.
<sub><em>聚合与运营分账依托六方分佣并结合 `setReferral`。</em></sub>

Roadmap: future activation of `T_GoodKey(ercType=2)` for tokenized equities and `T_GoodKey(ercType=3)` for prediction-market outcome shares.
<sub><em>路线图包含未来启用 `T_GoodKey(ercType=2)`（RWA/股票化）与 `T_GoodKey(ercType=3)`（预测市场结果份额）。</em></sub>

---

### Contacts

| | |
- **Twitter**: [@ttswapfinance](https://x.com/ttswapfinance)
- **Telegram**: [@ttswapfinance](https://t.me/ttswapfinance)
- **Email**: [bussiness@ttswap.io](mailto:bussiness@ttswap.io)
- **Discord**: [ttswap](https://discord.gg/XygqnmQgX3)
- **Website**: [ttswap.io](http://ttswap.io)
- **GitHub**: [github.com/ttswap](https://github.com/ttswap)
