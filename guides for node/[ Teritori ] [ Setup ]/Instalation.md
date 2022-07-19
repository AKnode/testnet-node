---
icon: star
order: 2000
---

---
teritori
---
Official documentation:
>- [Validator setup instructions](https://github.com/TERITORI/teritori-chain/blob/main/testnet/teritori-testnet-v2/README.md)

Chain explorer:
>- [Explorer from Nodes.Guru](https://teritori.explorers.guru/)
---
## Hardware Requirements
Like any Cosmos-SDK chain, the hardware requirements are pretty modest.
---
### Minimum Hardware Requirements
 - 3x CPUs; the faster clock speed the better
 - 4GB RAM
 - 80GB Disk
 - Permanent Internet connection (traffic will be minimal during devnet; 10Mbps will be plenty - for production at least 100Mbps is expected)

### Recommended Hardware Requirements 
 - 4x CPUs; the faster clock speed the better
 - 8GB RAM
 - 200GB of storage (SSD or NVME)
 - Permanent Internet connection (traffic will be minimal during devnet; 10Mbps will be plenty - for production at least 100Mbps is expected)
 ---

 #### auto Installation
 ```
wget -q -O teritori.sh https://raw.githubusercontent.com/AKnode/rekapan-node/main/teritori/teritori.sh && chmod +x teritori.sh && sudo /bin/bash teritori.sh
```

```
source $HOME/.bash_profile
```
### Logs and status
Logs
```
sudo journalctl -u teritorid -f --no-hostname -o cat
```


## Validator Info
```
teritorid status 2>&1 | jq .SyncInfo
```
```
teritorid status 2>&1 | jq .ValidatorInfo
```
```
teritorid status 2>&1 | jq .NodeInfo
```



## setup wallet

Add New Wallet
```
teritorid keys add wallet
```
Recover Existing Wallet
```
teritorid keys add wallet --recover
```
List All Wallets
```
teritorid keys list
```
Delete Wallet
```
teritorid keys delete wallet
```
---

## setup validator
### cek your balance
```
teritorid query bank balances $TERITORI_WALLET_ADDRESS
```
```
teritorid tx staking create-validator \
  --amount 1000000utori \
  --from $WALLET \
  --commission-max-change-rate "0.01" \
  --commission-max-rate "0.2" \
  --commission-rate "0.07" \
  --min-self-delegation "1" \
  --pubkey  $(seid tendermint show-validator) \
  --moniker $NODENAME \
  --chain-id $TERITORI_CHAIN_ID
```
### edit validator
```
teritorid tx staking edit-validator \
  --moniker=$NODENAME \
  --identity=<your_keybase_id> \
  --website="<your_website>" \
  --details="<your_validator_description>" \
  --chain-id=$TERITORI_CHAIN_ID \
  --from=$WALLET
```