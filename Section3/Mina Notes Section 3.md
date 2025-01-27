# Mina Notes Section 3

(Estimate 10-15 minutes)

## What are Zero Knowledge Proofs 
A zero knowledge proof allows a prover to convince a verifier of a claim. The zero knowledge aspect means that the verifier only finds out that the proof is valid, not what the inputs to the proof were.

For example a prover could claim they know the solution to a puzzle. They could create a proof, using their solution as an input. The verifier would be convinced that the prover knows a solution to the puzzle, but the proof doesn't reveal any details about the solution.

The role of a verifier is often supplied by a program that can take a proof as an input along with any public inputs and output a single bit, which indicates whether the proof is valid.


See [Docs](https://minaprotocol.com/blog/zero-knowledge-proofs-an-intuitive-explanation)

## SNARKS versus STARKS

- 2 successful approaches to ZKPs are SNARKS and STARKS
- They are both types of general purpose proving systems
- Both follow similar processes
    - Setup of the proving system
    - Arithmetisation
    - Use of Polynomial Commitment Schemes
    - Transformation from an interactive to non interactive process

Of these steps it is the last 3 that are used each time a proof is created and verified. 
This [video](https://youtu.be/liOn-n4lqfA?feature=shared) provides an overview of their differences.

### Important Differences between SNARKS and STARKS

STARKS have a transparent setup, that is,  there is no hidden information used when creating the system.
The cryptographic assumptions underlying the systems are different : 
STARKS rely on the existence of a collision resistant hash function making them post quantum secure.
SNARKS often rely upon pairs of elliptic curves. In Mina, these curves are collectively know as the pasta curves, the same curves that are used for ZCash.

SNARKS typically have smaller proof sizes than STARKS, of the order of 1KB.

## Proving systems 
SNARK systems have evolved becoming more flexible and performant. 
    - An updateable setup means the system code can be updated without having to run the whole initial setup again.
    - PLONK systems has been adapted widely, there are many variants of the original PLONK system, referred to as Plonkish protocols.

## Kimchi

Kimchi is a proof system built for Mina, it is a variant of PLONK, a SNARK type proof system. Along with Pickles it allows infinite recursion when creating proofs.
Kimchi differs from many SNARK based proving systems in that it doesnt need a trusted setup containing secret information.
Although based on PLONK it incorporates a number of optimisations, such as a more flexible architecture for circuits, and the use of lookup tables to more efficiently represent some operations such as boolean logic. 

See [Docs](https://minaprotocol.com/blog/kimchi-the-latest-update-to-minas-proof-system)


## What are proving systems used for ?

Two popular ways that proving systems have been used are 
- To create privacy preserving applications that have private inputs. This relies on the 'zero knowledge' aspect of the proving system
- To create create proofs that some computation executed as intended. Because the proof is succinct this allows the verifier to check the computation much more efficiently than having to re run the computation. This concept has been widely used to make blockchains more scalable a technique known as zkRollups.



## What is a circuit and how is it created

In a zero knowledge proof, a circuit is a mathematical representation of the computation or statement being proven. It defines the problem that the prover is demonstrating they can solve without revealing the solution itself.

A circuit can be though of as a set of constraints that must be satisfied if the prover's claim is correct. 

zkApp developers will write typescript code and use the o1js library to provide the data types and methods that we want to be provable. 

The zkApp CLI provides tools that allow us to create the circuit from our typescript code.

See [Docs](https://docs.minaprotocol.com/zkapps/writing-a-zkapp/introduction-to-zkapps/how-to-write-a-zkapp)



## What are pickles and recursion? 

Recursion lies at the heart of the Mina protocol and allows a succinct constant size blockchain. 

Pickles is a recursion layer built on top of Kimchi. 
In order to produce recursive proofs Pickles needs to verify a previous Kimchi proof from within the current proof's circuit.

The use of recursion in Mina goes beyond its use in the protocol, it can also be employed in zkApps to allow more sophisticated and scalable applications.


## What are proofs, attestations and verification keys?

A proof is the cryptographic artifact created by the prover to convince the verifier that a statement is true, without revealing any underlying information. 

An attestation is the claim that is made by the prover, for example this could be a claim that a transaction has executed correctly, or that some data represents valid state in a blockchain.

When a proving system is initially setup  succinct summaries of the setup are created to be used by the prover and verifier, these are called the proving and verification keys.
The verification key is used by the verifier, along with the proof, and any public inputs to check the validity of the proof.


## Q&A

1. What is the primary characteristic of a zero-knowledge proof (ZKP)?

a) It reveals all the details of the prover's solution.
b) It convinces the verifier of a claim without revealing the input.
c) It requires the prover to share their secret with the verifier.
d) It only works for simple mathematical puzzles.

2. Which of the following are two common types of ZKPs?

a) SHA-256 and RSA
b) SNARKS and STARKS
c) AES and DES
d) ECC and Diffie-Hellman

3. What is a key advantage of STARKS over SNARKS?

a) Smaller proof sizes
b) Post-quantum security
c) Reliance on elliptic curve cryptography
d) Faster proof generation

4. What is Kimchi in the context of Mina protocol?

a) A type of cryptocurrency
b) A consensus mechanism
c) A proof system variant of PLONK
d) A smart contract language

5. What does recursion enable in the Mina blockchain?

a) Larger block sizes
b) Increased transaction throughput
c) A succinct and constant-size blockchain
d) Smart contract execution

6. What is a circuit in a zero-knowledge proof?

a) An electronic component
b) A visual representation of a proof
c) A mathematical representation of the computation being proven
d) A programming language for zkApps

7. What is the role of Pickles in Mina?

a) A recursion layer built on top of Kimchi
b) A type of SNARK proof
c) A programming library for zkApps
d) A consensus mechanism

8. What is an attestation in the context of zero-knowledge proofs?

a) A cryptographic key
b) A claim made by the prover
c) A type of proof
d) A verification algorithm

9. What is the purpose of a verification key?

a) To generate a proof
b) To encrypt data
c) To check the validity of a proof
d) To create a zkApp

10. Which of the following is NOT a common use case for proving systems?

a) Privacy-preserving applications
b) Scalable blockchains (zkRollups)
c) Data encryption
d) Verifying computations efficiently



11. True or false 
- SNARKS have a transparent setup

12. Kimchi is
- A consensus mechanism used in Mina
- A custom proof system in Mina
- A STARK style proof system

13. Circuits are used to 
 - Specify the constraints in a proof system
 - Specify how the Mina network connects nodes
 - Compile programs for use in Mina

