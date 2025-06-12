# 🛡️ Smart Contract Vulnerabilities by Jeet Pal

Welcome to my collection of real-world smart contract vulnerabilities that I discovered and responsibly disclosed. This repo acts as my public resume for smart contract security research.

## 🚀 About Me
I'm Jeet Pal (aka Mr. Mars Hacker), a smart contract auditor, bug bounty hunter, and Web3 security enthusiast.

Note: Codebase cannot be disclosed so I created myself  a smart contract to demonstrate the vulnerability

1. [Overflow](https://sepolia.etherscan.io/address/0x31ec903b1f8574321527817ab8a9facb79e817fb#code)
* Oveflow inside the `_OF` Function where the contract owner has'nt use the `safemath` for `uint`

2. [Unbounded loops conspumtion](https://sepolia.etherscan.io/address/0x31ec903b1f8574321527817ab8a9facb79e817fb#code)
* Here The contract is using a `dynamic array` Where user can input the many address and the amount which can caused the contract failure to work

3. [Use require](https://sepolia.etherscan.io/address/0x31ec903b1f8574321527817ab8a9facb79e817fb#code)
* while the array is there but the contract doesn't check for `require` statement allow different values for amount as well as address

4. [Using ++ for loops](https://sepolia.etherscan.io/address/0x31ec903b1f8574321527817ab8a9facb79e817fb#code)
* While the contract has loops which has `i++` for increament and decreament but here `i++` cost expensive then `++i` in the solodity and `--i` too (3 Extra gas for each round)

5. [Mapping not found](https://sepolia.etherscan.io/address/0x31ec903b1f8574321527817ab8a9facb79e817fb#code)
* Here in the contract the mapping of `_address` is not found . it is required for code security and efficeny

6. Safemath not required more in solidity `0.8.x`
* Here  contract use safemath in `0.8.x` which is not required since the solodity has in-built protection against overflow/underflow.

7. Unused code in the contract
* In contract there too many unnecessary state variable is declared that create the size of contract and gas to deployed to be high
 
8. [Floating pragma version](https://medium.com/@jeetpal2007/gas-level-vulnerability-floating-pragma-version-10a7741ab096)
* The contract should be on a fixed version in this case `0.8.17` not `0.8.0 > ^0.8.17` it could deployed contract on any version and may have OP codes vulnerability or complier bugs

9. [Fixed Hardcoded data](https://medium.com/@jeetpal2007/low-level-vulnerability-fixed-hardcoded-data-f0cc9b9d971f)
* using a fixed value for your token effect the pricing use the chainlink to feed the data on real time
 
10. Ownable 2 is newer version with more secure use that
* current contract use the ownable.sol for ownership. it is requested to used the ownable2.sol so the address won't change at wrong addresss it allow 2 step verification

11. misspelling of variable name
* There are many mis-spell function name like `TranferFrom` written as `Transferfrom`. Recommand to make the spelling right so no error can be thrown

12. Using vulnerable global variable for sensitive hash
* contract is using `block.timestamp / block.prevrandao`  for hash function these functions can be influence by miner

13. [Zero address check](https://osintteam.blog/smart-contract-funds-lost-due-to-missing-address-validation-80m-in-danger-a4ec7d823a3f?gi=8333c7000569)
* Contract it not verifing the address of the new withdraw function an victim can change his address to 0 address lead all funds to be freeze

14. CEI(Check effect Interactions pattern)
* It is recommanded to use the CEI on sensitive  functions such as withdrawal

15. Funds drain due to division before multiple
* the contract divide the interest before multiple it with the principle making the user to deposit low interest everytime

16. Contract is proxy and using `tranfer`
- `Tranfer` is not recommanded since `Tranfer` and `Send` take only 2300 Gas to forward insteasd this use `call`

17. [Using `tx.origin` for confirmation of owner](https://osintteam.blog/authentication-with-tx-origin-why-you-should-never-use-it-for-authorization-04d00846b901)
- Here the code `owner == tx.origin` Which will fail or even lead to unexpected behiover since it will verify if the wallet that has created this contract is equal to current caller

18. Signature relay
- The contract does not use any secret data to encode the borrower hash here an attacker can use this to other chain or replay the transaction .Use chain.id or nonce to fix this issue


  
