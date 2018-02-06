# Cryptographic hash function
- A cryptographic hash (sometimes called ‘digest’) is a kind of ‘signature’ for a text or a data file. SHA-256 generates an almost-unique 256-bit (32-byte) signature for a text.
- It is a mathematical algorithm that maps data of arbitrary size to a bit string of a fixed size (a hash) and is designed to be a one-way function, that is, a function which is infeasible to invert.

```
               ┌──────┐                                                     
┌───────┐      │      │      ┌─────────────────────────────────────────────┐
│ Hello │─────▶│ Hash │─────▶│  f572d396fae9206628714fb2ce00f72e94f2258f   │
└───────┘      │      │      └─────────────────────────────────────────────┘
               └──────┘                                                     
```

# Public-key cryptography
Public key cryptography, or asymmetrical cryptography, is any cryptographic system that uses pairs of keys: public keys which may be disseminated widely, and private keys which are known only to the owner. 


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
A Merkle tree is a tree in which every leaf node is labelled with the hash of a data block and every non-leaf node is labelled with the cryptographic hash of the labels of its child nodes.
The Merkle tree allows verifying that a transaction exists in the block without having the entire block, by following its Merkle branch.
![BinaryMerkleTree](https://ds055uzetaobb.cloudfront.net/image_optimizer/7bd6fe56d9088a8efe8d22aaf9e47cb10d18ba9d.png)

# Blockchain
A blockchain, originally block chain, is a continuously growing list of records, called blocks, which are linked and secured using cryptography. Each block typically contains a cryptographic hash of the previous block, a timestamp and transaction data. By design, a blockchain is inherently resistant to modification of the data. It is "an open, distributed ledger that can record transactions between two parties efficiently and in a verifiable and permanent way". For use as a distributed ledger, a blockchain is typically managed by a peer-to-peer network collectively adhering to a protocol for validating new blocks. Once recorded, the data in any given block cannot be altered retroactively without the alteration of all subsequent blocks, which requires collusion of the network majority.

![aaa](https://upload.wikimedia.org/wikipedia/commons/thumb/9/98/Blockchain.svg/226px-Blockchain.svg.png)

<p><a href="https://commons.wikimedia.org/wiki/File:Bitcoin_Block_Data.svg#/media/File:Bitcoin_Block_Data.svg"><img src="https://upload.wikimedia.org/wikipedia/commons/5/55/Bitcoin_Block_Data.svg" alt="Bitcoin Block Data.svg" height="480" width="640"></a><br>By <a href="//commons.wikimedia.org/wiki/User:Matth%C3%A4us_Wander" title="User:Matthäus Wander">Matthäus Wander</a> - <span class="int-own-work" lang="en">Own work</span>, <a href="https://creativecommons.org/licenses/by-sa/3.0" title="Creative Commons Attribution-Share Alike 3.0">CC BY-SA 3.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=26816920">Link</a></p>


## Decentralized consensus

New coins are slowly mined into existence by following a mutually agreed-upon set of rules. A user mining bitcoins is running a software program that searches for a solution to a very difficult math problem the difficulty of which is precisely known. This difficulty is automatically adjusted on a predictable schedule so that the number of solutions found globally for a given unit of time is constant: the global system aims for 6 per hour. When a solution is found, the user may tell everyone of the existence of this newly found solution along with other information packaged together in what is called a "block". The solution itself is a proof-of-work or PoW. It is hard to find, but easy to verify.

Blocks create 12.5 new bitcoins at present [October 2016]. This amount, known as the block reward, is an incentive for people to perform the computation work required for generating blocks. Roughly every 4 years, the number of bitcoins that can be "mined" in a block reduces by 50%. Originally the block reward was 50 bitcoins; it halved in November 2012; it then halved again in July 2016. Any block that is created by a malicious user that does not follow this rule (or any other rules) will be rejected by everyone else. In the end, no more than 21 million bitcoins will ever exist.


## Distrubuted database

![im](https://en.wikipedia.org/wiki/File:Public-key-crypto-1.svg)
![im](https://octodex.github.com/images/yaktocat.png)

<a href="http://www.youtube.com/watch?feature=player_embedded&v=YOUTUBE_VIDEO_ID_HERE
" target="_blank"><img src="http://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>


- 区块链
    - UTXO transaction model
- 共识算法
    - consensus system
        - PoW (hard to find easy to validate problem)

- 智能合约

- 



- 参考
    - http://www.fintech.finance/featured/blockchain-5-key-concepts/
    - https://www.movable-type.co.uk/scripts/sha256.html
    - https://bitcoin.stackexchange.com/questions/10696/what-is-the-benefit-of-using-a-merkle-root-rather-than-simply-hashing-all-of-the
    - https://hbr.org/2017/01/the-truth-about-blockchain
    - https://en.wikipedia.org/wiki/Blockchain
    - https://www.pluralsight.com/guides/software-engineering-best-practices/blockchain-architecture
