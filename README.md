# Hyomoum Blockchain

Hyomoum addresses the existing limitations of the current blockchains and empowers a solid foundation for future decentralized projects.
Hyomoum’s unique approach is to provide built-in, on-chain solutions to process transactions in a deterministic way to ensure fast, secure, cheap and a green network for a variety of use-cases.

The chain is designed to solve real-world problems at scale by providing native token management systems and Decentralized 
Exchange (DEX), while being fully decentralized. In addition to the built-on-chain solutions, Hyomoum uses WebAssembly (WASM)
to process smart contracts, and utilizes the Tendermint Byzantine Fault Tolerance (BFT) consensus mechanism and Cosmos SDK’s 
proven Bonded Proof of Stake (BPoS).

## Build and Play

Hyomoum blockchain is under development and all the features are going to be added progressively over time.
Everyone is encouraged to run a chain locally for development and testing purposes.

Entire process of running local chain is automated by our tooling. The only prerequisites are:
- `docker` installed from your favorite package manager
- `go 1.18` or newer installed and available in your `PATH`

After the command completes you may find executable `$Hyomoum_PATH/crust/bin/cored`, being both blockchain node and client.

### Start local chain

To start local Hyomoum blockchain execute:

```
$ $Hyomoum_PATH/crust/bin/crust znet
(znet) [znet] $ start
```

After a while applications will be deployed to your docker:
- `cored-00`: single `cored` validator
- `explorer-postgres`, `explorer-hasura` and `explorer-bdjuno`: components of the block explorer (work in progress)

To stop and purge the testing environment run:

```
$ $HOME/crust/bin/crust znet remove
```

### Interact with the local chain

After entering `znet` console by executing:

```
$ $HOME/crust/bin/crust znet
(znet) [znet] $ start
```
you may use client to interact with the chain:
1. List pregenerated wallets:
```
(znet) [znet] $ cored-00 keys list
```
You may use those wallets to issue transactions and queries

2. Generate a Wallet and Query balances:
```
(znet) [znet] $ cored-00 keys add {YOUR_WALLET_NAME} 
```
This will generate a wallet and print out the mnemonic at the end. It will also print 
the address and public key. Use the address in the next commands to query its balance
and transfer funds to it.
```
(znet) [znet] $ cored-00 q bank balances {YOUR_GENERATED_ADDRESS}
```
Remember to replace address with the one existing in your keystore.

You will see the balance is zero.

3. Send tokens from one account to another:
```
(znet) [znet] $ cored-00 tx bank send alice {YOUR_GENERATED_ADDRESS} 10udevcore --broadcast-mode=block
```
Run the query again and you will see that there are now funds in the newly generated account.
```
(znet) [znet] $ cored-00 q bank balances {YOUR_GENERATED_ADDRESS}
```

## Connect to Running Chains
Hyomoum has `mainnet`, `testnet` and `devnet` chains running. In order to connect to any of those networks, get the
network variables from the docs [here](https://docs.Hyomoum.dev/tutorials/network-variables.html), and
provide the correct `node` and `chain-id` flags to the cli command. 
As an example here is a command to connect to the testnet to get the status:

```
$ cored status --chain-id=Hyomoum-testnet-1 --node=https://full-node.testnet-1.Hyomoum.dev:26657
```
It should also be mentioned that for development purposes testnet is more stable than devnet.

You can also find block explorers for each chain by this
