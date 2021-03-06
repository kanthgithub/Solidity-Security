# Solidity-Security

## How to write safe smart-contracts in solidity:

### References:

- http://chriseth.github.io/notes/talks/safe_solidity/#/
- https://blog.ethereum.org/2016/06/10/smart-contract-security/
- https://blog.ethereum.org/2016/06/19/thinking-smart-contract-security/
- http://solidity.readthedocs.io/en/latest/security-considerations.html

### Vulnerabilities:

- https://cryptoservices.github.io/fde/2018/05/01/Ethereum-top10.html
- https://cryptoservices.github.io/

### Design patterns For Secure Smarrt-Contracts:

- Checks-Effects-Interactions Pattern

  - https://solidity.readthedocs.io/en/develop/security-considerations.html?highlight=check%20effects#use-the-checks-effects-interactions-pattern
  
  
  - Avoid state changes after external calls

     - Whether using raw calls (of the form someAddress.call()) or contract calls (of the form ExternalContract.someMethod()), assume that malicious code might execute. Even if ExternalContract is not malicious, malicious code can be executed by any contracts it calls.

    - One particular danger is malicious code may hijack the control flow, leading to vulnerabilities due to reentrancy. (See Reentrancy for a fuller discussion of this problem).

    - If you are making a call to an untrusted external contract, avoid state changes after the call. This pattern is also sometimes known as the checks-effects-interactions pattern.

    -  Most functions will first perform some checks (who called the function, are the arguments in range, did they send enough Ether, does the person have tokens, etc.). These checks should be done first.

    - As the second step, if all checks passed, effects to the state variables of the current contract should be made. Interaction with other contracts should be the very last step in any function.

    - Early contracts delayed some effects and waited for external function calls to return in a non-error state. This is often a serious mistake because of the re-entrancy problem explained above.

    - Note that, also, calls to known contracts might in turn cause calls to unknown contracts, so it is probably better to just always apply this pattern.
