go mod init github.com/yourusername/go-ethereum
git checkout v1.9.25
go get github.com/ethereum/go-ethereum/v1.9.25
go mod tidy
make all


---

//新地址 两个 密码123
//copy geth to dgeth 这一步无所谓
./geth  --datadir ./deepdata account new 
 - 0x3C473e866934C7BF6aa1ffC418Ac9c062a7D8a2C
 - 0x3e178e66Dd0a914bC656F4806EBEdc023908159d
 - 0x501e359834af5e0D4CceD6079A2e8C095f954d72----2
 - 0x03079D2f71254B1472A966683c13C177741F1C57----2

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
  "gasLimit": "2100000",
  "difficulty": "6888888",
  "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "coinbase": "0x0000000000000000000000000000000000000000",
  "alloc": {
    "3C473e866934C7BF6aa1ffC418Ac9c062a7D8a2C": {
      "balance": "1000000000000000000"
    },
    "3e178e66Dd0a914bC656F4806EBEdc023908159d": {
      "balance": "1000000000000000000"
    }
  }
}
```

### 创建创世区块

- ./geth  --datadir ./deepdata init genesis.json

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

### 启动两个节点

mac:
- ./geth --rpc --nodiscover --datadir ./deepdata --networkid 10777 --rpcapi "eth,net,web3,personal" --port 30222 --rpcaddr 0.0.0.0 --rpcport 20222 console

ubun:
- ./geth --rpc --nodiscover --datadir ./deepdata --networkid 10777 --rpcapi "eth,net,web3,personal" --port 30333 --rpcaddr 0.0.0.0 --rpcport 20333 console

### 多节点连接

- net.peerCount
- admin.peers
- admin.nodeInfo.enode

mac:
- admin.addPeer("enode://6b8956a0380697ff02d212a3f28bccc8e6f6e540bf52ba3833f8f5686a269ba12afb67711a1c11c89e052a4086b22f614061dfeac6329968486b4d89327fdd07@192.168.31.113:30222?discport=0")

ubuntu:
- admin.addPeer("enode://7ccdb978feb60c22ca4bcb64c7ad36eb90ff59ec367ac9b9a361fce24a14d714fda08727885e55412e3657276a89b88f7d63ce8e2f094dc660ee27a4568f43ee@192.168.31.172:30333?discport=0")

---

### 余额/解锁账户转移eth
```
eth.getBalance(eth.accounts[0])
eth.getBalance(eth.accounts[1])
web3.fromWei(eth.getBalance(eth.accounts[0]),'ether')
web3.fromWei(eth.getBalance(eth.accounts[1]),'ether')
personal.unlockAccount(eth.accounts[0])
amount = web3.toWei(1,'ether')
eth.sendTransaction({from:eth.accounts[0],to:eth.accounts[1],value:amount})
txpool.status //查看处理状态
eth.blockNumber //区块数
eth.getBlock(1) //查看区块
eth.getTransaction("0x7d6f72b9bd40c8eafe2a2907992e6808c67dfda5f0d2a1969580fda1795fc6df") //tx
```

