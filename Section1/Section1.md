
# Section 1 - What is a blockchain

- An type of a decentralised system, it is a network of computers that work together to achieve a common goal, but there is no single point of control. 

- A system whose state is formed by consensus among the participants
- A system that allows digital assets to be transferred between users quickly and safely
- A system that allows transactions and computation to be validated.

Important components of the blockchain are 
- Nodes running 'client' software, each node will have a ledger holding the latest state of the system


![[decentralized-nodes-linked.png]]

- A network protocol, usually a P2P (peer to peer) network allowing blockchain nodes to communicate, and join or leave the network in a permissionless manner
- A protocol defining how nodes behave and how they can come to agreement about the system


## Features of a Blockchain

- The blockchain is robust and censorship resistant since there is no single point of failure.
- Transactions are verifiable, the blockchain provides an audit trail of transactions, all of which can be verified as correct
- Transactions are gathered into blocks which represent a state transition for the system 

![[cube_blockchain_linked.png]]


## Consensus mechanisms

Decentralised systems need a way to agree on the state of the system because there is no central authority to make decisions. 
A consensus mechanism is a way for a group of computers to agree on a single version of the truth.


![[decentralized_nodes_consensus.png]]



- There are 2 parts to the process
    - choosing a block producer to build a block of transactions
    - coming to agreement about the latest block on the chain.

![[cube_blockchain_linked.png]]


To send a payment the overall process is then
- Alice creates a transaction to pay Bob some Mina and sends this to the network which is in an initial state (purple)
- A block producer is chosen who builds a block consisting of a number of transactions
- The block is then passed around the network 

![[transaction_block_producer.png]]

- The nodes process the block and update their local state to reflect the state transition formed by the transactions in the block. Here we see the nodes changing to green as they update to the new state.
- The block with Alice's transaction is the latest block which has links to previous blocks that were produced
- Bob our end user will see the latest state which includes his balance being updated with the payment from Alice.


Mina uses a version of the Oroborous consensus mechanism, nodes vote to accept blocks and if a block receives enough votes it is accepted.


## Public / Private Keys
 - Public / Private key pairs are an example of asymmetric cryptography
 - Previously there was a problem sharing keys which is solved by asymmetric cryptography.
 - We start with a private key (a random number) from which a public key is derived.

![[private_public_keys.png]]

The derivation of the public key is computationally simple, but because of the nature of the derivation function, it is not feasible to reverse the direction of the function, that is to derive a private key from a public key.
The 'one way' nature of this derivation provides security and prevents our private keys from being compromised.


## Blockchain History

Bitcoin was the first useable fully decentralised blockchain.
It solved the double spend problem and provided incentives for people to participate in the system.

### Double Spend Problem

Blockchains allow transfer of digital assets such as tokens, but how can ensure that such assets are not copied and spent twice ? 

![[double_spend_problem.png]]

In a centralised system we could have a central registry tracking the assets.
Bitcoin solved this problem for decentralised systems, by allowing nodes to have their own ledger allowing them to chech that transactions are correct.

The nodes then have a means to come to consensus about the system, so that the system as a whole 'knows' that the state is correct and doesn't include any incorrect transactions.
### Smart Contracts

Ethereum introduced smart contracts allowing small programs to be executed on a blockchain as a component of a decentralised application.

The features of the underlying blockchain meant that the smart contracts

- Are immutable
- Are censorship resistant
- Have verifiable execution

In the early blockchains such as Ethereum, all of the execution of the contracts is done on chain. This means that each nodes executes the smart contract specified in the transaction.

In contrast to Ethereum, Mina has code execution off chain

![[MINA_off_chain_computation.png]]



This has the results of the off chain computation being added to the chain, along with a proof of the correctness of the off chain computation.


## Scalability

The scalability trillema is a rule of thumb, but it does show that some attempts to improve transaction throughput has been achieved at the cost of centralisation or security.

The Scalability Trilemma

![[blockchain_trilemma.png]]

For example reducing the number of nodes in the system can lead to greater throughput of transactions, but the system is then more centralised.


Q&A

1. Blockchains have the advantage of being

- Robust and censorship resistant
- Easily administered
- High performance

2. The state of the blockchain is held

- In a shared database that the nodes access
- On each node
- In a central ledger

3. A consensus mechanism allows the blockchain to

- Decide which nodes can be part of the system
- Decide on the latest state of the system
- Decide which users can use the blockchain

4. Accounts on the blockchain are

- Assigned to each user by the blockchain administrator
- Created by the users using asymmetric cryptography
- Allocated to the users on a first come first served basis

5. Smart contracts are

- AI enhanced programs used to administer the blockchain
- Verifiable code forming part of a decentralised application
- A legal contract that blockchain users need to accept

