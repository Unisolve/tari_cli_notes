# Start the local tari node

## Run the node

Create a new Linux window and start the base node for mining:

```console
./minotari_node -b ./tari-mainnet-data \
    --network mainnet \
    --grpc-enabled \
    -p bypass_range_proof_verification=true \
    -p base_node.grpc_address=/ip4/127.0.0.1/tcp/18142 \
    -p base_node.grpc_server_allow_methods=\"get_tokens_in_circulation,get_tip_info,get_sync_info,get_sync_progress,get_mempool_stats,get_version,get_network_status,list_headers,get_mempool_transactions,get_active_validator_nodes,get_blocks\" \
    --mining-enabled
```

When you're asked:

```console
Initializing logging according to "./tari-mainnet-data/mainnet/config/base_node/log4rs.yml"
Node config does not exist.
Would you like to mine (Y/n)?
NOTE: this will enable additional gRPC methods that could be used to monitor and submit blocks from this node.
```

answer "Y"

And when asked:

```console
Node identity does not exist.
Would you like to create one (Y/n)?
```

answer "Y"

Once the node is running, you can enter control-c at any time to call up the command
prompt and enter commands. For example:

```console
version
```

or

```console
list-peers
```
or

```console
status
```

or 
```console
help
```

## Wait for it to sync

TODO: Should then wait to sync to tip before trying to mine

[Return to the main README](README.md)
