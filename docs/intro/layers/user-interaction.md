# User Interaction

## What It Does

This is the layer which users will interact with directly to perform any action of funds in regards to DCEX. It contains a set of Smart Contracts that, at their most basic level, provide a way for a user to emit a given event. In more advanced cases, it can be a hybrid contract, where an external user can interact with the liquidity inside DCEX directly, without having to perform a deposit or withdraw, while still emitting an event such that any changes can take effect in the database.

```solidity
function transfer(
    address transferToken,
    uint256 transferAmount,
    address receiver
) external override {
    address sender = msg.sender;
    emit TransferRequest(sender, transferToken, transferAmount, receiver);
}
```

## Abstraction

Since funds are being stored in a common contract between users, and funds can be spent by modules, we don't require certian EIPs to be used in the traditonal way (in all scenarios). Lets take for example an ERC20 transfer to your friend, a user with a wallet would call to the ERC20 contract's `transfer(address dest, uint256 amount)` method, in the processess consuming aprx. `29,000-65,000` gas.

In the case of a DCEX user who is to transfer an ERC20 token (internally), then they would call to the DCEX-ERC20-CORE contract's `transfer(address token, uint256 amount, address receiver)` method, consuming aprx. `24,000-26,000` gas. Since funds are local, there is no need to execute any more code on-chain, the event is fired off, and the [Ingestion Layer](http://localhost:8000/intro/layers/ingestion/) will handle updating the database of balances depending on if the call is valid or not.

Taking that example a level deeper, we can imagine a DCEX user interacting with a protocol via a Module, in this case GroupSwap. Instead of a user calling to the ERC20 contract's `approve()` method and the DEX contract's `swap` method, they can call to the relevant Module contract's `groupSwap()` function which will allow users to pool gas together through requests, where each request consumes aprx. `25,000-27,000` gas. The DCEX user doesn't need to perform an `approve()`, because the `groupSwap()` function calls to the Core contract's `reserveToken()` function. In this design, reservations can be seen as approvals, where a reservation is defined by a user calling to a module with a (most the time) predefined behaviour, the reservation is treated as a current and future holding of token, the user does not have access to token that is reserved, but in most cases the user has an option to stop the action, and thus closing the reservation and returning the user their tokens.

## User Functionality

Any actions a user will perform is through a contract call to the Core or any authorized Module. For info on active Modules and what each function does in detal, see the developer docs.

## Production Requirements

**AUDITS REQUIRED**

This layer should be production ready; there are not any major differences between these contracts and any other protocol's contracts'.