# Introduction

version 2.0 ([pdf version](https://tao.network/docs/technical-whitepaper-2.0.pdf))

## Abstract
As the Tao Network approaches its fourth year of consistent, flawless operation it has become clear that while the industry, consumers, and markets have become more sophisticated, the codebase has not and a major technological overhaul is required. The vast experience we have gained serving the interests of the music industry have crystalized the technological requirements of a cryptocurrency which may truly begin to disrupt the power structures which dominate the landscape.  A platform which would enable a “DeFi for music” brings with it not only a set of technological prerequisites, but consensus must remain true to the ethics and ideals of the music industry we have come to serve.  It is towards these noble ends that we are creating the means to manifest that future: Tao2.

## Introduction
The blockchain industry and the infrastructure of the Internet of Value are being built rapidly around the globe, and to many the atmosphere is eerily similar to the building of the Internet in the late ‘90s, with pioneers and dreamers coming together to build a new future. **Tao** is the first blockchain platform which has dedicated its focus to leveraging the latest of blockchain technologies towards a more democratized, egalitarian future for the music economy.  This upgrade shall achieve this vision through seamlessly merging an ecosystem of applications with cryptographic tokens used by millions of mainstream users with a unique blockchain infrastructure architecture allowing for fast, secure, frictionless payments and a trusted store of value.

The distributed systems which currently dominate the music economy have been researched in a “*permissioned setting*” where the number of participants in the system and their identities are common knowledge. In 2008, Satoshi Nakamoto - “proposed his celebrated “blockchain protocol” which attempts to achieve consensus in a permissionless setting: anyone can join (or leave) the protocol execution (without getting permission from a centralized or distributed authority), and the protocol instructions do not depend on the identities of the players” (see [here](#PassCrypto2017)). Later on, Ethereum with its Ethereum Virtual Machine (EVM) proposed several significant enhancements compared to Bitcoin, including Smart Contracts. Both Bitcoin and Ethereum have some issues, especially with transaction processing performance. In order to construct an efficient and secured consensus protocol for **Tao**, we tackle the following main bottlenecks of classic blockchains:
-   **Efficiency:** Existing blockchains as employed by major cryptocurrencies(e.g., Tao 1.0 or Ethereum) do not scale well to handle a large transaction volume, e.g. Tao 1.0 and Ethereum can handle around 7-10 transactions/second. 
-   **Confirmation times:** The original Tao blockchain took 7.5 minutes per block, and is significantly longer than network latency. Furthermore, a Tao 1.0 block requires 10 subsequent blocks following it so that it can be confirmed; thus it takes on average 1.5 hours for a transaction to be confirmed (with low confidence). While Ethereum uses a shorter block-time, the average confirmation time still remains relatively high, around 13 minutes [Cardano](#Cardano2017). These long confirmation times hinder many important applications (especially smart contract applications).
-   **Unwanted Fork Potential:** The problem of a forked chain consumes computational energy/time and creates potential vulnerabilities for different types of attacks..
-   **Trust** While the systems are trustless, those who create them are not.  As a result, existing music economy stakeholders from across the spectrum have rejected those platforms such as Ethereum for anything more than experimental use.

The Tao project began life in 2015 by directly engaging the most significant music industry stakeholders in order to gain their input as to the pain points present in their industry with the goal of potentially solving them with blockchain technology.  The Tao 1.0 cryptocurrency was launched in 2016 based on these conversations with specific features which were desired by the music industry:
-   **Proof of Stake** Allowing for artists, producers, and labels to participate in network consensus
-   **Masternodes** Allowing for the instant settlement of transactions and enhancing Layer 1 consensus
-   **Tokenization** Allowing for the digital representation of paper contracts as well as advanced automation
-   **Community** – Providing clear focus and dedication to serving the needs of the music industry, while directly engaging fans and artists alike

While these goals were achieved, certain other important aspects of cryptocurrency adoption were neglected.
-   **Market traction** Listings on multiple exchanges
-   **Technological modernization** Keeping in line with the latest in cryptocurrency and blockchain developments
-   **Developer support** Missing tools which would allow developers to create applications using the blockchain

With these lessons now learned, the Tao cryptocurrency protocol will be upgraded to a protocol known as “Tao 2.0” or “Tao2". This document delves into the specifics of Tao2, including its consensus mechanisms, operational performance, and technological features:
-   Random Generals to reduce the proof of stake attack surface, increase data reliability, and reduce fork potential
-   Additional randomization to guarantee fairness and prevent handshaking and Sybil attacks
-   Fast confirmation time and efficient, decentralized checkpoints for transaction finality and minimal potential rebase

To start dealing with these problems, in this paper, we present an overview architectural design of **Tao**’s masternode design called "Shifu". In particular, we propose Delegated Proof of Stake (DPOS) consensus, a Proof-of-Stake (PoS)-based blockchain protocol with a fair voting mechanism, rigorous security guarantees and fast finality. This presents a novel reward mechanism which, with this mechanism, the blockchain has a low probability of forks and fast confirmation times, plus the contributions and benefits of masternodes are fair in the sense that the division of rewards is a fair probabilistic computation.

### Structure of the remainder of the paper

* Section [Shifu Protocol (Masternode) Design](#Sec:MasternodeDesign): explains the intuition ideas and overall architectural design of the Delegated Proof of Stake consensus mechanism, framework and background protocols that help mass readers (e.g., investors, traders, others) who may not have the technical knowledge to understand our mechanism easily.
* Section [Stakeholders, Delegates, & Voting](#Sec:StakeVoting) presents **Tao** stakeholder policy, masternode candidate delegate voting systems, and reward mechanism.
* Section [Tao consensus protocol](#Sec:ProtocolOverview) explains the motivation and Random Generals process as well as finality checkpoint of the protocol.
* In Section [Protocol formalizations](#Sec:ProtocolFormalization), we present the formalization of our model in a mathematical way to show the soundness of our model and protocol.
* Section [Security Analysis](#Sec:SecurityAnalysis) discusses the security analysis and resistant strain of potential attacks.
* We discuss and compare **Tao** with several existing blockchains in Section [related work](#Sec:relatedwork).
* Finally, we conclude the paper in Section [Conclusion](#Sec:Conclusion).

## Shifu Protocol (Masternode) Design {#Sec:MasternodeDesign}

### Tao architecture {#Sec:TaoOverview}

The **Tao** blockchain is produced and maintained by a set of *masternodes* in a consistent manner through the **Tao consensus** protocol as shown in Fig. [architecture](#fig:architecture). These masternodes are full nodes which operate an Etherem Virtual Machine (EVM).  For a token holder to become a masternode, two requirements must be satisfied:
-   The token holder must hold at least a minimum required amount of tokens (see next section for more details).
-   The token holder must be one of the most voted masternode candidates in the system. The voting by token holders is credited through a *Voting DApp* that allows token holders to *send TAO as a Delegate through the smart contract mechanism*.

In addition to the voting system which is an improvement over the current Bitcoin and Ethereum blockchain consensus mechanisms, Tao also provides a new technique, *Random Generals*. This new technique significantly decreases the probability of having invalid blocks in the blockchain, dramatically reducing the overall attack surface. These enhancements and the components of **Tao** are detailed step-by-step in the following sections.

![architecture](/assets/architecture.jpg){#fig:architecture}

## Stakeholders & Voting {#Sec:StakeVoting}

### Token holders, Masternodes {#coin-holders-masternodes .unnumbered}

Token holder is as simple as its name: users who join the network, who own and transfer TAO. Masternodes are full-nodes which maintain a copy of the blockchain, produce blocks and keep the chain consistent. It is worth noting that **Tao** is an extremely energy efficient cryptocurrency platform, as it does not use costly dedicated mining equiment as is required by Proof-of-Work-based blockchain systems.  Only masternodes can produce and validate blocks, and in a mechanism known as Delegated Proof of Stake.

Masternodes are selected via where token holders vote for block producers via an amount of TAO called a Delegate. The first requirement of being masternodes is to deposit 100,000 TAO to the Voting Smart Contract. These depositors are listed as masternode candidates in the Voting DApp, which allows token holders to vote for them by sending a Delegate to the smart contract in the name of that masternode.

Masternodes which process valid states to create and verify blocks will be incentivized with TAO. Furthermore, token holders who vote for these incentivized masternodes will also receive TAO in proportion to the amount of their Delegate. 

The list of masternode candidates is dynamically sorted based on Delegate counts. The performance of the masternodes will be tracked and reported back to the token holders in terms of three main metrics: CPU/Memory charts which ensure the workload of the masternodes, the number of signed blocks which indicates their work performance, and the last signed block which figures out their last activity. Token holders, at any time, can unvote masternodes, who have low performance, and provide their Delegates to the other masternodes which display superior performance. As lower performing masternodes lose Delegates, they will eventually be denied the ability to create and sign new blocks.  This mechanism keeps the system healthy and scalable as masternodes must always outperform their peers to maintain a superior production rate and thereby earn the most TAO. Therefore, only the strongest masternodes are voted for and can flourish.

###Voting & Masternode Pool {#voting-masternode-pool .unnumbered}

There are a maximum one hundred fifty (150) masternodes elected in the masternode pool. The required amount of deposit for a masternode role is set at 100,000 TAO. This amount is locked in a *voting smart contract*. Once a masternode is demoted (by not remaining in the top one hundred fifty voted masternodes) or intentionally quits the masternode candidates list/masternode pool, the deposit will have been locked for a month.

Token holders can vote at any time, by any number of votes (which is actually counted by the amount of TAO they bet on each masternode candidate). They can use the masternode performance statistics in the governance *Voting DApp* to determine which masternode candidates to support with their votes. The list of masternodes is dynamically sorted by the amount of TAO and counted up to one hundred fifty, upon reception of votes.

### Reward Mechanism {#reward-mechanism .unnumbered}

For each iteration of 360 blocks (called an epoch), a checkpoint block is
created, which implements only reward works. The masternode, which takes
its turn in the circular and sequential order to create blocks, has to scan
all of the created blocks in the epoch and count the number of signatures.
The reward mechanism is designed as follows: the
higher the number of signatures one masternode has made, the more rewards it
earns. For instance, within an epoch, masternode A which has sealed twice
the blocks of masternode B earns double the amount of TAO than
masternode B does.

Furthermore, there is also a reward sharing ratio among token holders and
masternodes who have been elected supported by the token holders.
Specifically, each epoch consists of 360 blocks, which will reward a total of 360 TAO in the first two years.
This amount of 360 TAO will be divided among all of the Masternodes proportionally to the number of signatures they sign during the epoch.

Afterward, the rewards achieved by each Masternode  will be divided into three portions.
-   **Infrastructure Reward**: The first portion of 40% called **Infrastructure Reward** goes to the Masternode.

-   **Staking Reward**: The second portion of 50% called **Staking Reward** goes to the pool of all voters for that Masternode which is shared proportionally based on the token stake.

-   **Foundation Reward**: The last portion of 10% called **Foundation Reward** goes to a special account controlled by the Masternode Foundation, which is run by the **Tao** community initially.

It is worth noting that coin-holders who unvote before the checkpoint block will not receive any shared reward in the **Staking Reward** portion.

## Tao Consensus Protocol {#Sec:ProtocolOverview}

### Random Generals Process {#double-validation-process .unnumbered}

In Tao, masternodes share equal responsibility to run the system and keep
it stable. Full nodes should run on powerful hardware configuration and
high-speed network connectivity in order to ensure the required block
time (target to five seconds). Only masternodes can produce and seal
blocks. In order for that, the **Tao** consensus relies on the concept of
**Random Generals** that improves some existing consensus mechanisms,
namely **Single Validation**. In the following, we first describe
**Random Generals**, then analyze the differences and improvements of
**Random Generals** compared to **Single Validation**.

### Random Generals (DV)

Similar to some existing PoS-based blockchains such as [Cardano](#Cardano2017), each
block is created by a block producer, namely masternode, that takes its
block creation permission turn following a pre-determined and circular
sequence of masternodes for each epoch. However, differently from these
existing blockchains, DV in **Tao** requires the signatures of two masternodes
on a block to be able to push the block to the blockchain. One of the
masternodes is the **block creator** while the other one, namely **block
verifier** is randomly selected among the set of voted masternodes that
validates the block and signs it. In the followings, for more
convenience, **block creator** and **block verifier** are used
interchangeably for the masternode 1 (block producer) and the randomly
selected masternode 2 for a block, respectively. The process of randomly
selecting the block verifiers is detailed in the next paragraphs. Note
that, there is no mining in the block creation as in Proof-of-Work-based
blockchains (e.g. Ethereum and Bitcoin). It means that a created block
is valid if and only if it is sealed by enough two signatures from a
block creator and a corresponding block verifier to confirm the
correctness of it.

We believe this DV technique enhances the stability of the blockchain by
diminishing the probability of producing “garbage” blocks while still
maintaining the system security and consistency. Randomization of block
verifiers in DV is the key factor of reducing risks coming from paired
masternodes trying to commit malicious blocks. Furthermore, comparing to
some current public blockchains in the market, by utilizing the DV
technique, **Tao** brings significant improvements in the block time by only
requiring two signatures per block. For the purpose of showing our
enhancement over existing PoS-based blockchains, we analyze the
differences between DV and the Single Validation mechanism in some
existing blockchains as follows.

### Improvements of Random Generals over Single Validation

Let’s show the improvements of DV compared to Single Validation through
analyzing some attacking scenarios as shown in Fig.
[Single Validation example](#fig:singlevalidation) and Fig. [Random Generals example](#fig:doublevalidation).

-   **Single Validation** In Single Validation, in an epoch, each
    masternode, e.g. M1, sequentially takes its turn to create a
    block, e.g. block100. The next masternode, e.g. M2, in the sequence
    then validates the created block100. If block100 is invalid (that
    potentially means that M1 is an attacker) and contains a transaction
    that invalidly benefits M1, if M2 is honest (see Fig.
    [SV a](#fig:singlevalidation)), it rejects block100 and creates
    another block100 next to block99. But, if M2 is an attacker
    (see Fig. [SV b](#fig:singlevalidation)) that cooperates with M1,
    M2 ignores the invalidation of block100, signs it and creates the next
    block, namely block101 that is valid. Then, the next masternode M3
    verifies that block101 is valid, M3 signs block101 and creates a
    block102. By doing it this way, Single Validation potentially leaves the
    blockchain with “garbage” or invalid blocks which require a “rebase”
    to restore the validity of the blockchain.


![singlevalidatioin](/assets/singlevalidation.jpg){#fig:singlevalidation}*Single Validation (SV): (a) SV with block creation masternode as an attacker and (b) SV with two consecutive block creation masternodes as attackers*

-   **Random Generals** We claim that our DV technique significantly
    reduces the probability of having garbage blocks in the blockchain.
    Assuming that M1 and M2 are the block creator and block verifier,
    respectively, for block100 in our DV. If block100 is invalid and M2
    is honest (see Fig. [DV a](#fig:doublevalidation)), M2 will not
    seal this block. Therefore, the next block creator M3 for creating
    block101 will see that block100 does not have enough 2 signatures,
    thus reject block100 and create another block100 next to block99. On
    the other hand, if M2 is also an attacker pairing/handshaking with
    M1 (see Fig. [DV b](#fig:doublevalidation)), M2 signs block100
    despite its invalidity (remember that the block verifier M2 is
    randomly selected), there is little chance of successfully pairing
    M1 and M2). Next, even though M3 will verify that block100 has two
    valid signatures, M3 still rejects it because block100 is
    invalidated by M3 that will create another valid block100. In order
    to break the stability and consistency of the blockchain in this
    case, M3 would need to be an attacker together with M1 and M2, which,
    however, has a very low probability. In other words, DV strengthens
    the consistency of the blockchain and makes it harder to break.


![doublevalidatioin](/assets/doublevalidation.jpg){#fig:doublevalidation}*Random Generals (DV): (a) DV with block creator as an attacker and (b) DV with both block creator and block verifier as attackers*

Randomization for Block Verifiers for Random Generals {#randomization-for-block-verifiers-for-double-validation .unnumbered}
----

### The First Masternode/Block Creator {#the-first-masternodeblock-creator .unnumbered}

The first masternode/block creator in a given epoch $e$ can be selected
by a round-robin game and can be formally defined as an array:

$$\begin{bmatrix}
\nu_1
\end{bmatrix}
= \begin{bmatrix}
V_{1.1}^e  \\
V_{1.2}^e\\
\cdot\\
\cdot\\
\cdot\\
V_{1.n-1}^e\\
V_{1.n}^e\\
\end{bmatrix}$$

### Random Matrix and Smart Contract {#random-matrix-and-smart-contract .unnumbered}

Let $m$ be the number of masternodes, $n$ be the number of slots in an
epoch. In order to randomly generate the block verifiers for the next
epoch $e+1$, the process is performed by the following steps.

-   **Step 1: Random Numbers Generation and Commitment Phase:**

    First, at the beginning of an epoch $e$, each masternode $V_i$ will
    securely create an array of $n+1$ special random numbers
    $ Recommend_i= [ r_{i.1}, r_{i.2}, ..., r_{i.n}, \theta_i]$, where
    $r_{i.k}\in [1, ..., m]$ indicating the recommendation of an ordered
    list of block verifiers for the next epoch of $V_i$, and
    $\theta_i \in \{-1, 0, 1\}$ is used for increasing the
    unpredictability of the random numbers. Second, each masternode
    $V_i$ has to encrypt the array $Recommend_i$ using a secret key $SK_i$, say
    $Secret_i = Encrypt (Recommend_i, SK_i)$. Next, each masternode forms a
    "*lock*” message that contains an encrypted secret array $Secret_i$; signs off this message with its blockchain’s private key through the Elliptic Curve Digital Signature Algorithm (ECDSA) scheme currently used in Ethereum and Bitcoin along with the corresponding epoch index and its public key generated from its private key. By doing this, every
    masternode can check who created this *lock* message through ECDSA verification scheme and which epoch
    it relates to. Then, each node $V_i$ sends their *lock* message with its signature and public key to a
    **Smart contract** stored in the blockchain, so that
    eventually each masternode collects and knows the *lock*s from all
    other masternodes.

-   **Step 2: Discovery and Recovery Phase:** The recovery phase is for every node to reveal its previous lock message so that other nodes can get to know the secret array it has sent before. A masternode only starts revealing its lock message if all masternodes have sent their lock messages to the smart contract or a certain timeout event occurs. Each masternode then opens its lock message by sending an ”*unlock*” message to the smart contract for other masternodes to open the corresponding lock. Imagine a commitment-like scheme in this case where a lock message is a commitment message locking its contained recommendation array $Recommend_i$ (so that no one can open or guess the contained array), and the unlock message gives the key for other masternodes to decrypt the box and retrieve the values of $Recommend_i$. Eventually, a masternode has both locks and unlocks of the others. If some elector is an adversary which might publish its lock but does not intend to send the corresponding unlock, other masternodes can ignore the adversary’s lock and set all its random values to *1* as default. The idea is simple: the network can keep working successfully even if some masternodes are adversaries.

-   **Step 3: Assembled Matrix and Computation Phase:** At the point of
    the slot $n^{th}$ of the epoch $e$, the secret arrays $Secret_I$ in
    the smart contract will be decrypted by each masternode and return
    the plain version of $Recommend_i$. Each tuple of the first $n$
    numbers of each $V_i$ will be assembled as the $i^{th}$ column of an
    $n \times m$ matrix. All the last number $\theta_i$ forms a
    $m\times 1$ matrix. Then each node will compute the block verifiers
    ordered list by some mathematical operations as explained below. The
    resulting output is a matrix $n \times 1$ indicating the order of
    block verifiers for the next epoch $e+1$.

### The Second Masternode/Block Verifier {#the-second-masternodeblock-verifier .unnumbered}

Then, each node will compute the common array $\nu_2$ for the order of
the block verifiers by the following steps as in the upper equation as follows below.
Then, $\nu_2$ is obtained by modulo operation of element values of
$\nu'_2$ as in the lower equation in the following:

$$\label{eq:matrix}
\begin{bmatrix} \nu'_2
\end{bmatrix}
=
\begin{bmatrix}
v_{2.1}^{e+1} \\
v_{2.2}^{e+1} \\
\vdots \\
v_{2.n}^{e+1}
\end{bmatrix}
=
\begin{bmatrix}
r_{1.1}  & r_{2.1}            & \cdots  & r_{m.1}  \\
r_{1.2}     & r_{2.2}       & \ddots  & \vdots   \\
r_{1.3}      &  \ddots   & \ddots  & r_{m.3}  \\
\vdots  &              & r_{m-1.n-1}  & r_{m.n-1}  \\
r_{1.n}      & \cdots      & r_{m-1.n}      & r_{m.n}
\end{bmatrix}
\begin{bmatrix}
\theta_1  \\
\theta_2  \\
\theta_3 \\
\vdots  \\
\theta_m
\end{bmatrix}$$

$$\label{eq:eq2}
\begin{bmatrix} \nu_2
\end{bmatrix}
=
\begin{bmatrix} \nu'_2 & mod & m
\end{bmatrix}
=
\begin{bmatrix}
\left| v_{2.1}^{e+1}\right| & mod & m \\
\left| v_{2.2}^{e+1} \right| & mod &  m\\
\vdots \\
\left| v_{2.n}^{e+1} \right| & mod & m
\end{bmatrix}$$

###Finality Analysis {#finality-analysis .unnumbered}


*"There is a standard definition of “total economic finality”: it takes
place when $\frac{3}{4}$ of all masternodes make maximum-odds bets that
a given block or state will be finalized. This condition offers very
strong incentives for masternodes to never try colluding to revert the
block: once masternodes make such maximum-odds bets, in any blockchain
where that block or state is not present, the masternodes lose their
entire deposit"* (see [here](#finality).

**Tao** keeps that standardization in the design so that one block is considered
as irreversible if it collects at least $\frac{3}{4}$ signatures of all
masternodes. The time-line of the blockchain creation process,
checking finality and marking the block as immutable is described as in
Figure: [ChainMaking](#fig:ChainMaking) below.

![ChainMaking](/assets/ChainMakingProcess3.jpg){#fig:ChainMaking}

## Consensus Protocol: Formalization {#Sec:ProtocolFormalization}

### Basic Concepts & Protocol Description {#basic-concepts-protocol-description .unnumbered}

In order to have a solid foundation for us to prove that our blockchain can achieve what is claimed, we first present our preliminary formalizations of the concepts that will be used in our yellow paper later.


To start, as we are dealing with a proof of stake consensus algorithm, we
follow the way of formalization in the recent works in the literature
like  [Cardano](#Cardano2017) and  [here](#Pass2017) and [here](#PassCrypto2017). In particular, we
recall the following concepts and definitions that were presented
in [Cardano](#Cardano2017) and adapt them to the context of Tao.

### Time, Slots, Epoch {#time-slots-epoch .unnumbered}
As previously described, ideally, each epoch is divided into 900 block time, that is called block slot.
Only one block can be created in a slot. We assume that there is a roughly synchronized clock that allows for masternodes to learn the current slot. This simplification will effectively permit masternodes to execute the signing and validation process of the DPOS consensus, where each masternode must collectively create a block to the current slot. For more simplification, each slot $sl_r$ is accessed by an integer $r \in \{1, 2, ...360\}$, and suppose that the real time window that corresponds to each slot has the following properties, which are similar to what are specified in [Cardano](#Cardano2017).

1. Every masternode can determine the index of the current slot based on the current time and ”any discrepancies between parties’ local time are insignificant in comparison with the length of time represented by a slot” [Cardano](#Cardano2017)

2. The amount of a slot time is sufficient to guarantee that any message transmitted by an honest party at the beginning of the time window will be received by any other honest party by the end of that time window. While this assumption is similar to [Cardano](#Cardano2017), Tao requires it in order for a block creator to propagate its created block to the corresponding block verifier to ensure that the block is signed by both the masternodes before the next block creator builds another block on top of it.


As mentioned in Section [TaoOverview](#Sec:MasternodeDesign), in our setting, we assume that the fixed collection of $m$ (150) masternodes
$V_1, V_2, ...., V_m$ interact throughout the protocol.
For each $V_i$ a public/private key pair ($pk_i$,$sk_i$) for a prescribed signature scheme, ideally ECDSA, is generated. Furthermore, we assume that the public keys $pk_1$,..,$pk_m$ of the masternodes are distributed and known by all of them (that means a masternode knows all public keys of other nodes). Some notable definitions of the blockchain concepts are defined following the notation in [here](#Garay2015).

- **State** A state (defined as in [here](#Cardano2017)) is an encoded string $st \in \{0,1\}^\lambda$.

- **Block** A block (defined as in [here](#Cardano2017)) $B$ generated at a slot $ sl_i \in \{sl_1,...,sl_R\}$
contains the current state $st \in \{0, 1\}^{\lambda}$, data
$d \in \{0, 1\}^{*}$, the slot number $sl_i$ and a signature
$\Sigma  =  Sign_{ski} (st, d, sl_i)$ computed under $sk_i$
corresponding to the masternode $V_i$ generating the block.

- **Blockchain** A blockchain (defined as in [here](#Cardano2017)) $C$ is a sequence of blocks $B_1,..., B_n$ associated with a strictly increasing sequence of slots for which the state sti of $B_i$ is equal to $H(B_{i−1})$, where $H$ is a collision-resistant cryptography hash function. A blockchain has a number of properties, including the length of a chain $len(C) = n$, which is its number of blocks, and the block $B_n$ is the head of the chain, denoted $head(C)$.

![al 1](/assets/al1.png)

As mentioned earlier, in our **Tao** model, we set each time *slot* $sl_i$ as 5
seconds; an epoch is a set $R$ of 900 slots
$\{ sl_1, sl_2, ..., sl_{900}\}$ (an epoch time duration equals to 1800
seconds).

In summary, the consensus protocol of **Tao** can be formalized in Algorithm ValidatorGeneration. The Algorithm ValidatorGeneration is simulated and explained as a
process shown in Fig. [EpochProcess](#fig:EpochProcess).

![image](/assets/Figure_Epoch.jpg){#fig:EpochProcess}

## Security Analysis {#Sec:SecurityAnalysis}

### Nothing-at-stake {#nothing-at-stake .unnumbered}

Nothing-at-stake is a well-known problem in PoS-based blockchains, just
like 51% attacks in PoW algorithms. PoW-based miners require CapEx
(capital expenditures) for buying mining equipment such as ASICs and
OpEx (operation expenditures) such as electricity to solve mathematical
puzzles securing the network (see [here](#capex)). That means, there is always an
intrinsic cost for miners in mining regardless of its success. In case
of a fork, miners therefore always allocate their resources (equipment and electricity)
to the chain that they believe is correct in order to get incentives for
compensating the intrinsic costs in mining.

To the contrary, in PoS-based systems without mining, during an ideal
execution for creating a fork, masternodes do not
incur intrinsic costs, other than  some block validation and
signing cost. As a result, there’s an inherent problem of the masternode
having no downside to staking both forks. Therefore, there are actually
two issues in the original design of PoS. On one hand, for any
masternode, the optimal strategy is to validate every chain/fork, so
that the masternode gets their rewards no matter which fork wins. On the
other hand, for attackers/malicious masternodes, they can easily create
a fork for double spending.

Let’s look back how **Tao** handles these two problems. As a reminder, **Tao** maintains
a certain order of masternodes in creating and sealing blocks in each
epoch. For the first issue, random/arbitrary forks are unlikely
because the order of block creation masternodes is pre-determined for
each epoch. Furthermore, the Random Generals mechanism eliminates the
second issue because even if one malicious masternode creates two blocks at
his turn, only one block then can be validated by the second randomly
selected masternode.

## Long-range attack {#long-range-attack .unnumbered}

In **Tao**, a block is valid only if it collects double validation and finalized
once $\frac{3}{4}$ of masternodes verify. Therefore, as long as the
number of attackers or malicious nodes and/or fail-stop nodes is less or 
equal than $\frac{1}{4}$ the number of masternodes, the number of
masternodes signing a block is at least $\frac{3}{4}$ the total number
of masternodes, which makes the block finalized. Thus, there is no
chance for one malicious masternode to create a longer valid chain because
other masternodes will refuse it.

### Censorship Attack {#censorship-attack .unnumbered}

If there are more than $\frac{3}{4}$ malicious masternodes in **Tao**,
a censorship attack might happen. For example, these masternodes refuse
valid blocks or simply become inactive. In this case, the chain is stuck.

In fact, masternodes are paid for their effort of correctly working so
that the chain is actively updated in a consistent manner. More
importantly, becoming a masternode means a certain amount of tokens are
locked, 100,000 TAO in particular. As a result, in order to control
more than$\frac{3}{4}$ masternodes, attackers must hold a considerable
amount of TAO and gain huge support from token holders. And because of
this, the attackers do not have incentives to do any malicious action to
harm the chain.

However, in the worst case, **Tao** has to do a soft fork in order to reduce the number
of masternodes to keep the chain running and figure out slasher
mechanisms for those malicious masternodes.

### Relay Attack {#relay-attack .unnumbered}

**Tao** supports [EIP155](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-155.md)
Transactions in **Tao** are included $CHAIN\_ID$ specified for different public
chains. Table \[table:chainid\] shows recognized $CHAIN\_ID$s.

  CHAIN\_ID  | Chain(s)
  -----------| ---------
  1          | Ethereum mainnet
  2          | Morden (disused), Expanse mainnet
  3          | Ropsten
  4          | Rinkeby
  30         | Rootstock mainnet
  31         | Rockstock testnet
  42         | Kovan
  61         | Ethereum Classic mainnet
  62         | Ethereum Classic testnet
  1337       | Geth private chains (default)
  77         | Sokol, the public POA Network testnet
  99         | Core, the public POA Network main network
  88         | Mainnet
  89         | Testnet


### Safety and liveness {#safety-and-liveness .unnumbered}

Safety implies having a single agreed upon chain where there are not two
or more competing chains with valid transactions in either (see [here](#Safety). A
consensus protocol can be *safe* when blocks have settlement finality,
or else probabilistic finality. This last sentence reveals that **Tao** can
provide safety because it has settlement finality.

A consensus protocol is considered *live* if it can eventually propagate
and make valid transactions onto the blockchain (see [here](#Safety). An occurrence
of a liveness fault is when transaction omission, information
withholding, or message reordering, among a number of violations are
observed. This type of fault is unlikely to happen in **Tao** because the block
creation masternodes list is ordered in a pre-determined way for each
epoch, thus even if an attacking masternode omits some transactions, the
latter will be processed and validated by the next honest masternode in
the next block.

### DDOS Attack {#ddos-attack .unnumbered}

Masternodes are encouraged to run in well-known public cloud providers
such as AWS, Google Cloud or Microsoft Azure which provides multiple
DDOS prevention mechanisms. Even if some nodes are attacked or
fail-stop, the network still works correctly as long as the number of
failing and/or attacked nodes is less than 1/4 of the number of
masternodes.

### Spam Attack {#spam-attack .unnumbered}

**Tao** keeps the same transaction fee mechanism as Ethereum which is indicated
via gasPrice. However, **Tao** supports minimum transaction fees (at 1 Wei),
which may lead to spamming, ie: an attacker tries to broadcast a huge
amount of low fee transactions to the system. However, **Tao** masternodes
always sort transactions and pick up only high fee transactions into the
proposing block. Thus, spammers have little chance to harm the system.

## Related work {#Sec:relatedwork}

Consensus plays an important role to guarantee the success of
distributed and decentralized systems. Bitcoin’s core consensus
protocol, often referred to as Nakamoto consensus [Bitcoin](#Bitcoin08), realizes a
“replicated state machine” abstraction, where nodes in a permissionless
network reach agreement about a set of transactions committed as well as
their ordering  (see [here](#hybrid). However, known permissionless consensus
protocols such as Bitcoin’s Nakamoto consensus come at a cost. Bitcoin
and Ethereum rely on PoW to roughly enforce the idea of “one vote per
hashpower” and to defend against Sybil attacks. Unfortunately, PoW-based
Bitcoin and Ethereum are known to have terrible performance (Bitcoin’s
transaction processing performance is at peak of around 7 transactions
per second as previously mentioned). Moreover, PoW is much criticized
because it costs a lot of electricity energy.

In order to design an efficient and cost-effective consensus protocol in
the permissionless model, PoS has been discussed extensively in the
Bitcoin and [Ethereum forum](#Ethe2014). A PoS blockchain can
substitute the costly PoW in Nakamoto’s blockchain while still providing
similar guarantees in terms of transaction processing in the presence of
a dishonest minority of users, where this “minority” is to be understood
here in the context of stake rather than computational
power [Cardano](#Cardano2017). The Ethereum design [Casper](#Casper), published by
Buterin & Griffith, provides as its initial version a PoW/PoS hybrid
consensus protocol, which might eventually switch to a pure PoS system.
As in **Tao**, Ethereum Casper requires that *validators* (term similar to
block creators) have to deposit an amount. In fact, some concepts used
in **Tao** such as checkpoint blocks are borrowed from Casper. Our (DPOS)
consensus protocol proposed in this paper can be seen as a hybrid model.
In particular, first, we apply with voting and **Random Generals** to
create, verify and vote for blocks smoothly and efficiently. Whenever
potentials of fork branches are detected, we employ the idea in PoW to
select the longest branch with the most votes and discard the other
branches. This hybrid approach not only increases the
performance and security of the blockchain, but also reduces the fork
situation in an efficient and practical manner.

Recently, there are several consensus protocol research works that are
closely related to **Tao** such as [EOS](#EOS) and Ouroboros of
[Cardano](#Cardano2017). The mechanism of *voting* for masternodes for
reaching consensus is utilized by [Bitshares](#bitshare) and [EOS](#EOS),
whose consensus protocol is termed *Delegated Proof-of-Stake* (DPoS).
DPoS is similar to the Proof-of-Stake Voting consensus of **Tao** in the sense
that masternodes (block creators or *witnesses* in DPoS) are elected
through a voting system. However, **Tao** requires that masternodes need to
deposit a required minimum amount of TAO to become a masternode
candidate, which puts more pressure on the masternodes to work honestly.
Furthermore, the **Random Generals** mechanism of **Tao** lowers the
probability of handshaking attacks and having invalid blocks, as
previously analyzed. EOS also has a maximum of 21 block producers for
each epoch, which is *less decentralized* than **Tao** with a maximum of 150
masternodes elected (and this number of masternodes can be changed following the decentralized governance through voting).

The research-backed [Cardano](#Cardano2017) blockchain solution, namely
Ouroboros, with the ADA coin, which is purely based on Proof-of-Stake,
promisingly claims to provide rigorous security guarantees. Similarly to
**Tao**, Ouroboros has a set of block producers for each epoch for creating
blocks and each block producer candidate needs to deposit a minimum
amount of stake (an amount of ADA). However, note that, Ouroboros only
provides **Single Validation**, while **Random Generals** of **Tao** provides
several advantages over Single Validation, as previously analyzed. In
Ouroboros, the order of block producers, selected among stakers, is
based on a biased randomization while the **Tao**’s randomization for block
verifiers is potentially uniform and based on smart contracts.
Furthermore, the use of voting as in **Tao** and DPoS enables a more incentive
equality between stakers: In Ouroboros, stakers with very little stake
have a very small probability of becoming block creators, while, in **Tao**,
these stakers can choose an optimal strategy to vote for potential
masternodes to get incentives.

## Conclusion and perspectives {#Sec:Conclusion}

In this paper, we proposed DPOS, a PoS Voting-based blockchain protocol
with heuristic and fair voting mechanism, rigorous security guarantees,
and fast finality. We also presented a novel reward mechanism and show
that, with this mechanism, the blockchain has a low probability of
having forks, fast confirmation time, plus the contributions and
benefits of masternodes are fair in the sense that the probability
distribution function is uniform eventually.

## Perspectives {#perspectives .unnumbered}

-   **Future work** The **Tao** team is currently working on the implementation
    of the Proof-of-Stake Voting, which will be released on schedule as
    stated in our roadmap. Furthermore, in parallel with our novel
    consensus protocol, we will investigate the Sharding mechanism in
    order to provide even better transaction processing performance. We
    believe that, the Sharding technique with the stable number of
    masternodes will provide better stability and efficiency to
    the blockchain. At the same time, we commit to keep EVM-compatible
    smart contracts within our masternode sharding framework.

-   **Economic sustainability** is also an important concept for a
    blockchain based decentralized network. That means to maintain the
    network in a sustainable condition, an equilibrium needs to be
    achieved, in which the cost of running the network infrastructure
    could be offset by the revenues generated. In this context, the cost
    of network infrastructure consists of two parts: the physical cost
    of having hardware such as servers, memory that passes the network
    technical requirements; and the capital cost of having TAO locked
    into smart-contracts. The revenues for Masternodes would primarily
    come from Reward Engine emission, and later on from service revenues
    such as token exchange fees provided by applications running on top
    of Tao. We will publish a Tao economic analysis and
    proposal, separate from this technical paper in a later date.

## References {#Sec:References}

Satoshi Nakamoto. Bitcoin: A peer-to-peer electronics cash system. 2008. [pdf](https://bitcoin.org/bitcoin.pdf){#Bitcoin08}

Ethereum Foundation. Ethereum’s White Paper. , 2014. Online available 25/05/2018. [link](https://github.com/ethereum/wiki/wiki/White-Paper){#Ethe2014}.

D. Larimer. Delegated Proof-of-Stake (DPOS). BitShare White Paper 2014. [link](https://bitshares.org/technology/delegated-proof-of-stake-consensus/){#Larime2016}.

S. King and S. Nadal. PPCoin: Peer-to-peer crypto-currency with
proof-of-stake. Self-Published, 2012. [pdf](https://peercoin.net/assets/paper/peercoin-paper.pdf){#King2012}

V. Buterin. On public and private blockchains. Ethereum Blog, 2015. [link](https://blog.ethereum.org/2015/08/07/on-public-and-private-blockchains/){#Vitalik2015}.

A. Kiayias, A. Russell, B. David, and R. Oliynykov: Ouroboros: A
Provably Secure Proof-of-Stake Blockchain Protocol. IACR-CRYPTO-2017.[pdf](https://eprint.iacr.org/2016/889.pdf){#Cardano2017}

D. Mingxiao, et al. A Review on Consensus Algorithms of Blockchain. 2017
IEEE International Conference on Systems, Man, and Cybernetics (SMC)
Banff Center, Banff, Canada, October 5-8, 2017[link](https://ieeexplore.ieee.org/document/8123011/){#Du2018}

R. Pass and E. Shi. Rethinking Large-Scale Consensus. In the Proceedings
of the IEEE 30th Computer Security Foundations Symposium, 2017. Thunder
Token Foundation: Thunder Consensus White Paper, Janurary, 2018[pdf](https://eprint.iacr.org/2018/302.pdf){#Pass2017}.

R. Pass, L. Seeman, and A. Shelat. Analysis of the Blockchain Protocol
in Asynchronous Networks. In EUROCRYPTO 2017[pdf](https://eprint.iacr.org/2016/454.pdf){#PassCrypto2017}.

Juan A. Garay, A. Kiayias, and N. Leonardos. The bitcoin backbone
protocol: Analysis and applications. In Elisabeth Oswald and Marc
Fischlin, editors, Advances in Cryptology - EUROCRYPT 2015, Volume 9057
of Lecture Notes in Computer Science, pages 281–310. Springer, 2015[pdf](https://eprint.iacr.org/2014/765.pdf){#Garay2015}.

Tendermint Team. Understanding the Basics of a Proof-of-Stake Security
Model.[link](https://blog.cosmos.network/understanding-the-basics-of-a-proof-of-stake-security-model-de3b3e160710){#Safety}.

V. Buterin. On Settlement Finality. [link](https://blog.ethereum.org/2016/05/09/on-settlement-finality/){#finality}.

EOS Team. EOS.IO Technical White Paper v2.
<https://github.com/EOSIO/Documentation/blob/master/TechnicalWhitePaper.md>.
Online available 25/05/2018. [link](https://github.com/EOSIO/Documentation/blob/master/TechnicalWhitePaper.md){#EOS}

Bitshares Team. Delegated Proof-of-Stake Consensus.
https://bitshares.org/technology/delegated-proof-of-stake-consensus/.
Online available 25/05/2018. [link](https://bitshares.org/technology/delegated-proof-of-stake-consensus){#bitshare}

R. Pass, and E. Shi. (2017). Hybrid consensus: Efficient consensus in
the permissionless model. In LIPIcs-Leibniz International Proceedings in
Informatics (Vol. 91). Schloss Dagstuhl-Leibniz-Zentrum fuer Informatik [pdf](http://drops.dagstuhl.de/opus/volltexte/2017/8004/pdf/LIPIcs-DISC-2017-39.pdf){#hybrid}.

V. Buterin, and V. Griffith. (2017). Casper the Friendly Finality
Gadget. arXiv preprint arXiv:1710.09437. [link](https://arxiv.org/abs/1710.09437){#Casper}

H. McCook. Under the Microscope: Economic and Environmental Costs of
Bitcoin Mining.
[link](https://www.coindesk.com/microscope-economic-environmental-costs-bitcoin-mining/){#capex}
