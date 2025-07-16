# 📚 Panoptic HypoVault Audit

**Platform:** Code4Arena  
**Duration:** June 27 - July 7, 2025  
**Prize Pool:** $18,000 USDC  
**Language:** Solidity  

## About

[Panoptic](https://panoptic.xyz/) is a DeFi options protocol that enables permissionless trading of options on top of Uniswap v3 pools. This audit focused on their new HypoVault implementation - an asynchronous vault system where managers allocate deposited assets and distribute profits through epochs.

## Scope

| Contract | SLOC | Description |
|----------|------|-------------|
| HypoVault.sol | 272 | Main vault with epoch-based deposit/withdrawal system |
| PanopticVaultAccountant.sol | 172 | NAV computation from Panoptic positions |

## Results

- **High Severity:** 2 findings
- **Medium Severity:** 0 findings  
- **Focus Areas:** Vault accounting, manager operations, state transitions

## Findings

📋 **[View Detailed Findings](findings.md)**

### Summary
- **H-1:** Reserved assets underflow attack causing user fund loss
- **H-2:** Reentrancy vulnerability in manager functions

## Links

- [Contest Page](https://code4rena.com/audits/2025-06-panoptic-hypovault)
- [Panoptic Protocol](https://panoptic.xyz/)
- [Repository](https://github.com/code-423n4/2025-06-panoptic)
