---
permalink: /features/miner-rewards/
title: Mining Rewards
subtitle: Earn STEEM by joining the peer-to-peer network and validating transactions.
image: ../images/frontpage/ico-paid-mine.svg
priority: 5
summary: >
   Anyone with a good internet connection and some server skills can make money by
   helping the network produce blocks and secure them with proof of work. Steem uses
   a mining algorithm and process that should eliminate mining pools and reward
   hosting a full node with a low-latency connection to the rest of the network.

---

## Miners earn 1% of Market Capitalization per Year

The Steem network pays miners 1% of its market cap every year.

Steem evenly divides 90% of the mining rewards among the top 19 "mining pools" voted on via proof of work and ensures that each pool is only given one block
production slot per round.  A round consits of 21 blocks produced exactly every 3 seconds. If no miners miss their slot, then all 21 blocks will be
produced by a unique miner.

Mining rewards are paid out as *vesting* STEEM and can only be converted to liquid steem over two years via 104 equal weekly payments.

## Proof of Work

Steem gives us the benefits of Proof of Work (aka mining) without the downsides such as unpredictable block production time,
mining pool centralization, or the potential for recent blocks to be orphaned. The primary benefits of POW include:

- An objective measure of quality that is expensive to forge
- A financial incentive to optimize a useful/necessary computer algorithm
- A distribution model that attracts tech-savvy users
- Creation of a robust low-latency network

Unlike traditional mining, block production time is separated from the time when work is performed. When a solution is found that meets the target difficulty, a transaction is submitted the network and included by the current block producer. To be included, the POW must be derived from the current head block. The user is then added to a queue to be included in a future block production round. The target difficulty (d) becomes a function of the queue length (q).

<center><b><h4> d = 2<sup> q / 4 + 4</sup> </h4></b></center>

With three-second block times, a POW miner needs to operate a node with minimal network latency so it can get the new head-block as quickly as possible and then
submit its result to the network with enough time to propagate to the next block producer.  The introduction of a mining pool would add additional latency that
would dramatically reduce the percentage of time available to actually do work.

On average one new POW transaction is submitted to the network every 63 seconds. Block producers are paid extra to include POW transactions.

### Mining Algorithm

While any mining algorithm could be used, we would like to introduce a new algorithm that has several beneficial properties. The mining algorithm requires proof that the miner possess the private key for the account that will ultimately produce the block and receive the reward. The algorithm also requires the user to do an elliptic curve signature verification, the optimization of which will benefit the validation of all transactions and lower the cost of operating the network in the long run.

    Let H    = Head Block ID
    Let H2   = SHA256(H+NONCE)
    Let PRI  = Producer Private Key
    Let PUB  = Producer Public Key
    Let S    = SIGN(PRI, SHA256( H ) )
    Let K    = RECOVER_PUBLIC_KEY( H2, S )
    Let POW  = SHA256( K )

To be valid the POW must be less than the target difficulty and RECOVER_PUBLIC_KEY(H2,S) must equal PUB. The miner introduces randomness in either the selection of the NONCE or via the randomness required for elliptic curve signature generation. This, combined with the private key selection should ensure that no two miners are searching the same work space.

By starting and ending the POW with a cryptographically secure hash function we can ensure that any vulnerabilities or computational shortcuts that may exist in the RECOVER_PUBLIC_KEY algorithm or SIGN algorithm will ultimately cause the POW algorithm to revert back to a simple HASH-based POW.

### Proof of Commitment is Proof of Work

If we are going to talk about the benefits of proof-of-work, then it helps to have a useful definition of work. In terms of physics, work is defined as *power* X *time*.

    W = Pt

 In more general terms, we would define work as something you must pay people to do. If it doesn’t cost anything then no work was done. Bitcoin satisfies both definitions of proof-of-work. No one would spend money building specialized hardware and consuming electricity if they weren’t paid to do so. Therefore, Bitcoin’s block difficulty represents mathematical proof that about 25 BTC worth of work was performed. The corollary here is that if you pay a fixed amount of money into a competitive market then market competition will drive the work required to earn that money toward the value of the money.

 We can view Bitcoin Work as Difficulty or HashPower * 10 minutes.

     W = D = HP * 10m

I would like you to consider that committing to hold a token for a period of time in the future is work.
No one gives up liquidity or locks funds up without expecting interest. The value of the interest paid is
therefore proportional to the work required to earn it. In the same way, the value of the Bitcoin mining rewards
is proportional to the work required to earn it.

The vast majority of Steem is held by those who commit to hold it for an average of one year. These committed stakeholders
vote to nominate someone to produce blocks on their behalf.  This is very similar to buying mining equipment and giving up liquidity
of your BTC until the miner can earn it back with interest.  People with Bitcoin miners vote on which mining pool they wish to join,
likewise, vesting stakeholders vote on which pool(s) should produce blocks on their behalf.

Users who commit their STEEM are rewarded in several ways:

  1. Network Bandwidth
  2. Additional STEEM
  3. Curation Influence
  4. Block Produciton Influence

People will convert STEEM into *vesting* STEEM (aka VESTS) until the value of the benfits equals the cost of lost liquidity.

## Not Proof of Stake

Proof of Stake is a consensus algorithm where block producers are selected by current stakeholders. Existing Proof of Stake blockchains
rely on either past-ownership or present ownership of tokens. This is all considered [sunk cost](https://en.wikipedia.org/wiki/Sunk_costs) which
has 0 value and therefore cannot be considered work.  

Vesting STEEM for an average of 1 year represents future work and has an [opportunity cost](https://en.wikipedia.org/wiki/Opportunity_cost) which
is just as real as the cost of electricity. This makes Vesting STEEM a variety of Proof of Work.

## Known Weaknesses (first 30 days)

For the first month of Steem's life, 100% of all blocks are produced by miners who have done a computational Proof of Work. This algorithm is
vulnerable to an attack whereby existing block producers may choose to exclude valid POW transactions from competing miners. If an attacker
controls 20% of the computational power, then he has the ability to handicap his competitors by 20% increasing his effective computational power
to 25% of the total.  An attacker with 34% of the real hash power is able to handicap his competitors to such an extent that the attacker gains over
50% of the effective hash power. Once an attacker reaches 50% of effective hash power they can start ignoring blocks produced by other miners and
gain 100% control.

This is why Steem switches to elected block producers for over 90% of all block production after 30 days. Elected producers are vetted and can easily be replaced
if they are shown to misbehave by failing to include valid POW transactions. Electing producers has been proven reliable via years of experience with
[BitShares](https://bitshares.org) and Bitcoin mining pools.
