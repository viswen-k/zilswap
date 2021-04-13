# SDK

A TypeScript SDK to easily integrate your dApp with Zilswap can be found at [https://github.com/Switcheo/zilswap-sdk](https://github.com/Switcheo/zilswap-sdk).

This SDK allows integrators to easily interface with the Zilswap smart contract without needing to do conversions between human and unitless numbers.

## Setup

Install from npm:
`npm install zilswap-sdk`

SDK Initialisation based on the required network: 
```ts
  import { Zilswap } from 'zilswap-sdk'

  (async () => {
    const zilswap = new Zilswap(Network.TestNet)
    await zilswap.initialize()
    // Method Calls
    await zilswap.teardown()
  })()
```

## Methods

 It also provides a set of getters to retrieve and monitor the Zilswap smart contract state.

### `getAppState()` - Gets the latest Zilswap app state

**Returns:** *[AppState](https://github.com/Switcheo/zilswap-sdk/blob/master/doc/modules/_index_.md#appstate)*
___
### `getPool(tokenID)` - Gets the pool details for the given tokenID

**Parameters:**
Name | Type | Description |
------ | ------ | ------ |
`tokenID` | string | is the token ID for the pool, which can be given by either it's symbol (defined in constants.ts), hash (0x...) or bech32 address (zil...). |

**Returns:** *[Pool](https://github.com/Switcheo/zilswap-sdk/blob/master/doc/modules/_index_.md#pool) | null*
if pool exists, or `null` otherwise.
___
### `getObservedTxs()` - Gets the currently observed transactions

**Returns:** *Promise‹[ObservedTx](../modules/_index_.md#observedtx)[]›*
___
Finally, it provides exchange rate calculations and converts limits and thresholds from a human understandable input into the format that the Zilswap smart contract requires.

### `toUnitless(tokenID, humanAmount)`  - Converts an amount to it's unitless representation from it's human representation 

**Parameters:**
Name | Type | Description |
------ | ------ | ------ |
`tokenID` | string | is the token ID related to the conversion amount, which can be given by either it's symbol (defined in constants.ts), hash (0x...) or bech32 address (zil...). The hash for ZIL is represented by the ZIL_HASH constant. |
`amountHuman` | string | is the amount as a human string (e.g. 4.2 for 4.2 ZILs) to be converted.  |

**Returns:** *string*
___
### `toUnit(tokenID, amountStr)`  - Converts a unitless integer used by scilla into a human readable amount.
  
**Parameters:**
Name | Type | Description |
------ | ------ | ------ |
`tokenID` | string | is the token ID related to the conversion amount, which can be given by either it's symbol (defined in constants.ts), hash (0x...) or bech32 address (zil...). The hash for ZIL is represented by the ZIL_HASH constant. |
`amountStr` | string | is the unitless amount as a string (e.g. 42000000000000 for 42 ZILs) to be converted.  |

**Returns:** *string*
___
### `getRatesForInput`  - Gets the expected output amount and slippage for a particular set of ZRC-2 or ZIL tokens at the given input amount

**Parameters:**
Name | Type | Description |
------ | ------ | ------ |
`tokenInID` | string | is the token ID to be sent to Zilswap (sold), which can be given by either it's symbol (defined in constants.ts), hash (0x...) or bech32 address (zil...). The hash for ZIL is represented by the ZIL_HASH constant. |
`tokenOutID` | string | is the token ID to be taken from Zilswap (bought), which can be given by either it's symbol (defined in constants.ts), hash (0x...) or bech32 address (zil...). The hash for ZIL is represented by the ZIL_HASH constant. |
`tokenInAmountStr` | string | is the exact amount of tokens to be sent to Zilswap as a unitless representable string (without decimals).  |

**Returns:** *[Rates](https://github.com/Switcheo/zilswap-sdk/blob/master/doc/modules/_index_.md#rates)*
___
### `getRatesForOutput`  - Gets the expected input amount and slippage for a particular set of ZRC-2 or ZIL tokens at the given output amount. Returns NaN values if the given output amount is larger than the pool reserve.

**Parameters:**
Name | Type | Description |
------ | ------ | ------ |
`tokenInID` | string | is the token ID to be sent to Zilswap (sold), which can be given by either it's symbol (defined in constants.ts), hash (0x...) or bech32 address (zil...). The hash for ZIL is represented by the ZIL_HASH constant. |
`tokenOutID` | string | is the token ID to be taken from Zilswap (bought), which can be given by either it's symbol (defined in constants.ts), hash (0x...) or bech32 address (zil...). The hash for ZIL is represented by the ZIL_HASH constant. |
`tokenOutAmountStr` | string | is the exact amount of tokens to be received from Zilswap as a unitless representable string (without decimals).  |

**Returns:** *[Rates](https://github.com/Switcheo/zilswap-sdk/blob/master/doc/modules/_index_.md#rates)*
