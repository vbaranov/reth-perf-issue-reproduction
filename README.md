## Repo for reproduction performance issue with Reth v0.1.0-alpha.4 JSON RPC

Steps to reproduce:

1. Run Reth node v0.1.0-alpha.4 for ETH Mainnet using docker-compose
2. Run Blockscout application:

```
git clone https://github.com/vbaranov/reth-perf-issue-reproduction
ETHEREUM_JSONRPC_HTTP_URL=... ETHEREUM_JSONRPC_WS_URL=... docker-compose up
```

where `ETHEREUM_JSONRPC_HTTP_URL` - node's JSON RPC endpoint, `ETHEREUM_JSONRPC_WS_URL` - node's WS endpoint

For instance, with the node running on the same host:
```
ETHEREUM_JSONRPC_HTTP_URL=http://localhost:8545 ETHEREUM_JSONRPC_WS_URL=ws://localhost:8545 docker-compose up
```

3. Keep it running for 1 - 2 hours. Blockscout will be working at http://localhost:4000 and load the node with various requests.

As a results the node will stop respond to any requests beside simple like `eth_blockNUmber`, `web3_clientVersion`, `net_version`. 

At leasts, JSON RPC requests to these methods will hang:

- `eth_getBlockByNumber`
- `eth_getTransactionReceipt`
- `eth_getTransactionByHash`
- `eth_getBalance`
- `trace_replayBlockTransactions`
