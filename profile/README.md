# PolyPay

> Privacy-preserving payroll platform built on Horizen

[![Website](https://img.shields.io/badge/Website-polypay.io-blue)](https://polypay.io)
[![Twitter](https://img.shields.io/badge/Twitter-@polypay-1DA1F2)](https://twitter.com/polypay)
[![Status](https://img.shields.io/badge/Status-Beta%20v0.1-yellow)]()

---

## What is PolyPay?

PolyPay is a **privacy-preserving payroll platform** that combines [Horizen's privacy layer](https://horizen-2-docs.horizen.io/) with cross-chain settlement infrastructure. It enables organizations, DAOs, and global teams to run payroll **privately on Horizen** while staying on their preferred blockchain.

### Key Features

- **Private Payments**: Salary amounts and recipients stay confidential
- **Private Multisig**: Team approvals without exposing signer identities using zero-knowledge proofs
- **Flexible Payment Logic**: Support for escrow-based, milestone-based, and recurring transfers
- **Cross-Chain Settlement**: Operate on Horizen while maintaining presence on preferred blockchains
- **Fiat Integration**: Seamless on/off-ramp services for fiat-to-crypto conversions

### Who Is It For?

- 🚀 **Crypto-native startups and SMBs** looking for private payroll solutions
- 🏛️ **DAOs** managing contributor payments and treasury operations
- 🏢 **Traditional businesses** entering the crypto ecosystem
- 🔒 **Teams using Safe or Squads** who want privacy upgrades without changing workflows

---

## The Problems We Solve

Current on-chain payment solutions expose sensitive business information publicly, creating significant barriers to enterprise adoption:

### 1. **Lack of Privacy**
- **Employee salaries are visible to everyone** on the blockchain
- **Payment recipients can be tracked** and linked to wallet addresses
- **Multisig approvers are publicly identified**, exposing organizational structure
- Competitors can analyze your spending patterns and business operations

### 2. **Limited Payment Flexibility**
- Most solutions offer only simple transfers
- No support for conditional payments (escrow, milestones)
- Difficult to implement recurring payroll schedules
- Poor integration with existing multisig workflows

### 3. **Poor User Experience**
- Complex crypto operations intimidate traditional businesses
- No seamless fiat conversion options
- Steep learning curve for non-crypto-native users
- Lack of compliance and audit trails

### 4. **Enterprise Barriers**
These privacy and usability issues prevent businesses from adopting on-chain payments, limiting:
- Mainstream crypto adoption
- On-chain transaction volume
- Enterprise migration to Web3
- DAO operational efficiency

---

## How PolyPay Helps

PolyPay addresses these challenges through innovative privacy technology and user-centric design:

### 🔐 Privacy Architecture

#### Commitment-Based Identity
Instead of storing public addresses on-chain, PolyPay uses **cryptographic commitments**:

```
commitment = hash(secret, secret)
```

- The **secret** is derived from signing a message with your wallet
- The **commitment** is stored on-chain in a Merkle tree
- Only you know the secret that matches your commitment

#### Zero-Knowledge Proofs
When you sign a transaction, you prove **"I am an authorized signer"** without revealing **which signer** you are.

**Traditional Multisig vs PolyPay:**

| Aspect | Traditional Multisig | PolyPay |
|--------|---------------------|---------|
| Signer Identity | Public addresses on-chain | Hidden behind commitments |
| Who Signed | Visible to everyone | Only the signer knows |
| Transaction Amount | Public | Private |
| Anonymity | None | Complete anonymity set |

#### Relayer Privacy
PolyPay uses a dedicated **relayer wallet** to further enhance privacy:

- Signers submit ZK proofs **off-chain** to the backend
- The relayer executes transactions on behalf of users
- **No signer address ever appears on-chain**

| Action | Without Relayer | With Relayer |
|--------|----------------|--------------|
| Deploy wallet | Creator address exposed | Only relayer visible |
| Execute transaction | Executor address exposed | Only relayer visible |

### 🛠️ Technical Implementation

#### Four Zero-Knowledge Proofs
Every transaction signature proves four things simultaneously:

1. **"I know the transaction"** - Verifies the transaction hash using Poseidon Hash
2. **"I signed it"** - Validates ECDSA signature (Ethereum standard)
3. **"I am authorized"** - Proves membership in signers list via Merkle proof
4. **"I haven't signed before"** - Prevents double-signing using nullifiers

```
nullifier = hash(secret, tx_hash)
```

#### ZK Circuit (Noir + UltraPlonk)
The circuit is written in **Noir** and compiled to **UltraPlonk** for efficient verification via [zkVerify](https://docs.zkverify.io/).

**Complete Flow:**
1. User signs `tx_hash` with Ethereum wallet → produces signature
2. Frontend generates ZK proof with private inputs (signature, secret, merkle_path)
3. Backend submits proof to **zkVerify** for verification
4. Smart contract executes when threshold reached, verifying all proofs and checking nullifiers

### 💼 Business Benefits

#### For Organizations
- **Confidential Payroll**: Keep salary information private
- **Compliance Ready**: Integration with compliance protocols like Predicate
- **Flexible Payments**: Escrow, milestone, and recurring options
- **Cost Efficient**: Reduce operational overhead

#### For DAOs
- **Private Treasury Operations**: Hide contributor payments and budget allocation
- **Multisig Privacy**: Maintain operational security
- **Cross-Chain Flexibility**: Operate on Horizen while supporting multiple chains

#### For Traditional Businesses
- **Easy Onboarding**: Fiat on/off-ramp integration
- **Familiar Workflows**: Upgrade existing Safe/Squads setups
- **Lower Barrier**: User-friendly interface for non-crypto teams

### 🌐 Ecosystem Integration

- **Privacy Layer**: [Horizen](https://horizen-2-docs.horizen.io/) for privacy infrastructure
- **Verification**: [zkVerify](https://docs.zkverify.io/) for efficient proof verification
- **On/Off-Ramp**: Integration with services like Bridge for fiat payments
- **Compliance**: Predicate and other third-party protocols
- **Deployment**: Base mainnet (Ethereum L2)

---

## Status

### Current Version: **Beta v0.1** (Testnet)

#### ✅ Available Features
- ✓ Create and manage multisig wallets on Ethereum Sepolia testnet
- ✓ Hide signer identities with ZK proofs
- ✓ Execute payroll payments to multiple recipients
- ✓ View transaction history and wallet balance
- ✓ Commitment-based identity system
- ✓ Zero-knowledge proof generation and verification

#### 🚧 Development Roadmap

**Milestone 1: Testnet Launch** ✅ *Completed: November 16, 2025*
- [x] Functioning app on Horizen testnet
- [x] Horizen privacy integration
- [x] Technical documentation with privacy proofs
- [x] Beta testing with user feedback

**Milestone 2: Mainnet Launch** 🏗️ *Target: December 31, 2025*
- [ ] Deploy on Base mainnet with full functionality
- [ ] Privacy compliance documentation and audit reports
- [ ] Integration with Horizen ecosystem tools
- [ ] Process 100+ transactions in first month
- [ ] Achieve 100% feature parity with testnet

**Milestone 3: Scale** 📈 *Target: March 1, 2026*
- [ ] Onboard 5+ active businesses from Base ecosystem
- [ ] Strategic on/off-ramp partnerships
- [ ] 30% of transactions involve fiat conversion
- [ ] Growth metrics achievement

### 🎯 3-6 Month Goals

1. **Mainnet Launch with Core Features**
   - Deploy on Base mainnet
   - 100% feature parity with testnet
   - 100+ transactions in first month

2. **Onboard Base Ecosystem Businesses**
   - Acquire 5+ active businesses
   - Migrate existing Base payroll users

3. **Strategic Partnerships**
   - Integrate major fiat on/off-ramp protocols
   - 30% fiat conversion rate

### 🏆 Competitive Advantage

PolyPay is the **first privacy-preserving, cross-chain payroll platform** that provides:
- ✨ Features that Request Finance and Copperx don't offer
- 🔒 Complete transaction privacy (amounts + identities)
- 🌉 Cross-chain settlement on Horizen
- 💰 Programmable payment logic (escrow, milestones, recurring)
- 🔐 Private multisig with ZK proofs
- 💵 Seamless fiat integration

---

## Getting Started

### User Workflow

1. **Connect Wallet**: Connect your Ethereum wallet
2. **Generate Identity**: Sign a message to create your secret commitment
3. **Create/Join Wallet**: Deploy new multisig or join existing one
4. **Propose Transaction**: Create transfer and generate ZK proof
5. **Sign**: Other signers approve with their ZK proofs
6. **Execute**: When threshold reached, execute the transaction

### Try It Out

🌐 **Beta App**: [Coming Soon]
📺 **Video Demo**: [Coming Soon]
📚 **Documentation**: [Coming Soon]

---

## Technology Stack

- **Privacy**: Horizen Privacy Layer
- **ZK Proofs**: Noir + UltraPlonk + zkVerify
- **Blockchain**: Base (Ethereum L2), Ethereum Sepolia (Testnet)
- **Smart Contracts**: Solidity
- **Frontend**: Next.js + TypeScript
- **On/Off-Ramp**: Bridge Protocol (planned)
- **Compliance**: Predicate (planned)

---

## Contributing

PolyPay is currently in private development. We welcome feedback and partnership inquiries.

---

## Resources

- 🌐 [Website](https://polypay.io)
- 🐦 [Twitter/X](https://twitter.com/polypay)
- 📖 [Horizen Documentation](https://horizen-2-docs.horizen.io/)
- 📖 [zkVerify Documentation](https://docs.zkverify.io/)
- 📧 Contact: [Coming Soon]

---

## License

[License information to be added]

---

<div align="center">

**Built with privacy by default. Powered by Horizen.**

*Accelerating mainstream crypto adoption through private, compliant on-chain payments*

</div>

