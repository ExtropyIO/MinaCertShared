# Overview

Protokit allows developers to build their own application-specific blockchains, where the features of the application are the features of the blockchain.

Caveat - under active development and changing quickly

## Architecture and features

Here's a breakdown of the features enabled by Protokit

- **Hybrid Execution Model:** Protokit uses a hybrid execution model, which allows for both off-chain and on-chain execution. This means that some parts of the application's logic can be executed on the client-side, generating zero-knowledge proofs, which are then submitted to the blockchain for verification. This approach enables private client-side execution, where a user can generate a proof locally, such as proving eligibility for an action, without revealing the details of their eligibility.  
    
- **Customisable and Modular Architecture:** Protokit is designed to be highly modular and customisable. Developers can replace any module of their app-chain. The framework consists of three main modularity layers: Runtime, Protocol, and Sequencer.
    - **Runtime:** The runtime layer is responsible for the business logic of the application chain. Developers implement runtime modules that define the specific application logic. Runtime modules are not limited to eight fields and can use key-value storage.
    - **Protocol:** The protocol layer defines how state transitions are applied to the underlying state tree and how proofs of state transitions are combined with proofs of runtime execution to form a block. It also determines how proofs of state transitions are brought together to form a block. The protocol can be extended with hooks to tap into the lifecycle of the protocol.
    - **Sequencer:** The sequencer layer is responsible for orchestrating the runtime and protocol, handling block production, the mempool, and settlement to the L1. It transforms unproven blocks into traces and provides user-facing APIs, like a GraphQL API, for inspecting internal state.
- **No Data Race Conditions:** Protokit chains do not have data race conditions due to sequenced transactions. The framework ensures that only valid and sequentially consistent state updates occur.  
    
- **Extensive On-Chain Storage:** Protokit chains offer effectively limitless on-chain storage, including key-value storage. The state map can have a large number of key-value pairs, with a default state tree height of 256, allowing for $2^{256}$ entries for the entire app-chain.  
    
- **Interoperability and Bridging:**
    - Protokit facilitates interoperability with the Mina L1 and other L2s.
    - It includes settlement and bridge contracts that enable the transfer of tokens between the Mina L1 and the Protokit L2.
    - A Merkle Mountain Range library is being developed to support bridging tokens from other blockchains like Ethereum.
    - It is possible to provably pass messages between L1 and L2, where developers can specify runtime methods that can be invoked by messages from L1. There is also a way to send messages from L2 to L1 but with some latency.
    - Custom token bridging is supported.
- **Settlement to L1:** Protokit outsources the settlement layer to the Mina L1 blockchain. Block proofs are created that tell the chain that a state transition is occurring and this is sent to the L1. The L1 consensus is used to settle the block proofs.  
    
- **Developer Experience:** Protokit aims for a supercharged developer experience by using TypeScript and o1js. It allows for the use of reusable modules and open-source libraries.  
    
- **Privacy:** Protokit enables privacy by using off-chain zero-knowledge proofs as arguments for on-chain transactions. The framework is built on Mina's o1js library, which is a zk-DSL allowing developers to write circuits that produce zero-knowledge proofs.  
    
- **Customisable Protocol:** Protokit allows for customisation of the underlying protocol via hooks that allow for the execution of tasks at predefined points.  
    
- **Data Handling**:
    - Protokit includes an indexer for historical data, enabling queries of past transactions and states using GraphQL APIs.
    - A data processor supports custom database schemas.
    - Runtime events can be emitted to capture transaction and state update information for later data processing.
- **Protokit as a Reducer:** Protokit functions like a reducer, allowing developers to manage application state changes and saving them the burden of handling the low-level infrastructure required to maintain state.  
    

**Caveats and Considerations:**

- **Single Sequencer Operator:** Currently, Protokit appchains rely on a single sequencer operator. The sequencer is responsible for block production and settlement to the L1.
- **Data Availability:** In the current version, data availability is handled by the sequencer, making Protokit application chains validiums. Data availability will be outsourced to the Mina L1 when the action/sequence state mempool module becomes available.
- **No Built-in Assertions:** The built-in assertion methods from o1js, such as `assertEquals`, cannot be used within runtime methods. This limits the usage of primitives that include range checks or call the built-in assertions.
- **Learning Curve:** While Protokit aims for a minimal learning curve, developers still need to understand TypeScript and some aspects of o1js.
- **Early Stage Development:** Protokit is in the early stages of development and developers are encouraged to provide feedback.
- **Potential for Reorgs:** Protokit needs a mechanism for protection against reorgs, due to the relatively long block confirmation time on Mina mainnet. If a reorg occurs on L1 and impacts batches of transactions sent from L2, the Sequencer on L2 could replay the affected transactions onto the new chain of L1.
- **Proof Generation Time:** Proof generation can take a significant amount of time.
- **Custom Tokens:** Custom token bridging is a separate integration that needs to be finished.
- **State Querying:** There are no built-in methods to query the whole state map of a runtime module.
- **Mobile Support:** There are no examples of mobile-based proof generation.

Overall, Protokit offers a powerful set of features for building privacy-enabled application chains on Mina, but it also has some caveats to consider, particularly around data availability and decentralisation of the sequencer.


# What is the difference between a zkRollup and an Appchain ?

![blockchain_L1_L2_L3.png](app://8a9505f0445c4f9583c1255bf3fce85cb7f6/Users/extropy/Work/Dev/MinaCertificationMaterial/graphics/blockchain_L1_L2_L3.png?1734190211670)  
A zk-rollup and an appchain are related concepts, with an appchain being a specific type of zk-rollup

- Zk-rollup: A zk-rollup is a layer-2 scaling solution that uses zero-knowledge proofs to ensure the validity of transactions.  
    Zk-rollups move transactions off-chain to improve scalability, while maintaining the security of the underlying layer-1 network.
    
- Appchain: An appchain is an application-specific form of a rollup, unlike general-purpose rollups.  
    This means that appchains are designed for a particular application and can be optimised to suit its needs, potentially offering faster block times and lower fees.
    

Key differences and relationships between the two are:

- Customisation: Appchains allow developers to optimise their rollup implementation for a specific application. With appchains, the features of an application are the features of the blockchain itself. Instead of deploying smart contracts, developers implement runtime modules and deploy them as their application chain.
    
- General Purpose vs. Specific Purpose: General-purpose rollups, like zkSync, aim to support a wide variety of applications, while appchains are tailored for a specific use case.
    
- Protokit's Role: Protokit is a framework for building privacy-enabled appchains  
    Protokit provides the tools to create zk-rollups that are application-specific.  
    It abstracts away the complexity of building a zk-rollup, allowing developers to focus on their application.
    
- Settlement: Protokit-based appchains can be settled to the Mina L1 blockchain, using L1 settlement contracts.  
    This anchors the state of the appchain to Mina and leverages its security1
    
- Modularity: Protokit is designed to be modular, and it is composed of the Runtime, Protocol and Sequencer layers.  
    Every layer accepts purpose-specific modules in Typescript. This modularity allows for a high degree of customisation.
    
- Hybrid Execution: Protokit offers a hybrid execution model, which means that code can run both on and off-chain.  
    This allows for client-side ZK proofs and sequential execution on the sequencer
    
- Smart Contracts vs Runtime Modules: Instead of implementing and deploying smart contracts, developers implement runtime modules and deploy them as their application chain.  
    Smart contracts are circuits that produce a proof of their own execution. Protokit runtime modules are executed by the sequencer, not off-chain
    

In summary, a zk-rollup is a general scaling solution that uses zero-knowledge proofs, while an appchain is a specific type of zk-rollup tailored to the needs of a particular application Protokit is a framework for building appchains on the Mina blockchain


# Runtime Configuration

The Protokit runtime can be configured at three different levels: runtime, chain, and client

Runtime configuration

- The overall runtime configuration specifies the definition and layout of runtime modules
    
- A runtime module consists of configuration, storage and methods.
    
- Each runtime module must extend the RuntimeModule class and be decorated with the `@runtimeModule()` decorator.
    
- The configuration of a runtime module is immutable during execution. Values defined as configuration become part of the underlying zero-knowledge circuits as constants and are accessible via `this.config`
    
- Runtime modules can define their own storage, such as a ledger of type state map
    
- Runtime modules can contain methods, specifically runtime methods, that can be called by users via transactions, which are decorated with `@runtimeMethod()`.
    
- Runtime modules are responsible for managing their own state.
    
- Runtime modules within the same runtime are aware of each other and can call each other's methods and access each other's state, allowing for modular development
    
- A runtime module can have a configuration object, which if empty can be signified by Record<string, never>
    
- A runtime module can define state using the `@state() decorator`. State can be a single value using `State.from()` or a key-value pairing using `StateMap.from()`
    
- The set state API does not work with options; values should be passed directly.
    

For example, a Balances runtime module can be configured with a totalSupply and can store balances as a StateMap where keys are PublicKey and values are UInt64, as well as having a circulatingSupply as a single State  
The Balances module can have a setBalance method that sets the balance for a given address, and an addBalance method that allows tokens to be minted.  
The module can be configured with a totalSupply

```
import { RuntimeModule, runtimeModule, state, runtimeMethod } from "@proto-kit/module";
import { State, StateMap, assert } from "@proto-kit/protocol";
import { Balance, Balances as BaseBalances, TokenId } from "@proto-kit/library";
import { PublicKey } from "o1js";

interface BalancesConfig {
    totalSupply: Balance;
}

@runtimeModule()
export class Balances extends BaseBalances<BalancesConfig> {
    @state() public circulatingSupply = State.from(Balance);
    // implicitly inherited from `BaseBalances`
    // @state() public balances = StateMap.from(..);
    @runtimeMethod()
    public addBalance(tokenId: TokenId, address: PublicKey, amount: Balance) {
        const circulatingSupply = this.circulatingSupply.get();
        const newCirculatingSupply = Balance.from(circulatingSupply.value).add(
            amount
        );
        assert(
            newCirculatingSupply.lessThanOrEqual(this.config.totalSupply),
            "Circulating supply would be higher than total supply"
        );
        this.circulatingSupply.set(newCirculatingSupply);
        this.mint(tokenId, address, amount);
    }
}
```

Chain and Client Configuration

• The runtime configuration is used to define app-chain configurations for both client and server-side app-chains

- chain.config.ts is used by the Protokit CLI to start a server-side app-chain
    
- client.config.ts is used by the Protokit SDK to connect to the server-side app-chain via GraphQL
    
- Configuration for the protocol and sequencer is provided implicitly
    
- The starter kit provides pre-configured environments such as in memory for development without data persistence
    

A typical runtime.ts file, which defines the modules and their configurations, would look like this:

```
import { Balance } from "@proto-kit/library";
import { Balances } from "./balances";
import { ModulesConfig } from "@proto-kit/common";
import { GuestBook } from "./guest-book";

export const modules = {
    Balances,
    GuestBook,
};

export const config: ModulesConfig<typeof modules> = {
    Balances: {
        totalSupply: Balance.from(10_000),
    },
    GuestBook: {},
};

export default {
    modules,
    config,
};
```

A typical chain.config.ts file, which is used by the Protokit CLI to start a server-side app-chain would look like this:

```
import { LocalhostAppChain } from "@proto-kit/cli";
import runtime from "./runtime";

const appChain = LocalhostAppChain.fromRuntime(runtime.modules);

appChain.configure({
    ...appChain.config,
    Runtime: runtime.config,
});

export default appChain as any;
```

And a typical client.config.ts file, which is used by the Protokit SDK to connect to the server-side app-chain via GraphQL would look like this:

```
import { ClientAppChain } from "@proto-kit/sdk";
import runtime from "./runtime";

const appChain = ClientAppChain.fromRuntime(runtime.modules);

appChain.configurePartial({
    Runtime: runtime.config,
});

export const client = appChain;
```

Protokit also allows for the implementation of custom protocol modules, which can interact with runtime modules, and also implement TransactionHooks, which are called during transaction processing


# Runtime State

Runtime state in Protokit refers to the data managed by runtime modules within an application chain. The runtime is the first modular component of an app-chain, containing all the business logic of the application itself. Runtime modules define the runtime state and runtime methods of each module.

Here's a more detailed breakdown of runtime state:

- **State Management:**
    - Runtime modules are responsible for managing their own state.
    - The sequencer stores the runtime state, and it is accessible in a provable way within runtime modules.
    - Interactions with the state produce state transitions. However, the runtime itself does not apply state transitions to the Merkle tree.
    - **State is represented as an _optional_ value**, since it may or may not exist at the time it is read. This is handled by the use of dummy values when a real value is not present.
- **State Tree:**
    - From an app-chain perspective, there is only a single **state tree** shared between all runtime modules.
    - This requires a way to determine which state property belongs to which runtime module to avoid name collisions.
- **State Paths**:
    - A **state path** consists of the _runtime module name_ and the _state property name_.
    - In the case of a state map, the state path is extended with the _state key_ used to access the value.
    - The state API takes care of generating the state paths, so developers do not have to worry about it.
- **Types of State:**
    - There are two types of state/storage available for runtime modules: **`state`** and **`state map`**.
    - **`state`** is a single value.
    - **`state map`** is a mapping between two values (key-value).
    - A module can have an infinite number of state properties, and a state map can have a large number of key-value pairs.
    - The amount of available entries in the state map is subject to the size of the underlying state tree. By default, the state tree height is 256, allowing for 2^256 entries combined for the entire app-chain.
- **Accessing State:**
    - Accessing runtime state within a runtime module is done via the state API.
    - State is represented as an optional value, because it may or may not exist at the time when it is read.
    - If a state value does not exist, the option will carry a dummy value. This allows runtime methods to execute provably, even if state values are not available.
    - State can be read using the `.get()` method, which will return an `Option<T>`. If the state is a struct, you must use `.get().value` to access the struct.
    - When writing state, you can use the `.set()` method. Setting a value of an existing state key will overwrite the previous value.
- **State and Structs**
    - When storing structs in the state, you must instantiate the struct after retrieving it from the state.
    - State values are represented as options, and might not have a _real_ value, necessitating the use of dummy values when a real value is not available.
- **Inter-Module Access:**
    - Runtime modules can access state from other modules (both read and write) as long as they can reconstruct the module's state paths for each state property.
    - State and method access is permissionless within the same runtime, so developers should be careful when injecting dependencies.
- **State Transitions**:
    - Every interaction with state produces a state transition, where a state transition is effectively Merkle operations.
    - State transitions allow for the modelling of how a state moves forward, and also to define how a state is meant to look at a certain point in time.
    - State transition preconditions allow the sequencer to supply unchecked values during on-chain execution of the runtime, and still prove the correctness of values supplied within the protocol.
- **No Direct State Mutation:**
    - The runtime does not directly apply state transitions to the Merkle tree. This helps to keep the runtime circuits as simple as possible, enabling parallelisation of proof generation between business logic and state transition circuits.
- **State Querying**
    - There are currently no built-in methods for querying the whole state tree. One trick is to use an incremental key index in the state map for UI pagination purposes.
    - It is possible to retrieve a Merkle witness via a GraphQL API to verify that a state is included in a settled state tree.
- **State Persistence**
    - To ensure state persistence, appchains can be run on a cloud as a Docker container or some other form of OS instance.

