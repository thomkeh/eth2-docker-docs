---
id: ConfigureWallet
title: "Step 3: Generate an eth2 wallet and key files"
sidebar_label: Configure Wallet
---

You will deposit ETH to the deposit contract, and receive staking rewards on this locked ETH in turn.<br />
> **Vital** [Recommendations.md](../Support/Recommendations.md) has comments on key security. If you haven't
read these yet, please do so now. You need to know how to guard your keystore password
and your seed phrase (mnemonic). **Without the mnemonic, you will be unable to withdraw your funds
after the "merge" of Ethereum 2.0 with Ethereum 1. You need the seed phrase or your eth is gone forever.**

> You can create the keys using eth2-docker. For mainnet, you may want to create
> the keys on a machine that is not connected to the Internet, and will be wiped
> afterwards. This can be done by using an [Ubuntu Live USB](https://agstakingco.gitbook.io/eth-2-0-key-generation-ubuntu-live-usb/)
> with [eth2.0-deposit-cli](https://github.com/ethereum/eth2.0-deposit-cli), then
> copy them to the machine the node will run on, and continue from
> "You brought your own keys", below.

Make sure you're in the project directory, `cd ~/eth2-docker` by default.

This command will create the keys to deposit Eth against:<br />
`sudo docker-compose run --rm deposit-cli`

Choose the number of validators you wish to create.
> A validator is synonymous to one 32 Ethereum stake. Multiple validators
> can be imported to a single validator client.

The created files will be in the directory `.eth2/validator_keys` in this project.
> eth2.0-deposit-cli shows you a different directory, that's because it has a view
> from inside the container.
 
This is also where you'd place your own keystore files if you already have some for import.

### You brought your own keys

They go into `.eth2/validator_keys` in this project directory, not directly under `$HOME`.

> You can transfer files from your PC to the node using scp. A graphical
> tool such as WinSCP will work, or you can use [command line scp](https://linuxize.com/post/how-to-use-scp-command-to-securely-transfer-files/).
### Test your Seed Phrase
*introduced in releases post 3/9/2020. Update if you are on an older version.*

From the project directory:

```
sudo docker-compose run --rm deposit-cli-add-recover --folder seed_check
```

Type your seed, and any password you like, as you'll throw away the duplicate `keystore-m` files.

Compare the `deposit_data` JSON files to ensure the files are identical.
```
diff -s .eth2/validator_keys/deposit_data*.json .eth2/seed_check/deposit_data*.json
```

Cleanup duplicate deposit_data.
```
rm ./eth2/seed_check/*
```