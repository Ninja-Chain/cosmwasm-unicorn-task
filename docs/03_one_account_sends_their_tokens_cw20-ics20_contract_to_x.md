# 3.One account sends their tokens via cw20-ics20 contract to chain X

You can transfer cw20-standard tokens to another chain via a contract called cw20-ics20.

Here we are using swap-testnet-2002 as another chain.

- Create an account for the recipient and check the balance.

Make a note of the mnemonic as usual.

```
$ liquidityd add key liq

$ liquidityd keys show -a liq

$ liquidityd query bank balances $(liquidityd keys show -a liq) --node http://13.248.175.68:80
```

- See IBC's channel information.

```
$ wasmd q ibc channel channels --node https://rpc.cosmwasm.hub.hackatom.org:443

...
- channel_id: channel-6
  connection_hops:
  - connection-6
  counterparty:
    channel_id: channel-3
    port_id: transfer
  ordering: ORDER_UNORDERED
  port_id: wasm.wasm18vd8fpwxzck93qlwghaj6arh4p7c5n89k7fvsl
  state: STATE_OPEN
  version: ics20-1
...

```
Use the latest channel that is connected to cw20-ics20. In this case, it seems to be channnel-6.


- Convert the channel information to base64 format and create a msg for the contract to refer to.

```
{"channel":"channel-6","remote_address":"cosmos17863eksgma069msqtxpxh4cpgkj7vypqdd6c4y","timeout": 3600}
```

You can use the following websites to convert to base64.
https://www.base64encode.org/

- Execute the send command

"msg" is the base64 version of the previous one
The destination is not cw20-ics20, but the cw20 contract you issued.

```
EXECUTE='{"send":{"contract":"[cw20-ics20 contract address]","amount":"[you decide]","msg":"eyJjaGFubmVsIjoiY2hhbm5lbC02IiwicmVtb3RlX2FkZHJlc3MiOiJjb3Ntb3MxNzg2M2Vrc2dtYTA2OW1zcXR4cHhoNGNwZ2tqN3Z5cHFkZDZjNHkiLCJ0aW1lb3V0IjogMzYwMH0"}}'

wasmd tx wasm execute [cw20 contract address] "$EXECUTE" --from fred --node https://rpc.cosmwasm.hub.hackatom.org:443 --chain-id hackatom-ru --gas-prices 0.01ucosm
```

- Confirmation of receipt
```
$ liquidityd query bank balances $(liquidityd keys show -a liq) --node http://13.248.175.68:80
balances:
- amount: "3000000"
  denom: ibc/54D4C10264917B4A90C0EA62F5B04676C76F58A933FAC51885E7C50F709FE323
pagination:
  next_key: null
  total: "0"
```

The denom at the destination is defined as such as a specification.
ibc/~
