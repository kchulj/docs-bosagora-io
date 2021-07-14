# UTXO Configuration

## The UTXO Model

Receiving and spending BOA is similar to how it’s done in Bitcoin in that all transactions involve UTXOs. UTXO, or *unspent transaction output*, is a fancy way of saying unspent coins or tokens. In other words, all transactions of BOA involve previously unspent BOA tokens.

Recall that one of the big challenges to decentralized cryptocurrency is the double spend problem. The UTXO model of cryptocurrency solves that problem by preventing double spending. How does it do that?

UTXOs are used as the input to every BOA transaction and each of those UTXOs are uniquely identifiable by its transaction ID. During the transaction, all the input UTXOs are in effect destroyed. Should the transaction result in any outputs, new  UTXOs, with new a transaction ID, are created. In this way, no UTXO can be spent twice because it is destroyed during spending.

When a transaction is completed, any unspent outputs (i.e., UTXOs) are deposited back into a database which can then be used as inputs at a later date for a new transaction. Network nodes record and maintain a database that contains every UTXO available for spending. If someone tries to use a UTXO that isn’t in that database, the nodes will reject it. The set of all existing UTXOs in the database at a given point in time is called the *UTXO set*.

## UTXO Tokens are Indivisible

In most BOA transactions, new output UTXOs will be created because BOA UTXOs are indivisible. As an example, suppose you receive 30 BOA and then 40 BOA as confirmation rewards. You have 70 BOA total.

Now, suppose you need to spend 35 BOA on a transaction fee. You can’t just spend 35 BOA because all you have is a 30 BOA UTXO and a 40 BOA UTXO and they aren’t divisible. It’s like buying something for 50 cents when all you have is a dollar bill. You’re going to have to spend the dollar and get change back.

Because UTXOs are indivisible, in the above transaction, you’ll have to spend the 40 BOA UTXO (i.e., the input) and receive a 5 BOA UTXO (i.e., the output) in return. As a result of the transaction, the input UTXO will be destroyed (removed from the database) and the new output UTXO will be created (added to the database).
