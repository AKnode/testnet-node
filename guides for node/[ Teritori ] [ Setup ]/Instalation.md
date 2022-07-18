---
icon: star
order: 2000
---

# [Teritorid] [Setup]

## Server Configuration 

Here is the configuration of the server we are using:
- No. of CPUs: 2
- Memory: 2GB
- Disk: 80GB SSD
- OS: Ubuntu 18.04 LTS

Allow all incoming connections from TCP port 26656 and 26657

Notes on the configurations.
1. Multicore is important, regardless the less CPU time usage
2. teritorid uses less than 1GB memory and 2GB should be enough for now.
Once your new server is running, login to the server and upgrade your packages.



## Setup your machine

If you already have go 1.18+ and packages up to date, you can skip this part and jump to the second section: [Setup the chain](#setup-the-chain)  
Make sure your machine is up to date:  
```shell
apt update && apt upgrade -y 
```  

Install few packages:  
```shell
apt install build-essential git curl gcc make jq -y
```

Install Go 1.18+:  
```shell
wget -c https://go.dev/dl/go1.18.3.linux-amd64.tar.gz && rm -rf /usr/local/go && tar -C /usr/local -xzf go1.18.3.linux-amd64.tar.gz && rm -rf go1.18.3.linux-amd64.tar.gz
``` 

Setup your environnement (you can skip this part if you already had go installed before):  
```shell
echo 'export GOROOT=/usr/local/go' >> $HOME/.bash_profile
echo 'export GOPATH=$HOME/go' >> $HOME/.bash_profile
echo 'export GO111MODULE=on' >> $HOME/.bash_profile
echo 'export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin' >> $HOME/.bash_profile && . $HOME/.bash_profile
```  
## Setup the chain  

Clone the Teritori repository and install the v2 of testnet:  
```shell
git clone https://github.com/TERITORI/teritori-chain && cd teritori-chain && git checkout teritori-testnet-v2 && make install
```    

Init the chain:
```shell
teritorid init <YOUR_MONIKER> --chain-id teritori-testnet-v2
```  

Add config file:
```shell
wget -O $HOME/.teritorid/config/addrbook.json https://raw.githubusercontent.com/StakeTake/guidecosmos/main/teritori/teritori-testnet-v2/addrbook.json

SEEDS=""
PEERS="c1fdbc3d0679bcaf4cfe3aeaf5247ba12b7daa6f@49.12.236.218:26656,0b42fd287d3bb0a20230e30d54b4b8facc412c53@176.9.149.15:26656,2f394edda96be07bf92b0b503d8be13d1b9cc39f@5.9.40.222:26656,8ce81af6b4acee9688b9b3895fc936370321c0a3@78.46.106.69:26656"; \
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.teritorid/config/config.toml

SNAP_RPC="http://teritori.stake-take.com:26657"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.teritorid/config/config.toml
```
```shell
teritorid tendermint unsafe-reset-all --home $HOME/.teritorid
```
## Create service
```
tee <<EOF >/dev/null /etc/systemd/system/teritorid.service
[Unit]
Description=Teritori Cosmos daemon
After=network-online.target

[Service]
User=root
ExecStart=/root/go/bin/teritorid start
Restart=on-failure
RestartSec=3
LimitNOFILE=4096

[Install]
WantedBy=multi-user.target
EOF
```  

```shell
systemctl enable teritorid
systemctl daemon-reload
systemctl restart teritorid
```
## to cek logs
```
teritorid start  
```
Wait for the chain to synchronize with the current block... you can do the next step during this time  

## to cek info
```shell 
teritorid status 2>&1 | jq .SyncInfo
teritorid status 2>&1 | jq .NodeInfo
teritorid status 2>&1 | jq .ValidatorInfo
```
## Setup your account  

Create an account:  
```shell 
teritorid keys add <YOUR_KEY>
 ```  
 
 You can also you `--recover` flag to use an already existed key (but we recommend for security reason to use one key per chain to avoid total loss of funds in case one key is missing)  

Join our [Discord](https://discord.gg/teritori) and request fund on the `Faucet` channel using this command:  
```shell
$request <YOUR_TERITORI_ADDRESS>
```  

You can check if you have received fund once your node will be synched using this CLI command:
```shell
teritorid query bank balances <YOUR_TERITORI_ADDRESS> --chain-id teritori-testnet-v2
```  

Once the fund are received and chain is synchronized you can create your validator:   
```shell 
teritorid tx staking create-validator \
 --commission-max-change-rate=0.01 \
 --commission-max-rate=0.2 \
 --commission-rate=0.05 \
 --amount 1000000utori \
 --pubkey=$(teritorid tendermint show-validator) \
 --moniker=<YOUR_MONIKER> \
 --chain-id=teritori-testnet-v2 \
 --details="<DESCRIPTION_OF_YOUR_VALIDATOR>" \
 --security-contact="<YOUR_EMAIL_ADDRESS>" \
 --website="<YOUR_WEBSITE>" \
 --identity="<YOUR_KEYBASE_ID>" \
 --min-self-delegation=1000000 \
 --from=<YOUR_KEY>
 ```  


FAQ: Coming soon.

Join us on [Discord](https://discord.gg/uBNazcxxEf) for Testnet v2 Village discussions.