# 🔐 Security Analysis — MetaMask & NFT Ecosystem

> **Subject:** Secure System Design | **Author:** Muhammad Ahmad (25I-7705)  
> **University:** FAST NUCES | **Instructor:** Prof. Zafar Iqbal

---

## Executive Summary

The NFT and Web3 ecosystem introduces a unique security paradigm where **users hold complete custody** of their digital assets. Unlike traditional finance, there are no banks, no fraud departments, and no chargebacks. This makes understanding and mitigating security threats a critical responsibility for every participant.

This document provides a comprehensive security analysis of the threats encountered and observed during the MetaMask & NFT hands-on activity.

---

## 1. Threat Model

### 1.1 Threat Actors

| Actor | Motivation | Capability |
|-------|-----------|------------|
| Phishing Attackers | Steal wallet credentials | Medium-High |
| NFT Scammers | Financial fraud via fake assets | Low-Medium |
| Smart Contract Hackers | Drain wallets via malicious contracts | High |
| Social Engineers | Manipulate users into revealing seed phrases | Medium |
| Rug Pull Developers | Exit scam after creating hype | High |

### 1.2 Attack Surface

```
┌─────────────────────────────────────────────────────────────┐
│                    ATTACK SURFACE MAP                       │
│                                                             │
│  Browser Extension   →   [Malicious Extensions]            │
│  Wallet Website      →   [Phishing Clones]                  │
│  NFT Marketplace     →   [Fake Listings, Wash Trading]      │
│  Smart Contracts     →   [Malicious Approvals, Reentrancy]  │
│  Social Media        →   [Impersonation, Fake Giveaways]    │
│  Email/Discord       →   [Phishing Links, Fake Alerts]      │
│  Seed Phrase Storage →   [Physical Theft, Digital Exposure] │
└─────────────────────────────────────────────────────────────┘
```

---

## 2. Detailed Threat Analysis

### 2.1 🎣 Phishing Attacks

**Description:**  
Phishing is the most prevalent threat in the Web3 space. Attackers create near-perfect replicas of MetaMask, OpenSea, or other platforms to deceive users.

**Attack Vectors:**
- Fake MetaMask popup windows on malicious websites
- Typosquatted domains (e.g., `0pensea.io` instead of `opensea.io`)
- Fake "wallet verification" emails
- Discord DMs from fake support accounts
- Google Ads leading to phishing sites (documented cases)

**Indicators of Compromise:**
- URL doesn't match the expected domain exactly
- HTTPS padlock missing or untrusted certificate
- Requests for seed phrase or private key
- Unusual urgency ("Your wallet will be suspended!")

**Mitigation:**
```
✅ Bookmark all trusted Web3 sites — never search Google
✅ Verify the EXACT URL before entering any credentials
✅ Never enter seed phrase on any website — MetaMask never asks for it
✅ Enable MetaMask's built-in phishing detection
✅ Use a hardware wallet (Ledger/Trezor) for high-value assets
```

**Risk Level:** 🔴 CRITICAL

---

### 2.2 🎨 Fake NFT Scams

**Description:**  
Since anyone can mint NFTs, the ecosystem is flooded with fraudulent tokens — copies of legitimate artwork sold without authorization.

**Common Scam Types:**
1. **Copy-Minted NFTs** — Stolen artwork re-minted under a fake contract
2. **Fake Collections** — Collections with names similar to popular projects (e.g., "BoredApeYC" instead of "BoredApeYachtClub")
3. **Wash Trading** — Artificially inflating trading volume to create hype
4. **Airdrop Scams** — Sending malicious NFTs that drain wallets when interacted with

**How to Verify Authenticity:**
```
Step 1: Check for OpenSea's verified blue checkmark ✓
Step 2: Verify the exact contract address on Etherscan
Step 3: Cross-reference with the project's official social media
Step 4: Check trading volume history for suspicious patterns
Step 5: Look up the creator's wallet history on Etherscan
```

**Risk Level:** 🟠 HIGH

---

### 2.3 🔑 Compromised Seed Phrase

**Description:**  
The seed phrase (12 or 24 words) is the absolute master key to a wallet. Anyone who obtains it gains **complete, irreversible control** over all assets.

**How Attackers Steal Seed Phrases:**
- Social engineering ("I'm MetaMask support, need your phrase to restore")
- Fake wallet recovery websites
- Malicious browser extensions logging keystrokes
- Screenshots stored in cloud (iCloud, Google Photos)
- Phishing forms that "verify" wallet by asking for the phrase
- Clipboard hijackers

**Real-World Impact:**
> Once a seed phrase is stolen, all funds can be drained in seconds. There is no recovery mechanism. No platform can reverse the transaction. The loss is permanent.

**Protection Measures:**
```
🔒 Write seed phrase on paper — NEVER digitally
🔒 Store in a fireproof/waterproof safe
🔒 Never photograph the seed phrase
🔒 Never type it into any website or app
🔒 Never share with anyone, including "support"
🔒 Consider a metal backup plate for long-term storage
```

**Risk Level:** 🔴 CRITICAL

---

### 2.4 📋 Malicious Smart Contracts

**Description:**  
Smart contracts are self-executing programs on the blockchain. Malicious contracts can be designed to steal permissions and drain wallets.

**Attack Patterns:**

**SetApprovalForAll Exploit:**
```
Normal Use:  User approves OpenSea to manage NFTs for listing
Attack Use:  Malicious site tricks user into approving unlimited 
             transfers to attacker's wallet
```

**Honeypot Tokens:**
- Tokens that can be bought but never sold
- Trapped liquidity that benefits only the creator

**Reentrancy Attacks:**
- A contract that calls back into the calling contract repeatedly before state updates, draining funds (e.g., the famous DAO hack of 2016)

**Signs of a Malicious Contract:**
```
⚠️  Requests SetApprovalForAll for no clear reason
⚠️  Contract code is unverified on Etherscan
⚠️  Unusually high gas fees requested
⚠️  Contract was deployed very recently (hours/days ago)
⚠️  No audit report available
```

**Mitigation:**
```
✅ Always review what a transaction does before signing
✅ Use Revoke.cash to audit and revoke token approvals
✅ Verify contract source code on Etherscan
✅ Check contract audit reports before interacting
✅ Use MetaMask's transaction simulation feature
```

**Risk Level:** 🔴 HIGH

---

## 3. MetaMask Security Architecture

### 3.1 Key Security Features

```
┌──────────────────────────────────────────────────────────────┐
│              MetaMask Security Architecture                  │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  LOCAL KEY STORAGE                                           │
│  Private keys encrypted with AES-256 and stored locally     │
│  Never transmitted to MetaMask servers                       │
│                                                              │
│  SEED PHRASE PROTECTION                                      │
│  12-word BIP-39 mnemonic for deterministic key derivation   │
│  Shown ONCE at setup — user responsible for backup          │
│                                                              │
│  TRANSACTION APPROVAL FLOW                                   │
│  Every transaction requires explicit user approval          │
│  Gas fee displayed before signing                           │
│  Transaction data decoded for review                         │
│                                                              │
│  PHISHING DETECTION                                          │
│  Maintains blocklist of known phishing domains              │
│  Warns users before connecting to flagged sites             │
│                                                              │
│  PERMISSION SYSTEM                                           │
│  dApps must request permission before accessing wallet      │
│  Users can revoke permissions at any time                   │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### 3.2 Cryptographic Foundation

MetaMask uses the **Ethereum key infrastructure**:

- **Key Generation:** Elliptic Curve Cryptography (secp256k1)
- **Address Derivation:** Keccak-256 hash of public key (last 20 bytes)
- **Transaction Signing:** ECDSA (Elliptic Curve Digital Signature Algorithm)
- **Wallet Encryption:** AES-256-GCM with PBKDF2 key derivation

---

## 4. Security Recommendations

### For Students & Beginners

| Priority | Action |
|----------|--------|
| 🔴 Critical | Never share seed phrase with anyone, ever |
| 🔴 Critical | Use a dedicated browser for crypto activities |
| 🟠 High | Enable 2FA on all exchange accounts |
| 🟠 High | Verify every URL before connecting wallet |
| 🟡 Medium | Use a hardware wallet for real funds |
| 🟡 Medium | Regularly audit token approvals on Revoke.cash |
| 🟢 Low | Join reputable communities for scam alerts |

### Security Checklist Before Any Transaction

```
□ I verified the website URL is correct
□ The smart contract is verified on Etherscan
□ I understand what permissions I'm granting
□ The gas fee seems reasonable for this operation
□ I'm not under pressure to act quickly
□ The offer seems realistic (not too good to be true)
□ I've checked the project's official channels
```

---

## 5. Incident Response

If your wallet is compromised:

1. **Immediately** transfer any remaining assets to a NEW wallet
2. Revoke all token approvals from the compromised wallet on Revoke.cash
3. Document the attack (transaction hashes, wallet addresses)
4. Report to the relevant platform (OpenSea, MetaMask)
5. Report the phishing site to MetaMask's phishing detector
6. Report to your local cybercrime authority if significant funds lost

---

*Security Analysis | Secure System Design | FAST NUCES*  
*Muhammad Ahmad · Roll No: 25I-7705*
