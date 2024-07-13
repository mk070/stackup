# Introduction

## Protocol Name: 
Uniswap

## Category: 
DeFi

## Smart Contract: 
UniswapV2Router02

# Function Analysis

## Function Name: 
swapExactTokensForTokens

## Block Explorer Link: 
https://etherscan.io/address/0x7a250d5630b4cf539739df2c5dacb4c659f2488d#code

## Function Code: 
```
function swapExactTokensForTokens(
    uint amountIn,
    uint amountOutMin,
    address[] calldata path,
    address to,
    uint deadline
) external ensure(deadline) returns (uint[] memory amounts) {
    amounts = UniswapV2Library.getAmountsOut(factory, amountIn, path);
    require(amounts[amounts.length - 1] >= amountOutMin, 'UniswapV2Router: INSUFFICIENT_OUTPUT_AMOUNT');
    TransferHelper.safeTransferFrom(
        path[0], msg.sender, UniswapV2Library.pairFor(factory, path[0], path[1]), amounts[0]
    );
    _swap(amounts, path, to);
}
```

## Used Encoding/Decoding or Call Method: 
abi.encodeWithSignature

# Explanation

## Purpose
The function allows users to swap an exact amount of input tokens for as many output tokens as possible, ensuring the output amount is above a specified minimum.

## Detailed Usage
The function internally calls another contract function using abi.encodeWithSignature to pass encoded function signatures and parameters. This method ensures that the correct function with the appropriate parameters is called on another contract.

## Impact
This function is crucial for enabling token swaps on Uniswap, contributing to the protocol’s functionality by facilitating decentralized exchange operations.

