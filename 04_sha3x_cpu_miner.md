# Start the sha3x CPU miner

With the wallet address in hand, create a new Linux window to start the Sha3x miner. In this
example you'll need to replace "123456789" with the address you saved from the "Tari Address interactive" 
field in the console_wallet.

```console
./minotari_miner -b ./tari-mainnet-data \
    --network mainnet \
    -p miner.base_node_grpc_address=http://127.0.0.1:18142 \
    -p miner.wallet_payment_address="123456789"
```

You should see:

```console
Initializing logging according to "/root/.tari/mainnet/config/miner/log4rs.yml"
04:21 INFO  Starting Minotari Miner version: 2.1.0-0df1ede27452e090cfa81c28338df390e9a11e6e-release
```

[Return to the main README](README.md)
