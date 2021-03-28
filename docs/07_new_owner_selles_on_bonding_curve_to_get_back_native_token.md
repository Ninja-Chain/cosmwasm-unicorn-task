# 7.New owner selles on bonding curve to get back native token

Burn the CW20 to get the native token.
Do the reverse of step 2.

- Send a Burn Msg to the cw20-bonding contract.
```
$ EXECUTE='{"burn":{"amount":"300000"}}'

$ wasmd tx wasm execute [cw20-bonding address] "$EXECUTE" --from [your account] --node https://rpc.cosmwasm.hub.hackatom.org:443 --chain-id hackatom-ru --gas-prices 0.01ucosm

```

- Check your balance.
```
$ wasmd query wasm contract-state smart [cw20-bonding address] '{"balance":{"address":"[your account address]"}}' --node https://rpc.cosmwasm.hub.hackatom.org:443

$ wasmd query bank balances [your account address] --node https://rpc.cosmwasm.hub.hackatom.org:443

```

Good work.
