# SimpleSwap

A minimal, self-contained clone of the core mechanics of **Uniswap V2**, aimed at study, testing, and front-end integration demos.  
**⚠️ For educational use only — do not deploy to mainnet.**

---

## Index
1. [Overview](#overview)  
2. [Architecture](#architecture)  
3. [Getting Started](#getting-started)  
4. [Contract Interface](#contract-interface)  
5. [Front-End Integration](#front-end-integration)  
6. [Author](#author)  
7. [License](#license)

---

## Overview

`SimpleSwap.sol` bundles the essential liquidity-pool logic:

| Function                   | Purpose                                                                                       |
| -------------------------- | --------------------------------------------------------------------------------------------- |
| `addLiquidity`             | Deposit *token A* + *token B*, mint LP tokens.                                                |
| `removeLiquidity`          | Burn LP tokens, withdraw proportional *token A* + *token B*.                                  |
| `swapExactTokensForTokens` | Swap a fixed input amount for the maximum possible output, enforcing `amountOutMin`.          |
| `getPrice`                 | View-only spot price (`reserveA / reserveB`, scaled to 18 decimals).                          |
| `getAmountOut`             | Pure helper: constant-product formula (no fees in this demo).                                 |

---

`SimpleSwap` inherits `TokenFactory.sol`, which deploys **two ERC-20 test tokens** (with `mint` / `burn`) so you can simulate any pool scenario without external dependencies.

---





## Contract Interface

```solidity
/// @notice Add liquidity and mint LP tokens.
function addLiquidity(
    address tokenA,
    address tokenB,
    uint256 amountADesired,
    uint256 amountBDesired,
    uint256 amountAMin,
    uint256 amountBMin,
    address to,
    uint256 deadline
) external returns (uint256 amountA, uint256 amountB, uint256 liquidity);

/// @notice Burn LP tokens and withdraw underlying tokens.
function removeLiquidity(
    address tokenA,
    address tokenB,
    uint256 liquidity,
    uint256 amountAMin,
    uint256 amountBMin,
    address to,
    uint256 deadline
) external returns (uint256 amountA, uint256 amountB);

/// @notice Swap exact input for output, enforcing minimum output.
function swapExactTokensForTokens(
    uint256 amountIn,
    uint256 amountOutMin,
    address[] calldata path, // [tokenIn, tokenOut]
    address to,
    uint256 deadline
) external;

/// @notice View spot price (reserveA / reserveB).
function getPrice(
    address tokenA,
    address tokenB
) external view returns (uint256 price);

/// @notice Calculate output amount given input and reserves.
function getAmountOut(
    uint256 amountIn,
    uint256 reserveIn,
    uint256 reserveOut
) external pure returns (uint256 amountOut);
```

ABIs are generated at `artifacts/contracts/SimpleSwap.sol/SimpleSwap.json`.

---

## Deployment Information

- **Network**: Sepolia (chainId 11155111)  
- **Contract Address**: `0xf939C0CCe76f4a3d52127E7D20c0eB73fB79Eda1`

---

## Author

**Einarmig**  


---

## License

MIT — see [`LICENSE`](LICENSE).
