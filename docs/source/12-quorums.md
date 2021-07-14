# Quorums

## Overview

Recall that FBA protocols implement a non-unanimous consensus mechanism by grouping nodes into groups known quorums. In general, a quorum is the minimum number of people who must participate in a vote in order for a certain proposal to be executed. In the early stage of the Bosagora platform, a quorum for resolution was set to one third of the total members. However, this can be adjusted later to reflect the average participation rate.

Initially, quorums were based on Stellar’s consensus protocol (SCP). But it has a weak point. The quorums on Stellar are configured manually by each node maintainer. This can lead to too much centralization if the quorums aren’t configured properly. Bosagora addresses that shortcoming by using *quorum balancing* (see below).

The rules for generating quorums on the Bosagora platform are as follows:

+ Nodes with a bigger stake have a higher chance of being included in other nodes’ quorums.
+ The probability of inclusion is equal to the percentage of a node’s stake compared to the stake of other nodes in the network. For example: If validators A, B, C stake 100K, 200K, 300K each, then validator C has a greater chance of being included in a node’s quorum configuration compared to A and B.
+ Randomness ensures that each node does not have the exact same quorum layout, as that would lead to too much centralization.
+ At specified intervals, the quorums are shuffled.

There are several checks to make sure quorums are generated correctly:

+ There is a check that threshold values are correct.
+ There is a quorum intersection check adapted from Stellar. It verifies there is sufficient quorum intersection in a given quorum configuration.
+ There is a verification that network splits are not possible with the given quorum configuration.

## Quorum Slicing

In an effort to incorporate trusted business relationships into the consensus process, FBA introduced the concept of a *quorum slice*. A quorum slice is a subset of nodes in a quorum that a given node chooses to trust and depend on. Validators get to decide which other validators they trust, and their list of trusted validators becomes their quorum slice. 

Every Bosagora validator node must be part of at least one quorum slice. A individual validator node can however appear in multiple quorum slices. Using quorum slices of trusted nodes not only produces quicker consensus, but also ensures greater stability and reliability. Because these trusted nodes carry more weight in reaching consensus, even if a bad actor were to add a million malicious nodes to the network, it won’t have any effect unless they can convince a critical mass of nodes to include them in their quorum slices.

## Quorum Balancing

The problem with letting validators manually configure quorums is the opportunity for bias and centralization. This is the situation with SCP. The Bosagora team addressed this shortcoming by automating the quorum creation process which is referred to as *quorum balancing*. Quorum balancing helps everyone participate as a validator and is essential to realize a truly open membership.

The idea is to make quorum configuration completely automated so there is no need for manual quorum configuration. Bosagora uses the set of all registered validators to automatically generate each node’s quorum set. This ensures the quorum configuration is sufficiently decentralized.

How does Bosagora ensure fairness in the configuration process? By using the pre-imaging technology from the consensus protocol to derive a randomness seed. This seed is then used as input to a deterministic pseudo-random number generator (PRNG). The PRNG then  generates a specific sequence of numbers for a given seed (which ensures verifiability). This seed is then used to introduce randomness into the quorum.

To further ensure fairness and randomness, the quorums are shuffled at specified intervals. This activity is referred to as *quorum rebalancing*. Currently quorum rebalancing happens every hour.
