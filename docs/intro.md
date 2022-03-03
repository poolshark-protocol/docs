# Intro to DCEX

## Layers

The design consists of 6 seperate layers, all intended to work together in an attempt to provide a fully decentralized execution loop, reduce user consumed gas, and present new ways to perform complex and costly tasks by utilizing code execution off-chain

## 1. User Interaction

#### 1.1 What It Does

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

#### 1.2 Abstraction

#### 1.3 User Functionality

#### 1.4 Production Requirements

## 2. Data Ingestion

#### 2.1 What It Does

#### 2.2 Abstraction

#### 2.3 Production Requirements

## 3. Database

#### 3.1 What It Does

#### 3.2 Abstraction

#### 3.3 User Functionality

#### 3.4 Production Requirements

## 4. Database Query

#### 4.1 What It Does

#### 4.2 Abstraction

#### 4.3 User Functionality

#### 4.4 Production Requirements

## 5. Execution

#### 5.1 What It Does

#### 5.2 Abstraction

#### 5.3 User Functionality

#### 5.4 Production Requirements

## 6. Trustless Code Storage

#### 6.1 What It Does

```

```
