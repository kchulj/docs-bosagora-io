# Proof of Stake?

One of the chief components of any blockchain is the consensus algorithm. The consensus algorithm is the method by which all the nodes in the blockchain come to an agreement on what is in a block before it gets permanently stored there.

Consensus algorithms try and balance two requirements: they should be robust and efficient. In other words, you want the algorithm to ensure consensus using the least amount of resources. There are three main prototocols used in consensus algorithms for blockchains today.

The first protocol used—the one used for Bitcoin—is *Proof of Work* (PoW). It operates by having every node do a mathematically difficult computation. It’s a very safe (i.e., robust) algorithm, but very inefficient as it requires a considerable amount of computation power (from each node) and therefore requires a lot of electrical power.

The next generation of protocol is *Proof of Stake* (PoS). Here each node stakes some cryptocurrency (called *tokens*) for the right to vote on a transaction. Unlike PoW, PoS is not computationally intensive. It is however, not as robust as PoW.

The third protocol is *Delegated Proof of Stake* (DPoS). Like PoS, each node stakes some tokens for the right to vote. But in this case, the nodes don't vote on trasactions. Instead, they vote for *delegates* and the delegates vote on the transactions. Delegates are a subset of trusted nodes which are elected by the other nodes. Since only a subset of nodes has to validate transactions, consensus can be reached faster with DPoS. Fewer nodes voting however is also less robust.

Requiring unanimous agreement by all participating nodes (like PoW and PoS) is referred to as a *Byzantine agreement*. DPoS on the other hand, which does not require unanimous agreement by all nodes to reach consensus, is called a *Federated Byzantine agreement* (FBA). Since they don’t have to wait for a unanimous vote, FBA protocols result in faster blockchain transactions.

Bosagora uses a modified version of the Federated Byzantine agreement (mFBA) consensus algorithm. In addition to FBA, the Bosagora consensus protocol also applies a PoS feature for the maintenance of a governance system. Transaction validators are required to freeze 40,000 BOA within a node and keep them there. The frozen coins in the node then act as both an economic incentive (in the form of confirmation rewards) to operate a node, as well as collateral for the security and integrity of the information held in the node’s blockchain.
