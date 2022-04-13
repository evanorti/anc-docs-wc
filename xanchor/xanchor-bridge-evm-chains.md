# xAnchor Bridge (EVM Chains)

The xAnchor bridges on all EVM chains (Avalanche, Polygon, Ethereum, etc.) have the same interface and available methods:

## Functions

Keep in mind that unless otherwise specified, all token addresses refer to the address on the foreign (EVM) chain, _not_ the Terra chain.

### `depositStable`

```solidity
function depositStable(
	address token,
	uint256 amount
)
```

Deposits a stable coin (currently only wUST), and will exchange it for aUST after the operation has succeeded.

| Argument | Description                                                                          |
| -------- | ------------------------------------------------------------------------------------ |
| token    | Which stable coin to deposit (Currently, xAnchor only supports wormhole-wrapped UST) |
| amount   | Amount of stable coin to deposit                                                     |

### `redeemStable`

```solidity
function redeemStable(
	address token,
	uint256 amount
)
```

Swaps the amount of aUST specified for wUST.

| Argument | Description              |
| -------- | ------------------------ |
| token    | The address of the aUST  |
| amount   | Amount of aUST to redeem |

### `claimRewards`

```solidity
function claimRewards()
```

Claims any pending ANC rewards (e.g. from providing Liquidity to the ANC-UST pool, before token distribution was stopped). This will return wANC to the user.

### `lockCollateral`

```solidity
function lockCollateral(
	address token,
	uint256 amount
)
```

Send a collateral token to be locked in Anchor. This will subsequently allow the user to borrow against their collateral.

| Argument | Description                                                           |
| -------- | --------------------------------------------------------------------- |
| token    | The address of the token to be locked (e.g.: bLUNA, bETH, sAVAX, etc) |
| amount   | Amount of the collateral token that will be locked                    |

### `unlockCollateral`

```solidity
function unlockCollateral(
	bytes32 collateralTokenTerraAddress,
	uint128 amount
)
```

Unlock collateral from Anchor, and return it to the user’s wallet.

| Argument | Description                                                             |
| -------- | ----------------------------------------------------------------------- |
| token    | The address of the token to be unlocked (e.g.: bLUNA, bETH, sAVAX, etc) |
| amount   | Amount of the collateral token that will be unlocked                    |

### `borrowStable`

```solidity
function borrowStable(
	uint256 amount
)
```

Borrow stable coins (currently, wUST) against any collateral the user has previously locked within Anchor

| Argument | Description                 |
| -------- | --------------------------- |
| amount   | The amount of UST to borrow |

### `repayStable`

```solidity
function repayStable(
	address token,
	uint256 amount
)
```

Repay any loans, partially or fully. If the amount is in excess of the amount needed to fully repay the loan, the user must run the `withdrawAsset` function to retrieve the excess.

| Argument | Description                                                                 |
| -------- | --------------------------------------------------------------------------- |
| token    | The token that is used to repay the loan (currently, only wUST is accepted) |
| amount   | Amount of wUST to repay loan with                                           |

### `withdrawAsset`

```solidity
function withdrawAsset(
	string calldata token
)
```

Withdraw any assets that are present in the user’s Terra-side AddressProxy (Effectively, the user’s wallet on the Terra chain). Assets accrue here because of over repayment on loans, or in some cases, previously failed operations.

| Argument | Description                                                                                                |
| -------- | ---------------------------------------------------------------------------------------------------------- |
| token    | The address of the token that will be withdrawn. Note that this address is the Terra address of the token. |

### `processTokenTransferInstruction`

```solidity
function processTokenTransferInstruction(
	bytes memory encodedIncomingTokenTransferInfo,
  bytes memory encodedTokenTransfer
)
```

Process an incoming transfer, if a previous operation resulted in a returning token (e.g.: aUST returned from `depositStable`). The arguments passed must be the wormhole message VAA, and matching wormhole token transfer VAA.

| Argument                         | Description                                                                                                                                                                                                       |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| encodedIncomingTokenTransferInfo | The VAA of the Wormhole Token Transfer                                                                                                                                                                            |
| encodedTokenTransfer             | The VAA of the Wormhole Core Message, corresponding to the returning operation. This message also contains the sequence number of the token transfer, which is generally how the token transfer VAA is retrieved. |
