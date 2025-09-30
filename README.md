# Stablecoins-Research-Challenge

## a. Analysis

# Stablecoin Comparison

| Stablecoin | **Backing Mechanism** | **Sustainability** | **Decentralization** |
|------------|------------------------|--------------------|-----------------------|
| **USDC (Circle)** | Fully fiat-backed by highly liquid cash and cash-equivalent assets. Collateral held in U.S. reserves, custodied by regulated U.S. financial institutions. Redeemable 1:1 for USD via Circle. | Highly stable with strong regulatory oversight and transparency (monthly attestations). Risks include exposure to U.S. banking system (e.g., Silicon Valley Bank collapse in March 2023 temporarily caused a depeg). | Fully centralized. Circle controls issuance, redemption, and reserves. Subject to U.S. regulations and blacklisting of addresses. |
| **DAI (MakerDAO)** | Overcollateralized with crypto assets (ETH, wstETH, USDC, etc.). Smart contracts enforce collateral ratios and liquidations. DAI maintains its peg to the US dollar through a mechanism controlled by smart contracts. | Proven resilience (e.g., March 2020 crash). Generates protocol revenue via fees and liquidations. Reliance on USDC as collateral reduces independence and increases exposure to centralized risk. | Semi-decentralized. Governed by MakerDAO token holders, but reliance on USDC and governance token concentration introduce centralization risks. |
| **FRAX (Frax Finance)** | Hybrid model: partially collateralized (USDC, ETH, other assets) and partially algorithmic through mint/burn and AMO (Algorithmic Market Operations). | Survived the UST collapse, showing relative resilience. Sustainability depends on liquidity depth and continued market confidence in fractional backing. Less time-tested than USDC and DAI. | More decentralized than USDC, governed by Frax DAO with on-chain AMOs. Still partly centralized due to USDC reliance and governance concentration. |

## b. Design

- Environment without liquidation risk: Designining an ideal stablecoin in a world where collateral cannot lose value would entail the following:





- Environment with highly risky collateral :
