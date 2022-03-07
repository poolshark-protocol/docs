# Core

The core provides the base functionality required by the protocol, plus extra functions that can be utilized by modules to optimize gas usage, while still providing a full feature set of asset management.


## User Functions
### deposit()
Allows users to transfer an ERC20 token or the network token into the contract and assigns the `#!solidity msg.sender` the relevant balance

??? code-preview "Code Preview"
    ```solidity
    function deposit(
        IERC20 depositToken,
        uint256 depositAmount
    ) external payable override {
        address user = msg.sender;
        if (!depositToken.isETH() && msg.value > 0) {
            emit Deposit(user, IERC20(ETH), msg.value);
        }
        if (address(depositToken) != address(0)) {
            depositToken.universalTransferFrom(msg.sender, address(this), depositAmount);
            emit Deposit(user, depositToken, depositAmount);
        }
    }
    ```
### requestWithdraw()
Gives users access to withdraw their unreserved tokens inside the DCEX contract to any address. This function is set as a request so the data being passed into the function call can be validated to the user, i.e. making sure the user owns the amount of token that they are wanting to withdraw.
??? event-preview "Event Preview"
    ```solidity
    event WithdrawRequest(
        address indexed user,
        address indexed withdrawToken,
        uint256 withdrawAmount,
        address indexed withdrawAddress
    );
    ```
### transfer()
Allows users to transfer their tokens to any address inside the DCEX contract, supports non-existant users, allows for someone to generate an account without having to perform a deposit. Is processed as a request so that the amounts can be validated for the same reason of withdraw being a request function.
??? event-preview "Event Preview"
    ```solidity
    event TransferRequest(
        address indexed sender,
        address indexed transferToken,
        uint256 transferAmount,
        address indexed receiver
    );
    ```


## Module Functions
### contractCall()
### mintTokenByUser()
### burnTokenByUser()
### burnTokenByReservation()
### mintTokenByKeyEven()
### mintTokenByKeyUntil()
### mintTokenByKeyEvenPartial()
### burnTokenByKeyEven()
### burnTokenByKeyUntil()
### reserveToken()
### unreserveToken()
### authorizedTransfer()


## Admin Functions
### updateModule()


## Gelato Functions
### finalizeWithdraws()