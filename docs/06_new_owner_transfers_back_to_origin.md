# 6.new owner transfers back to origin

Just as you sent CW20 from hackatom-ru to swap-testnet-2002 in step 3, send your token in the opposite direction.



- Check your current balance.
```
$ liquidityd query bank balances $(liquidityd keys show -a dity) --node http://13.248.175.68:80

balances:
- amount: "100000"
  denom: ibc/37075C5B491066D41670D8235351E49EBE84069CBBDDB5EE607E6B733F3DD04B
- amount: "299998806"
  denom: uatom
- amount: "100000000"
  denom: uband
- amount: "100000000"
  denom: uiris
- amount: "100000000"
  denom: ukava
- amount: "100000000"
  denom: uluna
- amount: "100000000"
  denom: uscrt
- amount: "100000000"
  denom: uusdt
pagination:
  next_key: null
  total: "0"
```

- See IBC's channel information.

```
liquidityd query ibc channel channels --node http://13.248.175.68:80

...
- channel_id: channel-3
  connection_hops:
  - connection-3
  counterparty:
    channel_id: channel-6
    port_id: wasm.wasm18vd8fpwxzck93qlwghaj6arh4p7c5n89k7fvsl
  ordering: ORDER_UNORDERED
  port_id: transfer
  state: STATE_OPEN
  version: ics20-1
...
```

- Send your token to the origin chain.
```
$ liquidityd tx ibc-transfer transfer transfer channel-3 [origin_chain_account_address] 10000ibc/37075C5B491066D41670D8235351E49EBE84069CBBDDB5EE607E6B733F3DD04B --from dity --node http://13.248.175.68:80 --gas-prices 0.01uatom --gas auto --gas-adjustment 1.3 --chain-id swap-testnet-2002
```

- Confirm that the balance of your token has been reduced.
```
$ liquidityd query bank balances $(liquidityd keys show -a dity) --node http://13.248.175.68:80

balances:
- amount: "90000"
  denom: ibc/37075C5B491066D41670D8235351E49EBE84069CBBDDB5EE607E6B733F3DD04B
- amount: "299997377"
  denom: uatom
- amount: "100000000"
  denom: uband
- amount: "100000000"
  denom: uiris
- amount: "100000000"
  denom: ukava
- amount: "100000000"
  denom: uluna
- amount: "100000000"
  denom: uscrt
- amount: "100000000"
  denom: uusdt
pagination:
  next_key: null
  total: "0"
```

If the ibc-transfer is not executed for a certain period of time, the balance will be restored.
