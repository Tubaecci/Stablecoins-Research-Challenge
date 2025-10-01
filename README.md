# Stablecoins-Research-Challenge

Stablecoins are a type of cryptocurrency designed to maintain a stable value by being tied to an external asset such as fiat currency, a commodity, or even another crypto asset. They offer less price volatility compared to traditional cryptocurrencies. Stablecoins are typically backed in four ways: fiat-backed, commodity-backed, crypto-backed, and algorithmic. Some popular stablecoins include USDC, USDT, DAI, FRAX, and EURC.

## a. Analysis

# Stablecoin Comparison

| Stablecoin | **Backing Mechanism** | **Sustainability** | **Decentralization** |
|------------|------------------------|--------------------|-----------------------|
| **USDC (Circle)** | Fully fiat-backed by highly liquid cash and cash-equivalent assets. Collateral held in U.S. reserves, custodied by regulated U.S. financial institutions. Redeemable 1:1 for USD via Circle. | Highly stable with strong regulatory oversight and transparency (monthly attestations). Risks include exposure to U.S. banking system (e.g., Silicon Valley Bank collapse in March 2023 temporarily caused a depeg). | Fully centralized. Circle controls issuance, redemption, and reserves. Subject to U.S. regulations and blacklisting of addresses. |
| **DAI (MakerDAO)** | Overcollateralized with crypto assets (ETH, wstETH, USDC, etc.), hence crypto-backed. DAI maintains its peg to the US dollar through a mechanism controlled by smart contracts. | Proven resilience (e.g., March 2020 crash). Generates protocol revenue via fees and liquidations. Reliance on USDC as collateral reduces independence and increases exposure to centralized risk. | More decentralized than fiat-backed coins. Governed by MakerDAO token holders, but reliance on USDC and governance token concentration introduce centralization risks. |
| **FRAX (Frax Finance)** | Hybrid model: partially collateralized (USDC, ETH, other assets) and partially algorithmic through mint/burn via AMOs (Algorithmic Market Operation Contracts). | Survived the UST collapse, showing relative resilience. Sustainability depends on liquidity depth and continued market confidence in fractional backing. Less time-tested than USDC and DAI. | Typically decentralized through its on-chain governance model where veFXS holders can vote on-chain to pass proposals. Still partly centralized because of reliance on USDC collateral and governance concentration among large holders.

## b. Design

1. Environment without liquidation risk: Designining an ideal stablecoin in a world where collateral cannot lose value would most likely involve a reserve-backed stablecoin fully collateralized 1:1 by a riskless on-chain asset with minting and burning (redemption). This will entail:
   
I. **Asset model and issuance**: A tokenized, non-volatile reserve asset (RESV) that is provably constant in value and instantly redeemable off-chain would serve as the collateral. Every stablecoin (STABLE) will be backed 1:1 by RESV held in onchain vaults. Because RESV never loses value, no over-collateralization required. Basically, users deposit RESV to mint equal amounts of STABLE. On the other hand users can burn their to STABLE to redeem similar amount in RESV. STABLE is an ERC-20 token in this case.
II. **Capital essiciency**: No over-collateralization needed here, so capital efficiency is maximal. Because collateral cannot lose value, a portion of RESV can be safely deployed into ultra-safe yield (short-duration T-bills / riskless lending equivalent) to earn interest. Thus, Interest accrues to a reserve surplus.

2. Environment with highly risky collateral: In a scenario where all collateral assets are volatile, I would design a stablecoin using the following processes:

I. **Overcollateralization**: Always require deposits worth more than the stablecoins minted (e.g., 150–300%). This provides a buffer against price drops.
II. **Dynamic Collateral Management**:
- Accept a basket of volatile assets rather than just one.
- Continuously rebalance to reduce exposure to sharp crashes.
III.  **Automatic Liquidations**:
- If collateral value falls near the debt level, the system auto-sells/liquidates collateral.
- Prevents under-collateralization.
IV. **Peg Stability Tools:**
- Arbitrage via mint/redeem at $1.
- Buyback-and-burn programs if peg drifts.
- Emergency shutdown to ensure final redemption.

In essence, such a stablecoin would be overcollateralized, basket-backed, and liquidation-driven, with strong incentive mechanisms to protect the peg against the volatility of all assets.


## c. Modelling: Bank Run On A Centralized Stablecoin
### Core idea

- A bank run happens if redemption demand (A) exceeds issuer’s liquid capacity (L).
- This creates unmet demand (U = A − L), eroding confidence and pushing price below $1.
- An attacker profits by shorting the stablecoin and triggering/predicting this panic.


### Key Variables

- S: supply of stablecoin
- R: liquid reserves
- C: daily redemption capacity
- D: delay window (days)
- B: backup credit lines
- L = R + B + C*D: issuer’s effective liquidity
- U = A − L: unmet redemptions (if positive)
- α: market sensitivity to panic
- H: attacker’s short position
- M + K + Lr: attacker’s total costs

### Profitability condition

Attack is profitable if:
```
Expected Profit = p_s * H * α * (U / S)  >  M + K + Lr
```

- p_s: probability the attack causes panic

- α * (U/S): size of the peg break (price drop fraction)

- Attacker needs large unmet redemptions U and cheap shorts H to succeed.

### Conditions for profitable attack
- Low liquidity capacity (L small) → easy to overwhelm.
- High market sensitivity (α large) → small unmet demand crashes price.
- Deep derivative markets (H cheap) → attacker can short big.
- Weak issuer transparency → higher panic probability (p_s).

### Mitigations
1. Hold high liquid reserves + committed credit lines (raise L).
2. Increase redemption throughput (raise C).
3. Publish proof-of-reserves to reduce p_s.
4. Use circuit-breakers or staged redemptions (limit U).
5. Cap per-account redemptions and diversify fiat rails.
6. Maintain liquidity on exchanges to lower α.


In essence, a centralized stablecoin is vulnerable if redemption demand outpaces liquid backing. Attacks succeed when unmet demand is large, panic sensitivity is high, and shorting is cheap. The defense is more liquidity, transparency, and throttling redemption speed.
