# Mina Notes - Section 4
Estimate 5 minutes


## How the Mina blockchain Works 
  At the heart of the Mina blockchain is the concept of recursion.
  For people looking to validate the blockchain it is sufficient to have a proof that the latest block and all of the previous blocks in the chain are correct.
  
  

## Why it is succinct
- Based on SNARK proofs which are succinct, they have a small proof size, irrespective of the size of the inputs to the proof.

## How payments work
### Payment lifecycle
See [Docs](https://docs.minaprotocol.com/mina-protocol/lifecycle-of-a-payment)
 - Payment transaction is signed by senders private key and submitted to the network

## Account and zkApp Accounts

## Wallets

- The software that allows users to view balances and create transactions
Popular Mina wallets include

[Pallad](https://pallad.co/)  
  
![Screenshot 2024-12-13 at 12.31.14](https://hackmd.io/_uploads/B1XBYiY41x.png)

  
[Auro Wallet](https://www.aurowallet.com/)
Available as an mobile app or as a broswer wallet.
![Screenshot 2024-11-29 at 07.29.25](https://hackmd.io/_uploads/HJDPpJDQJx.png)


## Block explorers

Popular explorers include
[Minascan](https://minascan.io/mainnet/home)



![Screenshot 2024-12-13 at 12.33.54](https://hackmd.io/_uploads/ByNTYiFN1e.png)
[Minataur](https://minataur.net/)


## How to browse a blockchain / transactions / accounts on Mina
Using a block explorer such as Mina Explorer it is simple to find details of blocks, transactions and accounts.

![Screenshot_20241204_135328](https://hackmd.io/_uploads/B1d1yJRQJg.png)



### Blocks
![Screenshot 2024-12-13 at 12.34.42](https://hackmd.io/_uploads/r1Ge5jK4kx.png)


### Transactions

![Screenshot 2024-12-13 at 13.49.30](https://hackmd.io/_uploads/r199i2K41g.png)


### Accounts
![Screenshot 2024-12-13 at 12.36.57](https://hackmd.io/_uploads/S1cu9it4Jx.png)




---

Q&A

1. **What is the core concept that enables Mina blockchain's efficiency?**
   - a) Proof of Work
   - b) Recursion
   - c) Hashing
   - d) Byzantine Fault Tolerance
2. **What type of proofs does Mina rely on for its succinctness?**
   - a) SHA-256 proofs
   - b) Zero-knowledge proofs
   - c) SNARK proofs
   - d) Merkle proofs
3. **What is the primary function of a wallet in the Mina ecosystem?**
   - a) To explore the blockchain
   - b) To validate transactions
   - c) To manage accounts and initiate transactions
   - d) To mine MINA tokens
4. **What is the purpose of a block explorer in the context of the Mina blockchain?**
   - a) To mine new blocks
   - b) To execute smart contracts
   - c) To view and analyze blockchain data
   - d) To develop zkApps
5. **True or False:** The size of a SNARK proof increases proportionally with the size of the input data.