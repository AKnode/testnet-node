---
tags: [guides]
icon: star
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

singup

-  https://community.aptoslabs.com/

buat cek node
-  https://node.aptos.zvalid.com/
  

#instalasi 
```
wget -q -O aptos.sh https://raw.githubusercontent.com/AKnode/rekapan-node/main/aptos/aptos.sh && chmod +x aptos.sh && sudo /bin/bash aptos.sh
``` 
  
  
cek logs
```
docker logs -f --tail 100 aptos-validator-1
```
restart node:
```
cd ~/.aptos && docker-compose restart
```
stop node:
```
cd ~/.aptos && docker-compose stop
```
cek sync :
```
curl 127.0.0.1:9101/metrics 2> /dev/null | grep aptos_state_sync_version
```

cek wallet info:
```
source ~/.bash_profile
cat ~/.aptos/$APTOS_NODENAME.yaml
```