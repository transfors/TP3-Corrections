# TP3-Corrections
Implementation of SimpleSwap

🚀 SimpleSwap
📄 Description

SimpleSwap is a minimal Solidity smart contract implementing a two-token liquidity pool for swapping and liquidity management. It allows users to:

    ➕ Add liquidity by depositing two ERC-20 tokens in proportion.
    ➖ Remove liquidity to redeem their share of the tokens.
    🔄 Swap one token for the other using an automated market maker (AMM) model.
    📊 Query the current price of one token in terms of the other.

This contract is a simple educational example of how AMMs like Uniswap work internally.
🛠️ Token and Contract Addresses
Name	Address
TokenA	0x843095CaA1702bb64f708C3B3781d8F4d89a72C6
TokenB	0x1e8741Bf6d1469075d03f23dEbCBb5584FD2a9Cc
SimpleSwap	0xb4fAe6D1359AeFE4C24C5B7bAE08e4d55C9bd745

✨ Main Features
➕ Add Liquidity (addLiquidity)

Allows a user to deposit two tokens into the pool and mint liquidity tokens representing their share.

    Calculates optimal token amounts based on current reserves.
    Updates internal reserves accordingly.
    Emits a LiquidityAdded event.

➖ Remove Liquidity (removeLiquidity)

Allows a user to burn liquidity tokens and withdraw their proportional share of tokens.

    Calculates amounts to withdraw based on pool share.
    Updates reserves.
    Emits a LiquidityRemoved event.

🔄 Swap Tokens (swapExactTokensForTokens)

Swaps an exact input amount of one token for a minimum output amount of the other.

    Applies a 0.3% fee on swaps.
    Updates reserves after the swap.
    Emits a TokensSwapped event.
    Protects against excessive slippage.

📊 Get Price (getPrice)

Returns the current price of one token in terms of the other, based on reserves.
📢 Events

    LiquidityAdded: emitted when liquidity is added.
    LiquidityRemoved: emitted when liquidity is removed.
    TokensSwapped: emitted when tokens are swapped.

🔒 Security

    Uses OpenZeppelin’s ReentrancyGuard to prevent reentrancy attacks.
    Validates token addresses and deadlines.
    Enforces transaction deadlines with the ensure modifier.

🔗 Interfaces

The contract interacts with standard ERC-20 tokens using OpenZeppelin's IERC20 interface.
🧑‍💻 Basic Usage Example

// Add liquidity example:

simpleSwap.addLiquidity(

    tokenA,
    tokenB,
    100 ether,           // desired amount of tokenA
    200 ether,           // desired amount of tokenB
    90 ether,            // minimum amount of tokenA (slippage)
    180 ether,           // minimum amount of tokenB (slippage)
    msg.sender,          // recipient of liquidity tokens
    block.timestamp + 600 // deadline (10 minutes)

);

// Swap tokens example:

address ;
path[0] = tokenA;
path[1] = tokenB;

simpleSwap.swapExactTokensForTokens(

    10 ether,            // amount of tokenA to swap
    9 ether,             // minimum amount of tokenB to receive (slippage)
    path,
    msg.sender,
    block.timestamp + 600

);

ℹ️ Notes

    This contract manages a fixed token pair defined at deployment.
    Liquidity shares are tracked internally, no separate liquidity token contract.
    Swap fee is fixed at 0.3%.
    Users must approve token spending before calling addLiquidity or swapExactTokensForTokens.

⚙️ Requirements

    Solidity version 0.8.27
    Standard ERC-20 tokens deployed
    OpenZeppelin contracts for interfaces and security

👤 Author

Nelly Herrero

