# 💡OrderBook Audit - Learnings

## Summary
This audit focused on a peer-to-peer ERC20 token trading system. The main findings were CEI (Checks-Effects-Interactions) pattern violations and incomplete access control protections.
A few of the findings were invalid, while a few probably were a little too imaginative, but nontheless possible. 

Overal I learned a lot. 

## Findings

### createSellOrder()
**Issue:** CEI violation - external call (`safeTransferFrom`) before state updates, enabling potential reentrancy attacks.  
**Learning:** While the vulnerability is technically valid, judges may reject it under "trusted owner" assumptions if malicious tokens are unlikely to be whitelisted.
I was making a hypothetical the owner could be phished as the function is called a lot and phishing does happen (it happened to me!). 

### amendSellOrder()  
**Issue:** CEI violation - external calls for token adjustments before state updates, similar reentrancy risk as createSellOrder.  
**Learning:** Same technical issue but judges applied consistent "malicious tokens won't be allowed and trusted owner" reasoning across all similar CEI violations.
Again, I was making a hypothetical the owner could be phished as the function is called a lot and phishing does happen (it happened to me!). 

### buyOrder()
**Issue:** CEI violation - multiple external calls before `totalFees` update, plus confusion about attack vectors in our submission.  
**Learning:** We focused too heavily on malicious USDC rather than malicious sell tokens, making our submission confusing and weakening the argument.

### withdrawFees()
**Issue:** CEI violation - external call before resetting `totalFees`, enabling potential fee drainage.  
**Learning:** Even though technically valid, judges applied "trusted owner" assumption - owners wouldn't send fees to malicious contract recipients.

### emergencyWithdrawERC20()
**Issue:** Incomplete protection - only protects 4 hardcoded tokens, not dynamically whitelisted tokens via `setAllowedSellToken()`.  
**Learning:** This represents a logic gap rather than malicious actor scenario - trusted owner could accidentally drain user funds from newly supported tokens.


## Key Takeaways

1. **CEI Violations Are Real But Context Matters:** Technical vulnerabilities exist, but judges weigh practical exploitability heavily based on threat model assumptions.

2. **"Trusted Owner" Assumptions:** Many audit contexts assume protocol owners are trustworthy, significantly reducing likelihood of owner-dependent attacks.

3. **Submission Clarity Is Crucial:** Our buyOrder submission was confusing because we mixed attack vectors (malicious USDC vs. malicious sell tokens), weakening an otherwise valid finding.

4. **Logic Gaps vs. Malicious Actors:** The emergency withdraw issue is stronger because it represents a design flaw rather than requiring malicious actors.

5. **Appeal Strategy:** Focus on technical correctness and code quality rather than elaborate attack scenarios when likelihood is disputed.

## What We'd Do Differently

- Emphasize CEI violations as code quality issues regardless of exploitability
- Clearer threat modeling in submissions (one attack vector per submission)
- Better likelihood assessment based on realistic scenarios
- Focus on design flaws over elaborate social engineering scenarios

## Conclusion

While several submissions were invalidated, the analysis identified real technical issues in the codebase. The main learning is that audit findings must balance technical correctness with practical risk assessment under realistic threat models.
