# 2.Buy tokens

- Send a native token to the created contract and issue a new CW20 token.

```
$ EXECUTE='{"buy":{}}'
$ wasmd tx wasm execute [token_contract_address] "$EXECUTE" --from fred --amount 1000ucosm --node https://rpc.cosmwasm.hub.hackatom.org:443 --chain-id hackatom-ru --gas-prices 0.01ucosm
```

- Make sure your address has a CW20 token.

```
$ wasmd query wasm contract-state smart [token_contract_address] '{"balance":{"address": "[your_account_address]"}}' --node https://rpc.cosmwasm.hub.hackatom.org:443
data:
  balance: "2080000"
```
