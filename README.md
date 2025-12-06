# 🛡️ Smart Contract Vulnerabilities by Jeet Pal

Welcome to my collection of real-world smart contract vulnerabilities that I discovered and responsibly disclosed. This repo acts as my public resume for smart contract security research [blog](https://medium.com/@jeetpal2007).

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

19. Unlimited mint-like behavior  
* The contract allows minting or tax manipulation in a way that simulates unlimited minting. This can inflate the token supply or allow the owner to extract disproportionate value.

20. No max tax fee limit  
* There is no upper bound on how high the tax fee can be set. A malicious owner could set this to 100% and trap user funds.

21. No Pausable Mechanism  
* The contract lacks a `pause()` function, which is useful during emergencies or when bugs are found.

22. No limit in `addBots()` – Denial of Service risk  
* The `addBots()` function has no cap, meaning a huge number of addresses can be added. This bloats storage and can break loops that iterate over this list.

23. Uncached `.length` in loops  
* Accessing dynamic array `.length` directly in loops increases gas. Cache it to reduce gas costs.

24. No slippage protection in swaps  
* The swapping mechanism doesn’t protect users from price manipulation. Slippage parameters should be introduced to avoid MEV or sandwich attacks.

25. Full centralization risk  
* Critical functions are fully controlled by the contract owner. Recommend implementing a multisig or governance structure.

26. Missing `ReentrancyGuard` in `swapAndSendFee()`  
* This function handles fund transfers but lacks protection against reentrancy attacks.

27. `manualSwap()` and `manualSend()` lack access control  
* These functions should be restricted. Right now, any user might be able to call them and interfere with fee mechanics.

28. Missing `Ownable2Step`  
* The contract uses traditional `Ownable`. Switch to `Ownable2Step` for safer ownership transfers.

29. No zero address check in `addBots()`  
* The function does not validate addresses, and the zero address can be added.

30. `sendETHToFee()` uses `.transfer()`  
* Using `.transfer()` is discouraged because of the 2300 gas stipend. Use `.call{value: amount}("")` instead.

31. No `require(amount > 0)` in transfers  
* Transfers with 0 amount should be reverted to prevent unnecessary gas waste or potential bugs.

32. `manualSend()` may send ETH to zero address  
* There’s no check that the recipient is valid. This could result in loss of funds.

33. `enableNewTax()` doesn’t emit previous value  
* Lacks event logging of old vs. new values, which reduces transparency in tax changes.

34. Should use `safeTransfer` / `safeApprove`  
* For ERC20 transfers, always use `safeTransfer()` or `safeApprove()` to avoid non-standard token issues.

35. No NatSpec comments  
* Code lacks Solidity NatSpec documentation which is useful for audits and formal verification.

36. Uses `SafeMath` in Solidity ^0.8.0  
* Not needed in Solidity 0.8.x and above. Redundant code increases contract size.

37. Uses `i++` instead of `++i` in loops  
* `++i` is slightly cheaper than `i++` in gas. Small optimizations matter in large loops.

38. Unsafe use of `_mint` instead of `_safeMint` in xyz.sol
* `_mint` function is used while miniting the NFT. This doesn't check for if the contract NFT receviable or not

39.Both block.prevrandao and block.timestamp are not reliably source of randonness
* This can be manupluated by miners

40.Improper Admin Address Validation and Missing Event in setTokenAdmin Function
* The contract doesn't validate the input for zero address and if address is same as current one and no event emit for this

41. Missing _disableInitializers() in FeeManager.sol
* The FeeManager contract is upgradeable and uses a proxy pattern with an initialize() function. While the initializer modifier ensures initialize() can only be called once per proxy instance, the implementation (logic) contract itself is not protected.

43. Incompatible ERC20 Handling – Non-Standard Tokens Like USDT Cause Liquidation Failure
* The function assumes all ERC20 tokens strictly follow the standard and return a boolean value on transfer(). Tokens like USDT, which omit the return value, cause this call to revert, breaking liquidation logic.

44.Fixed Hardcoded Data
* Pegged the token with other coin (1 BTC = 100 YC token) allow frontrunning when price fall or rise

45.No Slippage  protection 
* When selling the token there is no Slippage  protection allow attacker to inflate the shares values and booked loss for victim

46. No check for amount receive (protocol solvency)
* Some token demand on-chain fees allow less money -IN and  mint equal share


## Cario

47. [This contain code of all the finding in a cario contract](https://blog.blockmagnates.com/starknet-cairo-vulnerability-unused-function-72eb82fb4a10)
```
    fn main()->u8{  //This is main function it call very fist when the contract it deployed

let x:u8 = 5; //Variable declared with it type it is static type if you want you can deploy,not necessary but in audit it matter
let y:u8 = 10; //same as above
let z:u8 = 15; //same as above

println!("{}{}{}",x,y,z); //Here we have print the variable in cairo we have to use {} to print variable till now if the contract is deployed  over cario version 2 then it is .print() function
return add(x,y,z);  //Here the the return function call the add function and if you notice above there is u8 at main() function which defined the return type in cairo

}



fn add(a:u8,b:u8,c:u8) -> u8{ //Add function taking the variables and same returning a uint8 which is less then 256 there could be an Overflow or panic 
return a+b+c;  //here the function will return the variables sum but here we can use not retuns but we can use a+b+c not ";" required if it is end statement it will reduced the complexity.
}
```



  



> 🧠 *More vulnerabilities and research will be added regularly. Stay tuned!*  
> 🔗 *All issues responsibly disclosed and shared for educational purposes.*




  
