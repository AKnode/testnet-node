---
tags: [guides]
icon: dot
---

# create gentx on atlantic-1

## Setting up vars
Here you have to put name of your moniker (validator) that will be visible in explorer
```
NODENAME=<YOUR_MONIKER_NAME_GOES_HERE>
```

Save and import variables into system
```
echo "export NODENAME=$NODENAME" >> $HOME/.bash_profile
echo "export WALLET=wallet" >> $HOME/.bash_profile
echo "export CHAIN_ID=atlantic-1" >> $HOME/.bash_profile
source $HOME/.bash_profile
```

## Config app
```
seid config chain-id $CHAIN_ID
seid config keyring-backend test
```

## Init node
```
seid init $NODENAME --chain-id $CHAIN_ID
```

## Recover or create new wallet for Incentivized testnet
> ! If you are generating new wallet please don't forget to write down your 12-word mnemonic !

Option 1 - generate new wallet
```
seid keys add $WALLET
```

Option 2 - recover existing wallet
```
seid keys add $WALLET --recover
```

## Add genesis account
```
WALLET_ADDRESS=$(seid keys show $WALLET -a)
seid add-genesis-account $WALLET_ADDRESS 10000000usei
```

## Generate gentx
Please fill up `<your_validator_description>`, `<your_email>` and `<your_website>` with your own values
```
seid gentx $WALLET 10000000usei \
--chain-id $CHAIN_ID \
--moniker=$NODENAME \
--commission-max-change-rate=0.01 \
--commission-max-rate=0.20 \
--commission-rate=0.05 \
--details="<your_validator_description>" \
--security-contact="<your_email>" \
--website="<your_website>"
```

## Things you have to backup
- `12 word mnemonic` of your generated wallet
- contents of `$HOME/.sei/config/*`

## Submit PR with Gentx
1. Copy the contents of `$HOME/.sei/config/gentx/gentx-XXXXXXXX.json`
2. Fork https://github.com/sei-protocol/testnet
3. Create a file `gentx-{VALIDATOR_NAME}.json` under the `testnet/sei-incentivized-testnet/gentx` folder in the forked repo, paste the copied text into the file.
4. Create a Pull Request to the main branch of the repository

### Await further instructions!