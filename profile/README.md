## TTSWAP

### Overview

TTSWAP (Token-Token Swap) is a decentralized market-making protocol (AMM) on EVM-compatible chains.

It introduces a Constant Value AMM (CV-AMM) with O(1) algebraic formulas that unify CPMM, weighted pools, and StableSwap behavior.

It routes swaps through a Singleton market architecture instead of pair fragmentation.

---

### Core Mechanisms

Zero Impermanent Loss (Zero IL) returns token amounts based on the historic principal recorded in `proof`, independent of the pool's current price.

Cross-token swaps are O(1) and complete in two steps via `buyGoodInput -> buyGoodOutput` (or `payGoodOutput -> payGoodInput`).

Assets are addressed by `T_GoodKey` under a single `TTSwap_Market` state, enabling Singleton one-token-one-pool.

Protocol-native six-way fee split distributes fees to LP / Operator / Gate / Referral / Customer / Platform, with `checkGoodConfig` enforcing a 100% sum.

EIP-1153 transient storage uses `L_Transient` to guard reentrancy and defines a transient lock boundary for `multicall`.

X402 separates signing from execution so `buyGood` / `payGood` can verify EIP-712 and an Executor can pay gas for a fixed `executeFee`.

TTS uses a price-doubling unlock mechanism and community treasury fees are used for 100% buyback-and-burn.

---

### Entry Points & Docs

Think of TTSWAP as a supermarket checkout desk where each asset maps to its shelf (one good = one pool state).

The whitepaper is at `ttswap-doc/index/v2相关文档/whitepaper.md`; core entrypoints are `TTSwap_Market_Proxy` / `TTSwap_Token_Proxy`.

---

### Typical Use Cases

Launchpad / IDO: `initGood` + `investGood` + `isPromised` + `refreshPromise`.

Single-sided zero-IL market making: `investGood` + `disinvestProof`.

Cross-token swap / payment: `buyGood` / `payGood`.

Aggregation & operations commission: six-way fee split + `setReferral`.

Roadmap: future activation of `T_GoodKey(ercType=2)` for tokenized equities and `T_GoodKey(ercType=3)` for prediction-market outcome shares.

---

### Contacts

| | |
|---|---|
| Twitter | [@ttswapfinance](https://x.com/ttswapfinance) |
| Telegram | [@ttswapfinance](https://t.me/ttswapfinance) |
| Discord | [ttswap](https://discord.gg/XygqnmQgX3) |
| Email | [bussiness@ttswap.io](mailto:bussiness@ttswap.io) |
| Website | [ttswap.io](https://ttswap.io) |
| GitHub | [github.com/ttswap](https://github.com/ttswap) |
