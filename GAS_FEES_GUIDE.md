# ⛽ Ethereum Gas Fees — Complete Guide

> **Subject:** Secure System Design | **Author:** Muhammad Ahmad (25I-7705)

---

## What Are Gas Fees?

Gas fees are payments made to compensate validators for the computational energy required to process and validate transactions on the Ethereum blockchain. Think of it like a shipping fee — the heavier the package and the faster you want delivery, the more you pay.

---

## The Gas Formula

```
Total Fee = Gas Units Used × (Base Fee + Priority Fee)

Where:
  Gas Units   = Amount of computation required
  Base Fee    = Minimum fee, burned (removed from supply)
  Priority Fee = "Tip" to validator for faster inclusion
```

### Example Calculation

```
Operation:    NFT Transfer
Gas Used:     85,000 units
Base Fee:     20 Gwei
Priority Fee: 2 Gwei

Total = 85,000 × (20 + 2) Gwei
      = 85,000 × 22 Gwei
      = 1,870,000 Gwei
      = 0.00187 ETH
      ≈ $5.50 (at ETH = $2,941)
```

---

## Factors That Influence Gas Cost

### 1. 📈 Network Congestion
When many users are transacting simultaneously, demand for block space exceeds supply. Validators prioritize transactions with higher tips.

```
Low Traffic  → Low Gas  (e.g., 5-10 Gwei base fee)
High Traffic → High Gas (e.g., 100-200+ Gwei base fee)
```

**High traffic events:**
- Popular NFT mint drops
- DeFi protocol launches
- Market volatility causing mass transactions
- Major news events affecting crypto prices

### 2. 🔧 Transaction Complexity

| Operation | Gas Used | Complexity |
|-----------|----------|------------|
| Simple ETH Transfer | 21,000 | Minimal |
| ERC-20 Token Transfer | ~45,000 | Low |
| ERC-721 NFT Transfer | ~85,000 | Medium |
| NFT Mint (simple) | ~100,000–150,000 | Medium |
| NFT Mint (with traits) | ~150,000–250,000 | High |
| Smart Contract Deploy | ~500,000–2,000,000 | Very High |
| Complex DeFi Swap | ~150,000–400,000 | High |

### 3. ⏰ Time of Day / Week

Gas fees follow usage patterns:
- **Lowest:** Weekends, late night UTC (low US/EU activity)
- **Highest:** Weekday business hours (US/EU/Asia overlap)

### 4. 💰 User-Set Priority Fee

Users can choose how much to tip validators:
- **Slow (Low tip):** May wait minutes to hours
- **Standard:** Included in next few blocks (~15–45 seconds)
- **Fast (High tip):** Included in next block (~12 seconds)

---

## EIP-1559: The Fee Market Reform

Since August 2021 (London Hardfork), Ethereum uses a new fee mechanism:

**Before EIP-1559:**
```
User bids any amount → Highest bidder wins → Volatile, unpredictable fees
```

**After EIP-1559:**
```
Protocol sets Base Fee (algorithmically adjusted)
User adds optional Priority Fee (tip)
Base Fee is BURNED (reduces ETH supply = deflationary!)
Only Priority Fee goes to validator
```

**Benefits:**
- More predictable fees
- Reduces ETH supply over time
- Better UX with automatic fee suggestions

---

## Gas Optimization Tips

```
💡 Monitor gas prices at: etherscan.io/gastracker
💡 Transact during off-peak hours (weekends, late night UTC)
💡 Use MetaMask's gas fee suggestions (Low/Market/Aggressive)
💡 Batch multiple operations if possible
💡 Layer-2 networks (Polygon, Arbitrum, Optimism) have 10-100x lower fees
💡 Wait for low congestion windows during non-urgent transactions
```

---

## Layer-2 Solutions (Lower Gas Alternative)

For NFT activities with lower fees:

| Network | Gas vs Ethereum | Popular For |
|---------|----------------|-------------|
| Polygon | ~0.01% | Gaming NFTs, casual trading |
| Arbitrum | ~5-10% | DeFi, NFTs |
| Optimism | ~5-10% | DeFi, NFTs |
| Base | ~1-5% | Consumer apps |
| Immutable X | Gas-free | Gaming NFTs |

---

*Gas Fees Guide | Secure System Design | FAST NUCES*  
*Muhammad Ahmad · Roll No: 25I-7705*
