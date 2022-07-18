---
icon: star
order: 2000
---

# 1# setup - instalation 🐉
---
# sei node setup for atlantic-1
---
Official documentation:
>- [Validator setup instructions](https://docs.seinetwork.io/nodes-and-validators/joining-devnets)

Chain explorer:
>- [Explorer from Nodes.Guru](https://sei.explorers.guru/)
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
wget -q -O seid.sh https://raw.githubusercontent.com/AKnode/rekapan-node/main/sei-network/seid.sh && chmod +x seid.sh && sudo /bin/bash seid.sh
```

```
source $HOME/.bash_profile
```
### Logs and status
Logs
```
sudo journalctl -u seid -f --no-hostname -o cat
```


# Validator Info
```
seid status 2>&1 | jq .SyncInfo
```
```
seid status 2>&1 | jq .ValidatorInfo
```
```
seid status 2>&1 | jq .NodeInfo
```



# setup wallet

Add New Wallet
```
seid keys add wallet
```
Recover Existing Wallet
```
seid keys add wallet --recover
```
List All Wallets
```
seid keys list
```
Delete Wallet
```
seid keys delete wallet
```
---

# setup validator
### cek your balance
```
seid query bank balances $SEI_WALLET_ADDRESS
```
```
seid tx staking create-validator \
  --amount 1000000usei \
  --from $WALLET \
  --commission-max-change-rate "0.01" \
  --commission-max-rate "0.2" \
  --commission-rate "0.07" \
  --min-self-delegation "1" \
  --pubkey  $(seid tendermint show-validator) \
  --moniker $NODENAME \
  --chain-id $SEI_CHAIN_ID
```
### edit validator
```
seid tx staking edit-validator \
  --moniker=$NODENAME \
  --identity=<your_keybase_id> \
  --website="<your_website>" \
  --details="<your_validator_description>" \
  --chain-id=$SEI_CHAIN_ID \
  --from=$WALLET
```
