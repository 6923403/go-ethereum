go mod init github.com/yourusername/go-ethereum
git checkout v1.9.25
go mod tidy
make all

---

//新地址 两个 密码123
//copy geth to dgeth 这一步无所谓
./dgeth  --datadir ./deepdata account new 
 - 0x243C7E365C421D3899Fe9751cdbf6fbB337127fE
 - 0x5c74cb71D877053eAa433790129b91E1A986C08A

//genesis.json
```
{
  "config": {
    "chainId": 10777,
    "homesteadBlock": 0,
    "daoForkBlock": 0,
    "daoForkSupport": true,
    "eip150Block": 0,
    "eip155Block": 0,
    "eip158Block": 0,
    "byzantiumBlock": 0,
    "constantinopleBlock": 0,
    "petersburgBlock": 0,
    "ethash": {}
  },
  "nonce": "0x42",
  "timestamp": "0x0",
  "extraData": "",
  "gasLimit": "0x13888",
  "difficulty": "0x16888",
  "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "coinbase": "0x0000000000000000000000000000000000000000",
  "alloc": {
    "243C7E365C421D3899Fe9751cdbf6fbB337127fE": {
      "balance": "0x10000"
    },
    "5c74cb71D877053eAa433790129b91E1A986C08A": {
      "balance": "0x10000"
    }
  }
}
```

//创建创世区块
./dgeth  --datadir ./deepdata init genesis.json
```
INFO [02-04|20:21:05.343] Bumping default cache on mainnet         provided=1024 updated=4096
INFO [02-04|20:21:05.348] Maximum peer count                       ETH=50 LES=0 total=50
INFO [02-04|20:21:05.376] Allocated cache and file handles         database=/Users/vc/git/src/go-ethereum/build/deepdata/geth/chaindata cache=16.00MiB handles=16
INFO [02-04|20:21:05.407] Writing custom genesis block 
INFO [02-04|20:21:05.415] Persisted trie from memory database      nodes=4 size=573.00B time=206.727µs gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
INFO [02-04|20:21:05.416] Successfully wrote genesis state         database=chaindata hash=4c648c…b037bb
INFO [02-04|20:21:05.416] Allocated cache and file handles         database=/Users/vc/git/src/go-ethereum/build/deepdata/geth/lightchaindata cache=16.00MiB handles=16
INFO [02-04|20:21:05.440] Writing custom genesis block 
INFO [02-04|20:21:05.440] Persisted trie from memory database      nodes=4 size=573.00B time=167.486µs gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
INFO [02-04|20:21:05.441] Successfully wrote genesis state         database=lightchaindata hash=4c648c…b037bb
```
./dgeth --maxpeers 0 --datadir ./deepdata  console

./dgeth --datadir ./deepdata --networkid 10777 --rpc console --port 30304 --rpcport 8546
