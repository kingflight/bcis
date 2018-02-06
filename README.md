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

## Decentralized consensus

## 

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
