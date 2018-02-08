# Cryptographic hash function
> - A cryptographic hash (sometimes called ‘digest’) is a kind of ‘signature’ for a text or a data file. SHA-256 generates an almost-unique 256-bit (32-byte) signature for a text.
> - It is a mathematical algorithm that maps data of arbitrary size to a bit string of a fixed size (a hash) and is designed to be a one-way function, that is, a function which is infeasible to invert.

```
               ┌──────┐                                                     
┌───────┐      │      │      ┌─────────────────────────────────────────────┐
│ Hello │─────▶│ Hash │─────▶│  f572d396fae9206628714fb2ce00f72e94f2258f   │
└───────┘      │      │      └─────────────────────────────────────────────┘
               └──────┘                                                     
```
### 用途
- 在区块链中，主要用于生成数据的唯一标识，和校验数据是否被篡改。


# Public-key cryptography
### 定义
Public key cryptography, or asymmetrical cryptography, is any cryptographic system that uses pairs of keys: public keys which may be disseminated widely, and private keys which are known only to the owner. 

### 用途
非对称加密的两个常见用途是：加密/解密，签名/验证。

- 加密/解密
```
┌──────┐        ┌───────────────────┐    ┌──────────────────────┐
│ data │───────▶│ encrypt with pub  │───▶│    encrypted data    │
└──────┘        └───────────────────┘    └──────────────────────┘
    ▲                                                │           
    │                                                │           
    │           ┌───────────────────┐                │           
    │           │   decrypt with    │                │           
    └───────────│    private key    │◀───────────────┘           
                └───────────────────┘                            
```

- 签名/验证
```
               ┌───────────────────┐                      
┌──────┐       │ sign with private │     ┌───────────────┐
│ data │──────▶│   key (decrypt)   │────▶│   signature   │
└──────┘       └───────────────────┘     └───────────────┘
    ▲                                            │        
    │          ┌───────────────────┐             │        
    │          │ verify signature  │             │        
    └──────────│   with pub key    │◀────────────┘        
               │     (encrypt)     │                      
               └───────────────────┘                      
```
# Merkle tree
### 定义
> A Merkle tree is a tree in which every leaf node is labelled with the hash of a data block and every non-leaf node is labelled with the cryptographic hash of the labels of its child nodes.
> The Merkle tree allows verifying that a transaction exists in the block without having the entire block, by following its Merkle branch.

![BinaryMerkleTree](https://ds055uzetaobb.cloudfront.net/image_optimizer/7bd6fe56d9088a8efe8d22aaf9e47cb10d18ba9d.png)

### 用途
- 在不获取大块数据的情况下，快速验证某一小块数据是否属于一大块数据的一部分

# Blockchain
### 定义
> A blockchain, originally block chain, is a continuously growing list of records, called blocks, which are linked and secured using cryptography. Each block typically contains a cryptographic hash of the previous block, a timestamp and transaction data. By design, a blockchain is inherently resistant to modification of the data. It is "an open, distributed ledger that can record transactions between two parties efficiently and in a verifiable and permanent way". For use as a distributed ledger, a blockchain is typically managed by a peer-to-peer network collectively adhering to a protocol for validating new blocks. Once recorded, the data in any given block cannot be altered retroactively without the alteration of all subsequent blocks, which requires collusion of the network majority.

### 特点
- 链上的任意两个相邻区块之间的合法性是可以快速验证的（包括孤儿链上的区块）
- 只有其中的某一条链是被认可的，哪一条链被认可由预先定好的规则决定（如，工作量最大的链）
- 新区块不断添加到主链的尾部，旧区块很难被修改
- 数据存储在网络的所有节点上，任何人都可以查看

![blockchain](https://cdn-images-1.medium.com/max/2000/1*MZCUJTeZvgQsTDYPQOw_Vg.png)

<p><a href="https://commons.wikimedia.org/wiki/File:Bitcoin_Block_Data.svg#/media/File:Bitcoin_Block_Data.svg"><img src="https://upload.wikimedia.org/wikipedia/commons/5/55/Bitcoin_Block_Data.svg" alt="Bitcoin Block Data.svg" height="480" width="640"></a>

### Transaction

Transaction是业务数据(payload)，其他数据都是开销(crytographic overhead)。

##### UTXO模型
对于Bitcoin，业务就是货币功能，所以Bitcoin的区块链实质上是一个财务账簿，每个transaction记录了谁转给谁多少BTC。而每个账户的余额就是这个账户下的所有未花费输出(Unspent Transaction Output)。

为了保证UTXO只能被Owner账户使用，每个transaction的收款记录都会包括`金额`和一个`收款人公钥信息`。当收款人需要使用这笔UTXO时，收款人需要创建一个transation，以这笔UTXO作为输入，输入记录包含使用者的`私钥`的签名，以`新的收款人的公钥信息`和`金额`作为输出。然后将这个transaction向Bitcoin网络广播，记账人(miner)会用UTXO输出中的`公钥`验证使用者的签名。记账人会将一定时间内收集到的合法transaction打包，封装成一个Block，然后向Bitcoin网络广播。

一个单输入单输出的Bitcoin transaction:
```
Input:
Previous tx: f5d8ee39a430901c91a5917b9f2dc19d6d1a0e9cea205b009ca73dd04470b9a6
Index: 0
scriptSig: 304502206e21798a42fae0e854281abd38bacd1aeed3ee3738d9e1446618c4571d10
90db022100e2ac980643b0b82c0e88ffdfec6b64e3e6ba35e7ba5fdd7d5d6cc8d25c6b241501

Output:
Value: 5000000000
scriptPubKey: OP_DUP OP_HASH160 404371705fa9bd789a2fcd52d2c580b65d35549d
OP_EQUALVERIFY OP_CHECKSIG
```

##### Blockchain 2.0
对于Ethereum, 业务是记录EVM(Ethereum Virtual Machine)的状态变化。EVM是一个sandboxed turing complete transaction-based state machine。状态变化的记录单位是transaction，在Ethereum中，transaction是可以触发EVM的状态变化的输入。和恢复数据库同理，从创世区块到最新区块的中的transaction可以恢复出系统在任何时刻的状态。
![Ethereum block chain](https://cdn-images-1.medium.com/max/1600/1*jZ-VRXBJtOnePofB0z2Q8A.png)

Ethereum区块链存储的payload包括了数据和code，这里code就是smart contract. 支持smart contract的区块链被叫做Blockchain 2.0
> Blockchain2.0 is in effect a mechanism allowing programmable transactions (transactions modified by a condition or a set of conditions)

![Ethereum transaction](https://cdn-images-1.medium.com/max/1600/1*I635Y9btMh667inOhDBQ_g.png)

>A smart contract is a mechanism involving digital assets and two or more parties, where some or all of the parties put assets in and assets are automatically redistributed among those parties according to a formula based on certain data that is not known at the time the contract is initiated.
One example of a smart contract would be an employment agreement: A wants to pay \$500 to B to build a website. The contract would work as follows: A puts $500 into the contract, and the funds are locked up. When B finishes the website, B can send a message to the contract asking to unlock the funds. If A agrees, the funds are released. If B decides not to finish the website, B can quit by sending a message to relinquish the funds. If B claims that he finished the website, but A does not agree, then after a 7-day waiting period it’s up to judge J to provide a verdict in A or B’s favor.

### Decentralized consensus

共识算法的共性：
- 控制新区块生成速度
- 分散区块链的写权限

##### Proof of work
A proof of work is a piece of data which is difficult (costly, time-consuming) to produce but easy for others to verify and which satisfies certain requirements. Producing a proof of work can be a random process with low probability so that a lot of trial and error is required on average before a valid proof of work is generated.

以Bitcoin为例，Bitcoin网络中有两种角色，转账人和记账人(Miner)。转账人发起转账时，生成transaction，在网络中广播。记账人不断收集网络中的transaction，并打包成block，最早打包成功的记账人会获得一笔收益。打包本身对计算机来说是简单的运算，为了让区块链增长的速度不会过快，并且让所有记账人都有机会记账，打包的过程增加了一个较难的步骤，即寻找一个nonce值，让这个包的hash值小于某个特定的值（Difficulty）。nonce是区块里面的一个字段，通过改变这个字段可以让这个区块有不同的hash值。

Bitcoin网络的Difficulty值每2000个区块更新一次，Difficulty值越小，难度越大。值可以减少也可以增加，变化的目标是让区块平均10分钟生成一次。

当记账人在还没计算出正确的nonce值时，收到了其他人的计算结果，即区块。这个区块可以很快地被验证，验证过程即计算该区块的hash值，如果是错误的区块则丢弃。如果该区块正确，此时，有两种选择：
1. 忽略这个新区块，继续计算未完成的区块。
2. 放弃未计算完的区块，在此新区块加入链中，然后重新计算。

如果所有人都选择1，那么这个从上一个区块开始，会产生n个分叉，并且n个分叉的深度的是相等的，则没有办法选出主链。这种情况是Bitcoin网络不能支持的，因为网络设计时的一个假设是大部分人是遵守规则的，而现实情况确实是这样。

如果只有个别坏人选择1（或者个别好人因为网络原因没有收到这个新区块的广播），当坏人计算出结果，向网络广播时，网络中的大部分人都已经收到过这个深度的区块，这个区块成为一个老区块的第二个后继区块，因为这个区块的深度没有超过当前正在计算的区块深度，所以好人并不会在收到的这个区块后做计算，这个区块就成了孤儿区块。由于孤儿区块不在主链中，所以计算孤儿区块的人是没有收益的。总之，坏人选择1是没有任何好处的，只会浪费自己计算力。

proof of work是第一个被验证可行的共识算法，但缺点是明显的，一是消耗能源，二是存在51%攻击（当单个体的算力超过全网络的一般时，攻击的成功率是100%）。


##### Proof of stake

- Randomized block selection
Nxt and BlackCoin use randomization to predict the following generator, by using a formula that looks for the lowest hash value in combination with the size of the stake.[1][2][3] Since the stakes are public, each node can predict - with reasonable accuracy - which account will next win the right to forge a block.

- Coin age-based selection
Peercoin's proof-of-stake system combines randomization with the concept of "coin age", a number derived from the product of the number of coins times the number of days the coins have been held.
Coins that have been unspent for at least 30 days begin competing for the next block. Older and larger sets of coins have a greater probability of signing the next block. However, once a stake of coins has been used to sign a block, they must start over with zero "coin age" and thus wait at least 30 more days before signing another block. Also, the probability of finding the next block reaches a maximum after 90 days in order to prevent very old or very large collections of stakes from dominating the blockchain.[4][5][6] 
This process secures the network and gradually produces new coins over time without consuming significant computational power.[7] Peercoin's developer claims that this makes a malicious attack on the network more difficult due to the lack of a need for centralized mining pools - and the fact that purchasing more than half of the coins is likely more costly than acquiring 51% of proof-of-work hashing power .[8]





# DApp
> DApp is an abbreviated form for decentralized application.
> A DApp has its backend code running on a decentralized peer-to-peer network. Contrast this with an app where the backend code is running on centralized servers.
> A DApp can have frontend code and user interfaces written in any language (just like an app) that can make calls to its backend. Furthermore, its frontend can be hosted on decentralized storage such as Swarm or IPFS.
> If an app=frontend+server, since Ethereum contracts are code that runs on the global Ethereum decentralized peer-to-peer network, then:
> DApp = frontend + contracts

# Side chain
### Lightning network

# Dao and The Dao



# 参考资料
- https://medium.com/@preethikasireddy/how-does-ethereum-work-anyway-22d1df506369
- https://blog.ethereum.org/2014/05/06/daos-dacs-das-and-more-an-incomplete-terminology-guide/
- http://www.fintech.finance/featured/blockchain-5-key-concepts/
- https://www.movable-type.co.uk/scripts/sha256.html
- https://bitcoin.stackexchange.com/questions/10696/what-is-the-benefit-of-using-a-merkle-root-rather-than-simply-hashing-all-of-the
- https://hbr.org/2017/01/the-truth-about-blockchain
- https://en.wikipedia.org/wiki/Blockchain
- https://www.pluralsight.com/guides/software-engineering-best-practices/blockchain-architecture
https://en.bitcoin.it/wiki/Transaction