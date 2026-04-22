# 🖼️ NFT Technical Reference Guide

> **Subject:** Secure System Design | **Author:** Muhammad Ahmad (25I-7705)

---

## What is an NFT?

A **Non-Fungible Token (NFT)** is a unique digital asset whose ownership is recorded on a blockchain. The word *non-fungible* means it cannot be replaced by an identical item — unlike ETH or BTC, where every unit is equal.

```
FUNGIBLE TOKENS          NON-FUNGIBLE TOKENS
─────────────────        ────────────────────
1 ETH = 1 ETH            NFT #1 ≠ NFT #2
Interchangeable           Each is unique
No individual identity    Has metadata & traits
Example: Currency         Example: Digital Art
```

---

## Token Standards

### ERC-721 (Single NFTs)
- Each token has a unique `tokenId`
- One token = one owner
- Transfer function: `safeTransferFrom(from, to, tokenId)`
- Used by: CryptoPunks, Bored Apes, Moonbirds

### ERC-1155 (Multi-Token Standard)
- Single contract can hold both fungible and non-fungible tokens
- Gas-efficient for large collections
- Used by: Gaming items, editions of the same art

---

## NFT Anatomy

```json
{
  "name": "Moonbirds #9141",
  "description": "A collection of 10,000 utility-enabled PFPs",
  "image": "ipfs://QmXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
  "attributes": [
    { "trait_type": "Background", "value": "Purple" },
    { "trait_type": "Body", "value": "Crescent" },
    { "trait_type": "Eyes", "value": "Discerning" },
    { "trait_type": "Feathers", "value": "Brown" },
    { "trait_type": "Headwear", "value": "Witch's Hat" }
  ]
}
```

---

## Moonbirds Collection — Observed on OpenSea

| Property | Value |
|----------|-------|
| Collection | Moonbirds (MOONBIRD) |
| Contract | `0x23581767a106ae21c074b2276D25e5C3e136a68b` |
| Chain | Ethereum Mainnet |
| Standard | ERC-721 |
| Total Supply | 10,000 |
| Floor Price | 1.775 ETH |
| Total Volume | 374.7K ETH |
| Unique Owners | 5,682 (56.8%) |
| Launched | April 2022 |

---

## NFT Lifecycle

```
CREATION (Minting)
    │
    ▼
  Artist creates digital asset
  Metadata stored on IPFS or Arweave
  Smart contract deployed to blockchain
  Token minted → assigned to creator's wallet
    │
    ▼
LISTING (OpenSea / Other Marketplace)
    │
    ▼
  Owner approves marketplace contract
  NFT listed at fixed price or auction
  Royalties configured (% to original creator)
    │
    ▼
PURCHASE (Transfer)
    │
    ▼
  Buyer initiates transaction
  Smart contract executes transfer
  ETH sent to seller (minus marketplace fee)
  NFT ownership recorded on blockchain
    │
    ▼
OWNERSHIP
    │
    ▼
  NFT visible in buyer's wallet (MetaMask, etc.)
  Ownership provably recorded on-chain forever
  Can be re-listed, transferred, or held
```

---

## Storage: Where is the NFT Actually Stored?

A common misconception — NFTs are NOT images stored on the blockchain. The blockchain stores:
- The **token ID** and **ownership record**
- A **URL/URI** pointing to the metadata JSON

The actual image is stored on:
- **IPFS** (InterPlanetary File System) — decentralized, content-addressed
- **Arweave** — permanent, decentralized storage
- **Centralized servers** — (risky! if the server goes down, the image disappears)

> ⚠️ **Security Note:** NFTs stored on centralized servers can have their images changed or disappear entirely if the company shuts down. Always prefer IPFS or Arweave-backed NFTs.

---

## Key Metrics When Evaluating an NFT

| Metric | What It Tells You |
|--------|------------------|
| Floor Price | Minimum price to buy any item in collection |
| Volume (7d/30d) | Trading activity and liquidity |
| Unique Owners % | Distribution — higher = more decentralized |
| Listed % | How many are for sale right now |
| Royalty % | Creator's share on secondary sales |
| Verified ✓ | OpenSea verified the collection is authentic |

---

*NFT Technical Reference | Secure System Design | FAST NUCES*  
*Muhammad Ahmad · Roll No: 25I-7705*
