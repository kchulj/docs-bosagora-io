# Trust Contracts

To add smart contract functionality to the blockchain requires a couple of things. First, you’ll need some kind of programming language to create the kind of complex math and algorithms necessary to implement business rules on the blockchain.

The first attempts to add smart contracts to the blockchain, like Ethereum, included a Turing-complete programming language to write smart contracts. A Turing-complete system can be proven mathematically to be capable of performing any possible calculation or computer program.

However, it is possible that a Turing-complete language might be inappropriate for writing a smart contract as they are inherently *undecidable*. Due to this undecidability issue, a smart contract based on a Turing-complete language will make it difficult to know what a smart contract will do before running it.

The second thing you’ll need is some way to execute those programs faster than is possible in the native blockchain environment. Blockchains were designed for consensus and immutability, not computation.

To address both of these challenges, Bosagora has developed the idea of the *Trust Contract*. Trust Contracts provide a decidable and approachable framework for creating and executing smart contracts on the blockchain.

Trust Contracts enable the programming of decidable contracts, either by using a flexible programming language on a virtual machine or using a slightly less flexible, but decidable, domain-specific language.

To overcome performance limitations inherent in blockchain, Trust Contracts utilize [WebAssembly](https://developer.mozilla.org/en-US/docs/WebAssembly). WebAssembly provides a way to run code, written in multiple languages, on the web at near-native speed, with client apps running on the web that previously couldn’t have done so.

The ultimate goal of this architecture is to enable users to build a decidable contract, which ensures safe and accurate execution while maximizing its scalability.
