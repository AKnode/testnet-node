---
icon: star
order: 2000
---

hermes relayer config atlantic-1 channel-4 / deweb-testnet-1 channel-3

```
cd ~
wget https://github.com/informalsystems/ibc-rs/releases/download/v0.15.0/hermes-v0.15.0-x86_64-unknown-linux-gnu.zip
unzip hermes-v0.15.0-x86_64-unknown-linux-gnu.zip
sudo mv hermes /usr/local/bin
hermes version
```
```
mkdir $HOME/.hermes
wget -qO $HOME/.hermes/config.toml "https://raw.githubusercontent.com/AKnode/rekapan-node/main/sei-network/config.toml"
```
```
hermes keys restore deweb-testnet-1 -m "<YOUR_MNEMONIC>"
hermes keys restore atlantic-1 -m "<YOUR_MNEMONIC>"
```
```
sudo tee /etc/systemd/system/hermesd.service > /dev/null <<EOF
[Unit]
Description=hermes
After=network-online.target

[Service]
User=$USER
ExecStart=$(which hermes) start
Restart=on-failure
RestartSec=3
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload
sudo systemctl enable hermesd
sudo systemctl restart hermesd && sudo journalctl -u hermesd -f -o cat
```