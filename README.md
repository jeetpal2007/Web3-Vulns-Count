# 🛡️ Smart Contract Vulnerabilities by Jeet Pal

Welcome to my collection of real-world smart contract vulnerabilities that I discovered and responsibly disclosed. This repo acts as my public resume for smart contract security research.

## 🚀 About Me
I'm Jeet Pal (aka Mr. Mars Hacker), a smart contract auditor, bug bounty hunter, and Web3 security enthusiast.

Note: Codebase cannot be disclosed so I created myself  a smart contract to demonstrate the vulnerability
- [Overflow](https://sepolia.etherscan.io/address/0x31ec903b1f8574321527817ab8a9facb79e817fb#code)
* Oveflow inside the `_OF` Function where the contract owner has'nt use the `safemath` for `uint`

- [Unbounded loops conspumtion](https://sepolia.etherscan.io/address/0x31ec903b1f8574321527817ab8a9facb79e817fb#code)
* Here The contract is using a `dynamic array` Where user can input the many address and the amount which can caused the contract failure to work

- [No require](https://sepolia.etherscan.io/address/0x31ec903b1f8574321527817ab8a9facb79e817fb#code)
* while the array is there but the contract doesn't check for `require` statement allow different values for amount as well as address

- [Using ++ for loops](https://sepolia.etherscan.io/address/0x31ec903b1f8574321527817ab8a9facb79e817fb#code)
* While the contract has loops which has `i++` for increament and decreament but here `i++` cost expensive then `++i` in the solodity and `--i` too (3 Extra gas for each round)

- [Mapping not found](https://sepolia.etherscan.io/address/0x31ec903b1f8574321527817ab8a9facb79e817fb#code)
* Here in the contract the mapping of `_address` is not found . it is required for code security and efficeny

