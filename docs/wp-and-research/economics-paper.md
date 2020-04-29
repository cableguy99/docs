# TAO - Designed for the Music Economy

## Preface

### Tao's vision and mission

Our mission is to be a leading force in building the Internet of Value, and its infrastructure and applying it specifically towards addressing the pain points of the music economy. 
We are working to create an alternative, scalable financial system which is more secure, transparent, efficient, inclusive and equitable for everyone.

Tao is an innovative solution to the scalability problem with the Tao 1.0 blockchain. 
Tao relies on a system of 150 Masternodes with Delegated Proof of Stake (DPOS) consensus that can support near-zero fee, and 5-second transaction confirmation time. 
Security, stability and chain finality are guaranteed via novel techniques such as double validation, staking via smart-contracts and "true" randomization processes. 


Tao supports all EVM-compatible smart-contracts, protocols, and atomic cross-chain token transfers. 
New scaling techniques such as sharding, EVM parallelisation, private-chain generation and  hardware integration will be continuously researched and incorporated into Tao's Masternode architecture which will be an ideal scalable smart-contract public blockchain for decentralized apps, token issuances and token integrations for stakeholders in the music economy of any size.

### Scope

This document describes Tao's initial draft for the Tao blockchain’s economics system.

## Masternodes

- **Masternodes** are full-nodes that create, verify and validate new blocks in Tao's platform. 

- **Masternode Candidate**: Any account can deposit 100K TAO using the official on-chain governance d-app to become a Masternode Candidate. 
100K TAO deposit can earn staking rewards. 
A Candidate can resign, but the tokens will be locked for the next 30 days (1,296,000 blocks) after the resignation. 

- **Becoming a Masternode**: A Candidate becomes a Masternode when the user belongs to the top 150 most voted Candidates in each epoch. 
A Masternode can resign, but the tokens  will be locked for the next 30 days after the resignation.

- **Reward**: The reward a Masternode receives in each epoch is proportional to the number of signatures he/she  signs.

## Token Voting and Staking

-   **Token  voting**: Token holders can vote for Masternode Candidates by sending TAO to each Candidates specific voting address using the official governance d-app. The top 150 most voted Candidates will become Masternodes. 
Token holders can un-vote a Candidate, but the tokens will be locked for the next 48 hours (86,400  blocks) after the un-voting.   

-   **Staking**: Masternode token  deposits, and all  tokens used to vote for Masternodes will enter the staking program and earn block rewards in each epoch, plus any fees. 
Tokens used to vote for Candidates who do not become Masternodes will not earn staking rewards.

## Token Emission Schedule

-   **Following the fundraising commitment**: The total amount of tokens at the genesis block is 55 million TAO tokens in circulation; 
12 million are reserved for the team vested over the next 4 years; 
16 million are reserved for strategic partners and an ecosystem building fund which totals 83 million tokens. 
Plus, 17 million are reserved as block rewards for the next 8 years, the amount of tokens in circulation at the end of the 8th year after the genesis block is around 100 million TAO. 
After the mainnet launch: the block reward for the first and second year is 6 million TAO annually; the block reward for the 3rd, 4th and 5th year is 2 million TAO annually; and the block reward for the 6th, 7th and 8th year is 1 million TAO annually. 
Subsequently, the block reward will be halted, or activated at a number less than or equal to 1 million TAO annually.


-   **Implementation**: Each epoch consists of 360 blocks, which will reward a total of 360 TAO in the first two years. 
360 TAO will be divided to all the Masternodes proportional to the number of signatures they sign during the epoch. 
Afterward, the reward achieved by each Masternode  will be divided into three portions. 
The first portion of 40% called “Infrastructure Reward” goes to the Masternode. 
The second portion of 50% called “Staking Reward” goes to the pool of all voters for that Masternode which is shared proportionally based on the token stake. 
The last portion of 10% called “Foundation Reward” goes to a special account controlled by the Masternode Foundation, which is run by the Tao community initially. 

## Voting/Staking Consideration

### Candidate/Masternode incentives

Masternodes will receive a significant amount of block rewards, which likely exceeds the cost of running the infrastructure. 
However, Masternodes need to invest in Tao by depositing at least 100K Tao, and stake them for the long term. 
Furthermore, after depositing 100K TAO to become a Candidate, if the account cannot become a Masternode (has less votes than the top 150 most voted Candidates), he/she will receive no rewards. 
Therefore, Candidates have an incentive to do as much as they can such as signaling their capability to support Tao to get into top 150 most voted Candidates.

### Token voter incentives

Token voters should vote for Candidates who signal strong support for Tao because if the Candidate does not become a Masternode, voters will not receive any rewards. 
However, token voters should also vote for the less voted Candidates because the most voted Candidates will receive less rewards per token stake comparatively. 

## Long Term Platform Economics Consideration

### P/E theory of token value

Equity price can often be a multiple of annual earnings a company generates. In the case of a blockchain platform, earnings could be considered as the total rewards and fees that the platform produces. 
The multiples for technology startups in the early days could exceed 200 which is where the Ethereum network is approximately at the moment.  

### Quantity theory of money for token value

In this theory, the total amount of TAO can be considered the money supply for the blockchain economy including all the d-apps and tokens running on Tao. 
Assuming a constant price and velocity of money, demand will rise proportionally to the total amount of activity of the whole blockchain network, which will raise the price of TAO if the supply is fixed or the inflation rate is very small. 
Tao's advantages of minimal transaction fees and very fast confirmation time could spur a massive amount of activity for TAO itself and all tokens running on Tao.    

### Store of value theory of token value

Blockchain native tokens can be considered as the means of fundraising, or the store of value within their own blockchain economy if the supply of the token is fixed, or the inflation rate is very small and predictable. 
These conditions apply to Ether and Bitcoin at the moment, and can be applied to TAO in the future as Tao's economy grows. 

### Built-in decentralized exchange
Tao's roadmap includes a built-in decentralized exchange, in which a portion of fees will be added to the pool of epoch rewards. These fees could be substantial if there are many valuable tokens running on Tao. 
This extra feature can increase the future earnings of the network, and raise TAO's price based on the P/E theory.

## Decentralized Governance

### Become a Masternode

Becoming a Masternode is an important signal of long-term support for the Tao platform. 
We would welcome other entities to become Masternodes, to show their support by helping the network, and gradually decentralize the platform governance.  

### Board of Governors

It is postulated that the Tao platform would later be operated by a non-profit body such as a Board of Governors (or Foundation) amongst many other decentralized bodies which receive a steady amount of income from the network, and act solely in the interest of the network.

### Technical decision making

The technical decisions should be considered, debated, and decided upon by qualified experts based on the long-term interest of the network.

### Economic decision making

The economic decisions such as the amount of block rewards, inflation rate and the division of block rewards might be based on the consensus of the majority of the Masternodes (with their voters). 
The Board of Governors could be one of the coordinating bodies for these activities using the official governance d-app.

<!--## Appendix A: History of the Project
aos' advantages of minimal transaction fees and very fast confirmation times could spur a 
Tao PTE. LTD. raised funds to build Tao blockchain platform in early 2018. 
The ICO whitepaper is at https://goo.gl/avtnZ1. 
The terms of sale and other documents can be found at  https://tao.network/exchanges the Tao platform will be gradually decentralized in 2-8 years after the mainnet launch, and eventually become a secure public blockchain platform for everyone.-->

## Appendix B: Reward Calculation Formula and Details

### General notations

-   N: the current number of masternodes, maximum of N = 1..150
-   $M_1$, $M_2$, .., $M_N$: the set of masternodes in the current epoch
-   $C_1$, $C_2$, .., $C_N$: the number of signatures a masternode has made
-   $S_1$, $S_2$, .., $S_N$: the total amount of staked (including deposited and voted) TAO for a masternode
-   $D_1$, $D_2$, .., $D_N$: the amount of deposited TAO by a masternode
-   X: the total reward per epoch for all masternodes
-   Total reward per masternode = Infrastructure reward + staking reward
-   MN: stand for masternode

Reward divided to Masternode $M_i$: 			$R_i = \frac{C_i*X}{\sum_{i=1}^{N}C_i}$

Reward per epoch:   

-   Masternode infrastructure reward: 		1$R_i$

-   Voter with 1k voted TAO: 				$\frac{0.5R_i*1000}{S_i}$

-   Masternode staking reward: 			$\frac{0.5R_i*D_i}{S_i}$

Reward per week (48 * 7 = 336 epochs):
	
-   Masternode infrastructure reward: 		336 * 1$R_i$

-   Voter with 1k voted TAO: 				336 * $\frac{0.5R_i*1000}{S_i}$

-   Masternode staking reward: 			336 * $\frac{0.5R_i*D_i}{S_i}$

Reward per year (48 * 365 = 17520 epochs):

-   Masternode infrastructure: 				17520 * 1$R_i$

-   Voter with 1k voted TAO:				17520 * $\frac{0.5R_i*1000}{S_i}$

-   Masternode staking reward: 			17520 * $\frac{0.5R_i*D_i}{S_i}$

-   Total reward for a masternode:		17520 * 1$R_i$ + 17520 * $\frac{0.5R_i*D_i}{S_i}$

### Applying the reward calculation formula to specific scenarios 

Note that, for simplification of illustration: 

-   The total amount of staked TAO for all masternodes is equal 

-   The signatures for all masternodes in the scenarios are equal 

With these assumptions, all masternodes receive the same divided reward (R) and the same infrastructure reward. 
Furthermore, the reward for Voters with 1k voted TAO is equal regardless of which the amount is voted for.

### Scenario 1: 50 Masternodes, 2.5 million token voting, a total of 7.5 million token locked.

N = 50, X = 360, $S_1 = S_2 = .. = S_{50} = 7,500,000 / 50 = 150k$ TAO

$C_1 = C_2 = .. = C_{50}$

Therefore, $R_1 = R_2 = .. = R_{50} = R = X/50 = 7.2$ TAO

#### Reward per epoch:

-   MN infrastructure reward = 1 * 7.2 = 7.2 TAO

-   For Voter with 1k voted = (0.5 * 7.2 * 1000) / 150k = 0.024 TAO

-   MN staking reward with 100k TAO deposited: 100 * 0.024 = 2.4 TAO

#### Reward per week: 
   
-   MN infrastructure reward = 336 * 7.2 = 2,419.2 TAO
   
-   For Voter with 1k voted = 336 * 0.024 = 8.064 TAO
   
-   MN staking reward with D = 100k TAO deposited: 336 * 2.4 = 806.4 TAO

#### Reward per year: 
   
-   MN infrastructure reward = 17,520 * 7.2 = 126,144 TAO

-   For Voter with 1k voted = 17,520 * 0.024 = 420.48 TAO

-   MN staking reward with 100k deposited: 17,520 * 2.4 = 42,048 TAO

-   Total reward per MN with D = 100k deposited: 126,144 + 42,048 = 168,192 TAO

### Scenario 2: 100 Masternodes, 3 million tokens voting, a total of 13 millions token locked.

N = 100, X = 360, $S_1 = S_2 = .. = S_{100} = 13,000 000 / 100 = 130k$ TAO

$C_1 = C_2 = .. = C_{100}$

Therefore, $R_1 = R_2 = .. = R_{100} = R = X/100 = 3.6 TAO

#### Reward per epoch:
    
-   MN infrastructure reward = 1 * 3.6 = 3.6 TAO

-   For Voter with 1k voted = (0.5 * 3.6 * 1000) / 130k = 0.01384

-   MN staking reward with D = 100k deposited: 100 * 0.01384 = 1.384 TAO

#### Reward per week: 
   
-   MN infrastructure reward = 336 * 3.6 = 1,209.6 TAO
   
-   For Voter with 1k voted = 336 * 0.01384 = 4.65024 TAO
   
-   MN staking reward with D = 100k deposited: 336 * 1.384 = 465.024 TAO

#### Reward per year: 

-   MN infrastructure reward = 17,520 * 3.6 = 63,072 TAO

-   For Voter with 1k voted = 17,520 * 0.01384 = 242.4768 TAO

-   MN staking reward with D = 100k deposited: 17,520 * 1.384 = 24,247.68 TAO

-   Total reward per MN with D = 100k deposited: 63,072 + 24,247.68 = 87,319.68 TAO

### Scenario 3: 150 Masternodes, 12.5 million tokens voting, a total of 27.5 million tokens locked.

N = 150, X = 360, $S_1 = S_2 = .. = S_{150} = 27,500,000 / 150 = 183k$ TAO

$C_1 = C_2 = .. = C_{150}$

Therefore, $R_1 = R_2 = .. = R_{150} = R = X/150 = 2.4$ TAO

#### Reward per epoch:

-   MN infrastructure reward = 1 * 2.4 = 2.4 TAO

-   For Voter with 1k voted = (0.5 * 2.4 * 1000) / 183,000 = 0.00655 TAO
    
-   MN staking reward with 100k deposited: 100 * 0.00655 = 0.655 TAO

#### Reward per week: 

-   MN infrastructure reward = 336 * 2.4 = 806.4 TAO

-   For Voter with 1k voted = 336 * 0.00655 = 2.2 TAO
   
-   MN staking reward with D = 100k deposited: 336 * 0.655 = 220.08 TAO

#### Reward per year: 
   
-   MN infrastructure reward = 17,520 * 2.4 = 42,048 TAO
   
-   For Voter with 1k voted = 17,520 * 0.00655 = 114.756 TAO
   
-   MN staking reward with D = 100k deposited: 17,520 * 0.655 = 11,475.6 TAO
   
-   Total reward per MN with D = 100k deposited: 42,048 + 11,475.6 = 53,523.6 TAO






