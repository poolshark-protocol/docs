A queue of orders which enforces price-time priority fills.

Each `Page` is a price tick that contains a collection of orders.

`Offsets` are used to track which maker orders have been filled.

## Functions

### getPagePrice

```solidity
    function getPagePrice(
        address takerToken,
        uint256 takerAmount,
        uint256 makerAmount
    ) public view returns (uint256 pagePrice)
```

Returns the `pagePrice` given the token being swapped in as well as the `takerAmount` and `makerAmount`.

** Parameters: **

| Name        | Type  | Description                 |
| :---------- | :---- | :-------------------------- |
| `takerToken`  | address | The token being swapped in |
| `takerAmount` | uint256 | The amount of the token swapped in or received by the liquidity provider |
| `makerAmount` | uint256 | The amount of the token swapped into or provided by the liquidity provider |

** Return Values: **

| Name                            | Type    | Description                                         |
| :------------------------------ | :------ | :-------------------------------------------------- |
| `pagePrice`          | uint256  | the value of the page price based on the input amounts  |

### getPageKey

```solidity
    function getPageKey(
        address takerToken,
        uint256 takerAmount,
        uint256 makerAmount
    ) public view returns (bytes32)
```

Returns the `pageKey` given the token being swapped in (i.e. `takerToken`) as well as the `takerAmount` and `makerAmount`.

** Parameters: **

| Name        | Type  | Description                 |
| :---------- | :---- | :-------------------------- |
| `takerToken`  | address | The token being swapped in |
| `takerAmount` | uint256 | The amount of the token swapped in or received by the liquidity provider |
| `makerAmount` | uint256 | The amount of the token swapped into or provided by the liquidity provider |

** Return Values: **

| Name                            | Type    | Description                                         |
| :------------------------------ | :------ | :-------------------------------------------------- |
| `pageKey`          | bytes32  | the key in the `pages` mapping used to lookup the `Page` |

### getOrderKey

```solidity
    function getOrderKey(
        address owner,
        bytes32 pageKey,
        uint256 endOffset
    ) public pure returns (bytes32)
```

Returns the `orderKey` given the `owner` address as well as the `pageKey` and `endOffset`.

** Parameters: **

| Name        | Type    | Description                                     |
| :---------- | :------ | :---------------------------------------------- |
| `owner`     | address | The token being swapped in                      |
| `pageKey`   | uint256 | The page key for which the `Order` is linked to |
| `endOffset` | uint256 | The offset representing the end of the `Order`  |

** Return Values: **

| Name                            | Type    | Description                                         |
| :------------------------------ | :------ | :-------------------------------------------------- |
| `orderKey`          | bytes32  | the key in the `orders` mapping used to lookup the `Order` |

### limitOrder

```solidity
    function limitOrder(
        address fromToken,
        uint256 fromAmount,
        uint256 destAmount,
        uint256 limitPrice,
        bool makerOnly,
        bool takerOnly
    ) public returns (uint256 fromAmountIn, uint256 destAmountOut)
```

Executes or creates a limit order. If `makerOnly` is set to `true`, liquidity will be added to the book to collect fees from swappers. If `takerOnly` is set to `true`, liquidity will only be taken from the book (i.e. normal `swap` call).

Note: a token `approve()` call required prior with the amount `fromAmount`. 

** Parameters: **

| Name        | Type    | Description                                    |
| :---------- | :------ | :--------------------------------------------- |
| `fromToken` | address | The address of the token being swapped in      |
| `fromAmount`| uint256 | The max amount of `fromToken` to be spent      |
| `destAmount`| uint256 | The max of `destToken` to be received          |
| `limitPrice`| uint256 | The max `pagePrice` to pull liquidity from     |
| `makerOnly` | bool    | Default false; set true to force liquidity add |
| `takerOnly` | bool    | Default false; set true to force liquidity swap|

** Return Values: **

| Name                            | Type    | Description                                         |
| :------------------------------ | :------ | :-------------------------------------------------- |
| `fromAmountIn`  | uitn256  | the amount of `fromToken` transferred into the contract |
| `destAmountOut` | uitn256  | the amount of `destToken` transferred to the recipient  |

### claimOrders

```solidity
    function claimOrders(
        uint256[] memory pagePrices,
        uint256[] memory endOffsets,
        address[] memory takerTokens,
        uint256[] memory amounts
    ) external 
```

Claims an executed limit order(s). If `amount` is greater than the actual amount in the order, the entire amount will be claimed.

** Parameters: **

| Name         | Type      | Description                                     |
| :----------- | :-------- | :---------------------------------------------- |
| `pagePrices` | uint256[] | An array of `pagePrice` values for the orders being claimed |
| `endOffsets` | uint256[] | The page key for which the `Order` is linked to |
| `amounts`    | uint256[] | The offset representing the end of the `Order`  |

** Return Values: **

| Name                            | Type    | Description                                         |
| :------------------------------ | :------ | :-------------------------------------------------- |
| `amountsCancelled`  | uint256[]  | the amount of `takerToken` transferred back to the recipient |

### cancelOrders

```solidity
    function cancelOrders(
        bytes32[] pageKey,
        uint256[] endOffset,
        uint256[] amount
    ) public returns (uint256[] amountsCancelled)
```

Cancels an existing limit order(s). If `amount` is greater than the actual amount in the order, the entire order will be cancelled. 

Note: If the amount left in the order would be less than the `makerTier`, the minimum order size, the order will remain unmodified.

** Parameters: **

| Name         | Type      | Description                                     |
| :----------- | :-------- | :---------------------------------------------- |
| `pageKeys`   | address[] | The page keys of the orders being cancelled     |
| `endOffsets` | uint256[] | The end offset of each `Order` being cancelled  |
| `amounts`    | uint256[] | The amounts being cancelled from each `Order`   |

** Return Values: **

| Name                            | Type    | Description                                         |
| :------------------------------ | :------ | :-------------------------------------------------- |
| `amountsCancelled`  | uint256[]  | the amount of `makerToken` transferred back to the recipient |

### quoteExactAmountOut

```solidity
    function quoteExactAmountOut(
        address fromToken,
        uint256 fromAmount,
        uint256 limitPrice
    ) public view returns (uint256 fromAmountIn, uint256 destAmountOut)
```

Gives a quote based on the `fromAmount` desired and the liquidity in the book.

Liquidity will be checked up to and including the specified `limitPrice`.

** Parameters: **

| Name         | Type    | Description                                            |
| :----------- | :------ | :----------------------------------------------------- |
| `fromToken`  | address | The token that would be passed in for a swap           |
| `fromAmount` | uint256 | The amount of `fromToken` that would be transferred in |
| `limitPrice` | uint256 | The `pagePrice` value to swap up to                    |

** Return Values: **

| Name                            | Type    | Description                                         |
| :------------------------------ | :------ | :-------------------------------------------------- |
| `fromAmountIn`  | uitn256  | the amount of `fromToken` that can be transferred into the contract  |
| `destAmountOut` | uitn256  | the amount of `destToken` that will be transferred to the recipient |

### quoteExactAmountIn

```solidity
    function quoteExactAmountIn(
        address destToken,
        uint256 destAmount,
        uint256 limitPrice
    ) public view returns (uint256 fromAmountIn, uint256 destAmountOut)
```

Gives a quote based on the `destAmount` desired and the liquidity in the book.

Liquidity will be checked up to and including the specified `limitPrice`.

** Parameters: **

| Name         | Type    | Description                                            |
| :----------- | :------ | :----------------------------------------------------- |
| `destToken`  | address | The token that would be received from a swap           |
| `destAmount` | uint256 | The amount of `destToken` that would be transferred in |
| `limitPrice` | uint256 | The `pagePrice` value to swap up to                    |

** Return Values: **

| Name                            | Type    | Description                                         |
| :------------------------------ | :------ | :-------------------------------------------------- |
| `fromAmountIn`  | uitn256  | the amount of `fromToken` that can be transferred into the contract  |
| `destAmountOut` | uitn256  | the amount of `destToken` that will be transferred to the recipient |
