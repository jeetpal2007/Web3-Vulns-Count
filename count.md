# 🛡️ Smart Contract Vulnerabilities by Jeet Pal

Welcome to my collection of real-world smart contract vulnerabilities that I discovered and responsibly disclosed. This repo acts as my public resume for smart contract security research.

## 🚀 About Me
I'm Jeet Pal (aka Mr. Mars Hacker), a smart contract auditor, bug bounty hunter, and Web3 security enthusiast.

Note: Codebase cannot be disclosed so I created myself  a smart contract to demonstrate the vulnerability

# Unbounded Gas consumption

Here The contract is using a `dynamic array` Where user can input the many address and the amount which can caused the contract failure to work

```

```

# Overflow (CTF)
Oveflow inside the `useradd` Function where the contract owner has'nt use the safemath for uint


```
function useradd(uint8 _value1) public    returns (uint8, string memory) {
    uint8 _result = _value1 + 255;
    if (_result == 255) {
         emit Complete(msg.sender, block.timestamp);
        return (_result, "You won");
    } else {
        return (_result, "Try again You havn't won the whole thing");
    }
    
}
```
