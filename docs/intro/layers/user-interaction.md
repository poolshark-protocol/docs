# User Interaction

## 1.1 What It Does

This is the layer which users will interact with directly to perform any action of funds in regards to DCEX. It contains a set of Smart Contracts that, at their most basic level, provide a way for a user to emit a given event. In more advanced cases, it can be a hybrid contract, where an external user can interact with the liquidity inside DCEX directly, without having to perform a deposit or withdraw, while still emitting an event such that any changes can take effect in the database.

```js title="Basic Example" linenums="1" hl_lines="7"
function transfer(
    address transferToken,
    uint256 transferAmount,
    address receiver
) external override {
    address sender = msg.sender;
    emit TransferRequest(sender, transferToken, transferAmount, receiver);
}
```

## 1.2 Abstraction

## 1.3 User Functionality

## 1.4 Production Requirements
