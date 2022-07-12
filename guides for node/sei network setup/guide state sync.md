---
icon: star
order: 2000
---

# guide + state sync guud

### set rpc
```
RPC="http://rpc2.bonded.zone:21157"
```

### set variables
```
LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)
```

### check variables
```
echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH
```
### stop the node and reset
```
sudo systemctl stop seid && seid tendermint unsafe-reset-all
```

### configure persistent peers
```
peers="3f6e68bd476a7cd3f491105da50306f8ebb74643@rpc2.bonded.zone:21156"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.sei/config/config.toml


sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.sei/config/config.toml

```
### start node
```
sudo systemctl restart seid
sudo journalctl -u seid -f --no-hostname -o cat
```