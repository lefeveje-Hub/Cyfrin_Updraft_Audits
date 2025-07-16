# ❄️ Snowman Merkle Airdrop Audit (my first audit)
**Platform:** CodeHawks  
**Duration:** June 16 - June 19, 2025  
**Prize Pool:** 100 EXP  
**Language:** Solidity  
**Difficulty:** Beginner Friendly

## About
The Snowman Merkle Airdrop protocol is a beginner-friendly First Flight consisting of three main contracts that work together to create an NFT distribution system. Users can earn or purchase Snow tokens and stake them to receive Snowman NFTs through an efficient Merkle tree-based airdrop mechanism. The system features weekly token earning capabilities, dual payment methods (ETH/WETH), and on-chain NFT storage using Base64 encoding.

## Scope
| Contract | Description |
|----------|-------------|
| Snow.sol | ERC20 token enabling weekly earnings and purchases via ETH/WETH |
| Snowman.sol | ERC721 contract with Base64-encoded on-chain storage |
| SnowmanAirdrop.sol | Merkle tree implementation for efficient NFT distribution with signature support |

## Results
- **High Severity:** 6 findings
- **Medium Severity:** 6 findings  
- **Low Severity:** 3 findings
- **Focus Areas:** Access control, reentrancy, signature verification, payment logic

### Judge Feedback
**Lead Judge:** yeahchibyke

> "H3, H5, M3 are valid. The other submissions in your report are invalid, but it is a mixture of design choice, incorrect statements, and a couple of informationals.
> 
> Good job."

### Validated Findings
The following findings were confirmed as valid by the judge:

**🔴 H-3: Unrestricted NFT mint function**
- The mint function of the Snowman contract is unprotected, allowing anyone to mint NFTs without participating in the airdrop

**🔴 H-5: Inconsistent MESSAGE_TYPEHASH with standard EIP-712 declaration**  
- A typo in the `MESSAGE_TYPEHASH` variable prevents signature verification claims (used 'addres' instead of 'address')

**🟡 M-3: Lack of claim check**
- The claim function doesn't verify that a recipient has already claimed a Snowman, posing potential risks in future implementations

## Findings
📋 **[View Detailed Findings](paste.txt)**

### High Severity Issues
- **H-1:** Global timer prevents multiple users from earning Snow tokens
- **H-2:** Incorrect payment logic causes user fund loss in buySnow()
- **✅ H-3:** Missing access control allows unlimited NFT minting *(Validated)*
- **H-4:** Arbitrary transferFrom enables token theft
- **✅ H-5:** Typo in MESSAGE_TYPEHASH breaks signature verification *(Validated)*
- **H-6:** Reentrancy vulnerability in mintSnowman()

### Medium Severity Issues
- **M-1:** Reentrancy vulnerability in fee collection
- **M-2:** Transaction atomicity issues in fee collection
- **✅ M-3:** Missing double-claim protection *(Validated)*
- **M-4:** DoS via unbounded loop in minting
- **M-5:** Unchecked transfer return values
- **M-6:** Missing merkle root validation

### Low Severity Issues
- **L-1:** Incorrect event emission semantics
- **L-2:** Missing event emission in earnSnow()
- **L-3:** Accidental ETH collection as fees

## Links
- [Contest Page](https://codehawks.cyfrin.io/c/2025-06-snowman-merkle-airdrop)
- [Repository](https://github.com/CodeHawks-Contests/2025-06-snowman-merkle-airdrop)
