# 📚 OrderBook Audit

**Platform:** CodeHawks  
**Duration:** July 2025  
**Language:** Solidity  

## About

The OrderBook contract is a peer-to-peer trading system designed for ERC20 tokens like wETH, wBTC, and wSOL. Sellers can list tokens at their desired price in USDC, and buyers can fill them directly on-chain with deadline enforcement and order management capabilities.

## Scope

| Contract | SLOC | Description |
|----------|------|-------------|
| OrderBook.sol | ~400 | Main P2P trading contract with order creation, amendment, and execution |

## Results

- **High Severity:** 5 findings
- **Medium Severity:** 0 findings  
- **Focus Areas:** CEI pattern violations, reentrancy vulnerabilities, fund protection mechanisms

## Findings

📋 **[View Detailed Findings](findings.md)**

### Summary
- **H-1:** CEI Pattern Violation in createSellOrder() Enables Reentrancy Attacks
- **H-2:** CEI Pattern Violation in amendSellOrder() Enables Reentrancy Attacks  
- **H-3:** CEI Pattern Violation in buyOrder() Enables Reentrancy and Fee Manipulation
- **H-4:** CEI Pattern Violation in withdrawFees() Enables Protocol Fee Drainage via Reentrancy
- **H-5:** Incomplete Protection in emergencyWithdrawERC20() Allows Drainage of User-Deposited Tokens

## Links

- [Repository](https://github.com/code-423n4/orderbook-audit-codehawks)
```
