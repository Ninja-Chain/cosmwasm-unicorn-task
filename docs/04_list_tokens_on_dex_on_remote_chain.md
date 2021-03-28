# 4.List Tokens on dex on remote chain.

The chain to which you send Cw20 has an integrated liquidity module, and you can list those tokens.

Liquidity (DEX) is implemented as a module, not a contract, and you will be executing liquidity commands.

If you want to learn about the commands and parameters used below, please refer to the following.

https://github.com/tendermint/liquidity/blob/develop/doc/client.md

- Create a liquidity pool

```
$ liquidityd tx liquidity create-pool 1 3000000uatom,3000000ibc/37075C5B491066D41670D8235351E49EBE84069CBBDDB5EE607E6B733F3DD04B --from liq --node http://13.248.175.68:80 --gas-prices 0.01uatom --gas auto --gas-adjustment 1.3 --chain-id swap-testnet-2002
```

Since the options are long, you can define them in environment variables.

- Check the pool

Let's find the pool we created based on denom pairs.

```
$ liquidityd query liquidity pool 2 --node http://13.248.175.68:80
pool:
  id: "2"
  pool_coin_denom: pool04B5C8804B6A7A56EC4BAD80F9A2A723C155CA4C8A241AA804999A4E06CA4A42
  reserve_account_address: cosmos1qj6u3qztdfa9dmzt4kq0ng48y0q4tjjvcmssnw
  reserve_coin_denoms:
  - ibc/37075C5B491066D41670D8235351E49EBE84069CBBDDB5EE607E6B733F3DD04B
  - uatom
  type_id: 1
```
