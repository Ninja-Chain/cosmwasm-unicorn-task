# 1.Create a bonding curve contract.

The contract cw20-bonding prepared by CosmWasm can be used to issue tokens using the Bonding Curve.

[cw20-bonding](https://github.com/CosmWasm/cosmwasm-plus/tree/master/contracts/cw20-bonding)

After compiling this contract, let's deploy it to the chain with the cosmwasm module.

Pay attention to the version of cosmwasm-std described in cago.toml and the version supported by the cosmwasm module of the chain you are deploying to.
For more information on how to deploy contracts, please refer to the official CosmWasm documentation.

[CosmWasm](https://docs.cosmwasm.com/)

In this document, we use a testnet chain called hackatom-ru.

- Deploying the cw20-bonding contract
```
$ wasmd tx wasm store cw20_bonding.wasm --from fred --chain-id hackatom-ru --gas-prices 0.01ucosm --gas auto --gas-adjustment 1.3 --node https://rpc.cosmwasm.hub.hackatom.org:443  -y
```

- Checking the deployed contract

```
wasmd query wasm list-code --node https://rpc.cosmwasm.hub.hackatom.org:443
```

- Initialize the contract
```
$ INIT=$(jq -n '{"name":"naushika","symbol":"NAU","decimals":6,"reserve_denom":"ucosm","reserve_decimals":6,"curve_type": {"square_root":{"slope":"100",scale:5}}}')
$ wasmd tx wasm instantiate 17 "$INIT" --from fred --label "NAUSHIKA" --node https://rpc.cosmwasm.hub.hackatom.org:443 --chain-id hackatom-ru --gas-prices 0.01ucosm
```

- Check the information of the issued token.
```
$ wasmd query wasm contract-state smart wasm1sh4r6cpxua7k8hcu4auqu8pk9g9luzz7qf2pex '{"token_info":{}}' --node https://rpc.cosmwasm.hub.hackatom.org:443
data:
  decimals: 6
  name: naushika
  symbol: NAU
  total_supply: "7297000"
```
