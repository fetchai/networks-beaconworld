# Fetch.ai Beaconworld network

This repo contains information on how to connect to the fetch.ai Beaconworld test network.

## Network APIs/endpoints and info
- **Chain ID:** beaconworld-0
- **Coin denomination:** atestfet
- **Decimals:** 18 (i.e. 1 testfet = 10^18 atestfet)
- **RPC Endpoint:** [https://rpc-beaconworld.fetch.ai:443](https://rpc-beaconworld.fetch.ai:443)
- **Token Faucet:** [https://faucet-beaconworld.fetch.ai/claim](https://faucet-beaconworld.fetch.ai/claim)
- **REST Endpoit:** [https://rest-beaconworld.fetch.ai:443](https://rest-beaconworld.fetch.ai:443)

## Block explorer
The block explorer can be accessed by clicking [here](https://explore-beaconworld.fetch.ai/)

## Installing fetchd
Fetchd requires mcl to be installed. This can be done by executing the following commands
```bash
# Run the following command if using Ubuntu
sudo apt-get install libgmp-dev swig libboost-all-dev
# Run the following command if using OS X
brew install swig boost gmp
```
```bash
cd ~
wget https://github.com/herumi/mcl/archive/v1.05.tar.gz
tar xvf v1.05.tar.gz
cd mcl-1.05
sudo make install
sudo ldconfig
```

To install the fetchd and fetchcli executables, execute the following commands:

```bash
cd ~
git clone https://github.com/fetchai/fetchd
cd fetchd && git checkout tags/v0.3.0-alpha10
make install
```



## Generating an account
Having installed fetchd, you can configure fetchcli to connect to the Beaconworld network by doing the following:
```bash
fetchcli config chain-id beaconworld-0
fetchcli config trust-node false
fetchcli config node https://rpc-beaconworld.fetch.ai:443
```

You can generate an account by executing the following line of code:
```bash
fetchcli keys add <Key name>
```

## Getting funds from the token faucet

Press the `Get Funds` button in the [block explorer](https://explore-beaconworld.fetch.ai/). Target wallet address has to be specified.

## Steps for running an agent-land network node
- Initialize fetchd by running:
  ```shell script
  fetchd init <Moniker-name> --chain-id beaconworld-0
  ```
- Execute the following command to get the genesis file:

  `curl https://rpc-beaconworld.fetch.ai/genesis? | jq .result.genesis > ~/.fetchd/config/genesis.json`
- Change `allow_duplicate_ip = false` to `allow_duplicate_ip = true` in `~/.fetchd/config/config.toml`
  - on **macOS X**:
    ```bash
    sed -i  '' 's/allow_duplicate_ip = false/allow_duplicate_ip = true/' ~/.fetchd/config/config.toml
    ```
  - on **Linux**:
    ```bash
    sed -i  's/allow_duplicate_ip = false/allow_duplicate_ip = true/' ~/.fetchd/config/config.toml
    ```
- Start fetchd by connecting to the seed node:
  ```bash
  fetchd start --p2p.seeds=8aeb090b6a4aa3c53e11453b3354bf020b1be990@connect-beaconworld.fetch.ai:36656
  ```
