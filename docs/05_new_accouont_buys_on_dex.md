# 5.New account buys on dex.

Through the liquidity pool, listed tokens can be purchased by other accounts.

- Create another account.
```
$ liquidityd keys add dity[your favorite name]
```

Don't forget to faucet the listed pair of tokens.

- Requesting a Swap
```
$ liquidityd tx liquidity swap 2 1 1000uatom ibc/37075C5B491066D41670D8235351E49EBE84069CBBDDB5EE607E6B733F3DD04B 1 0.003 --from dity --node http://13.248.175.68:80 --gas-prices 0.01uatom --gas auto --gas-adjustment 1.3 --chain-id swap-testnet-2002

```

It is recommended to refer to the following for more information about these parameters.

https://github.com/tendermint/liquidity/blob/develop/doc/client.md#tx-swap


- Verify that the swap request is successful.
```
$ liquidityd query liquidity batch 2 --node http://13.248.175.68:80
batch:
  begin_height: "38875"
  deposit_msg_index: "1"
  executed: false
  index: "1"
  pool_id: "2"
  swap_msg_index: "2"
  withdraw_msg_index: "1"
```

This Liquidity module's swap is working based on batch processing, so it won't be swapped immediately.

Wait for the validator to approve the swap. (It may not be working on the testnet).


