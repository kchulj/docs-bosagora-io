# Consensus Algorithm

The consensus algorithm is central to any blockchain-based currency or system. The consensus algorithm attempts to answer the question, “How can we prove with confidence that all distributed databases hold the same set of information?”

As blockchains have evolved, so too have the consensus algorithms. The first generation was based on a *Byzantine Agreement* (BA). BA requires that all the nodes in the blockchain form a consensus. Requiring unanimous agreement can be challenging as the number of blockchain nodes grows.Z

## FBA

The next generation of consensus algorithms are based on *Federated Byzantine Agreement* (FBA). Rather than have every node in the blockchain vote on consensus, a network consisting of *quorums* votes on consensus, where each quorum is a set of nodes sufficient to reach an agreement. The consensus process is achieved via the quorums, and the collective agreement of the quorums is used as the final decision of the entire network. FBA powers the [Stellar Network](https://www.stellar.org/), the 8th largest cryptocurrency with a market capitalization of over $2.5 billion.

There are two main features that make FBA suitable for the Bosagora consensus protocol. First, because it doesn’t have to wait to hear from every node, confirmation of the transaction is **fast** (transactions confirm every 3 – 5 seconds). As a utility coin, confirmation speed and low latency are critical to be utilized in a real-life environment.

Second, because validators are not chosen by someone or some organization, membership in the blockchain is completely **open** to the public. This is in contrast to the Stellar Network, where everyone who wants to join the network needs permission from someone.

## mFBA

For Bosagora, it is not only important for anyone to be able to join the network, but also for them to be able to participate in validation without authorization. The way we do that is by combining Proof of Stake (PoS) with FBA, which we refer to as modified FBA (mFBA).

In this case, we use PoS for the maintenance of the governance system. Anybody can be a validator, as long as they *stake* 40,000 BOA cryptocurrency within a node and forgo liquidity (i.e., they can’t sell that BOA).

The frozen BOA in the node acts as both an economic incentive (via confirmation rewards) to operate a node, as well as collateral for the security and integrity of the information held in the node’s blockchain. According to the pre-set rules, if a node is discovered to have forged the blockchain on the node, the frozen BOA are forfeited to the Commons Budget.
