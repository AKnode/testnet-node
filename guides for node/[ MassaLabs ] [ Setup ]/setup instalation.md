---
tags: [guides]
icon: star
---

# Massalab TEST.12.0

### Update & Dependencies..
```
sudo apt-get update && sudo apt-get upgrade -y

ufw allow 31244 && ufw allow 31245
```

### Instalasi
```
sudo apt install pkg-config curl git build-essential libssl-dev libclang-dev
```
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
### Nanti ada pilihan : 
1. Procced with installation  (default)    2. Customize Installation
3. Cancel Installation
### Ketik 1
### Terus tunggu sampe selesai installation

```
source $HOME/.cargo/env
rustc --version
rustup toolchain install nightly
```
### Tunggu proses sampe selesai
```
rustup default nightly
rustc --version
git clone --branch testnet https://github.com/massalabs/massa.git
```
### Create Boostrap
```
cd ~/massa/massa-node/config/
nano config.toml
```
### Copy semua yang dibawah lalu paste :
```
[network]
routable_ip = "0.0.0.0"  # ganti IP VPS Kalian
[bootstrap]
bootstrap_list = [["5.9.58.125:31245", "2TTHLbx94jTHdCJZgo1h5BqtPas9ApgF8mCKqCKcafU9PvZKze"],
    ["65.21.242.27:31245", "fttW6A1wsPeDMFU12CB4gZQwjmrL95PB3Ju4xsy5nH5FG9MnX"],
    ["66.94.126.163:31245", "2eFPtegA2YfscDpDpkej7QGXvzrGYmZzGyw2PqTmq9V8yDZBEd"],
    ["65.108.125.55:31245", "2jgNcHvHdU3suZx69xafZjvuDFNaxk8CG3q1QSm5H4e2A4obKF"],
    ["89.108.81.147:31245", "TFdNf3Qqhn8eAFmsjAVDurKPMphJkQCTqHz9grpTkSgqCxFd5"],
    ["109.107.191.199:31245", "PVmYspc6VrfYfGcXNqsr2ydDUm7PANTwgKAJ5QZETdzAsyeS5"],
    ["45.90.218.123:31245", "2qb35CqhWPKmAE2msU7LKX6hqTZfAfGWqEa3N5eMFLjwq2g9TC"],
    ["217.69.15.164:31245", "2YedW6Hz5M2W7SZktoD6Q3rxBT9RivkDsYxGvggnULVqWNjfLp"],
    ["54.36.174.177:31245", "xzGjgD7BBxTJZYo4p522TQzTkMUbKF3cVgfvuwjVdzo4XJgDM"],
    ["138.201.52.133:31245", "ci1GrVgQCzXwWgjf3ne3FxuDwrswZYiR15b1MEoufEyiJTce7"],
    ["[2a01:4f9:c011:1031::1]:31245", "2tozZ8UumtehXbn56o4cigpa4vtHU4rVLMEik3KCjmxP2oTT9x"],
    ["158.69.120.215:31245", "2Hujf2rHBquDrhixnw3dQTHaZMGp5xJq4q766dTRwy6v224CAi"],
    ["198.100.148.148:31245", "2mjmUgDxQVKpgepoaHw9xsyk6FySRmJoeRmgGzqKJ5ipgYGpMC"],
    ["89.58.26.33:31245", "2LZXGm4VU5wGGhYbqLuU6rHn1qUXMQJRGRcJzBFiX8BQNZffTF"],
    ["65.108.88.179:31245", "2J8JiN7FyYDpYwpL1MQpy7FeRbfT913qhLgmXG4GvRq1ZLWY8K"],
    ["88.198.23.230:31245", "8fgpM1UWqNbc7UFKTzMHHWrMwDt6Gcf3BWKYNGCZSFsMuZaiz"],
    ["5.196.26.217:31245", "2dsRkKvTrWmM7xJTmAiuvrkat5KsVgpEr5x2ExczYegJB4xvZS"],
    ["62.109.11.170:31245", "2vjycNEM3Wbf7rC8JxQNLMPtCLYWycVJfMV1J9ER5MTUpiQwp4"],
    ["95.216.143.66:31245", "2JoSyey3aruGQow5CMZ9hkreHxd3jGCRcRUShSqGQfKhsozhzB"],
    ["65.21.1.2:31245", "XMDRCjsSQSUmGMX9oK4acNnYhq7iC2HGFq87BB3PMbo4zVyoh"],
    ["[2a01:4f8:1c1e:676e::1]:31245", "ePCX7jRq9FpxfGFKA9pCftA3UfjBxR2DNmUpPafnZofMpnoe2"],
    ["88.218.170.191:31245", "mJViNCYddiLMq9dAdZ3mXSxwqpkgCURyTBZs5258fFESfjsKQ"]]

```
### CTRL + X Save Yes

### jika bootstrap error bisa ganti dengan ini
```
[network]
routable = "0.0.0.0" // ganti ip vps kalian
[bootstrap]
bootstrap_list = [
["20.213.239.67:31245", "2YbnetnuzpbVMZegk7D2ob5d5Beg9eR5GKk9KYZVQcDa6nbimD"],
["54.67.85.245:31245", "xa5GEYNQvVvR8YmZbn3HHrr3btbzNzNYnqD1T67kqmPVYiMHF"]
]
```
```
[network]
routable = "0.0.0.0" // ganti ip vps kalian
[bootstrap]
    # list of bootstrap (34.64.144.101, xMH7JJ467UaMkPY2XdnE3zzkSjZ2wAXhhicmUYmpp5DUpiBfp)
    bootstrap_list = [
        ["159.223.59.48:31245", "xMH7JJ467UaMkPY2XdnE3zzkSjZ2wAXhhicmUYmpp5DUpiBfp"],
        ["65.21.73.90:31245", "QhUK4RYAn6ec2kq3kPZgqvoyuGy89Tz9Q64TArqZGR6E5jdNU"],
        ["207.180.249.210:31245", "E9xhyG6mwyr6htatmUHUwmAd6wPLQLHdLUfZVF3LKT4HAedw4"],
        ["38.242.194.94:31245", "2FCjoJTxRKihZmJ5os97FHRxs3wqHC7uktL1miBqr15XRgGpcJ"],
        ]
```

### Sebelum ganti bootstrap silahkan kill node kalian
```
pkill -f massa-node
```
### Lanjut Screen biar enak

```
sudo apt install screen
screen
```

### Running Node
```
cd massa/massa-node/
RUST_BACKTRACE=full cargo run --release |& tee logs.txt
```

### Start Client
```
cd massa/massa-client/
cargo run --release
```

### Create Wallet
```
cd massa/massa-client/
cargo run
wallet_generate_private_key
```

### Simpan Private Key Kalian
```
wallet_info
```

### Get Faucet
- Join DC https://discord.gg/ECsFVDvt
- Channel #testnet-faucet -> Paste Address kalian

### Cek faucet
```
wallet_info
buy_rolls address kalian 1 0 
```
### Ambil juga NODE ID & STAKING KEY Kalian Carannya :
```
cd massa/massa-client/
cargo run 
```
```
node_add_staking_private_keys PK kalian
```
```
node_testnet_rewards_program_ownership_proof ADDRESSKALIAN ID-DISCORD-KALIAN
```

### Proof Ownership
### - DM botnya enter IP Address VPS Kalian
### - Copykan node_testnet_rewards_program_ownership_proof 
### - untuk cek status node tinggal enter info aja di botnya

kalo udh ketik info

tanks to @paperhang @Adefebrianft