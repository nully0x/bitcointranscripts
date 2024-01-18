---
title: Atomic Multi Channel Updates
transcript_by: Bryan Bishop via tstbtc --needs-review
categories: ['conference']
tags: ['scalability']
speakers: ['Matteo Maffei']
---

Atomic Multi-Channel Updates with Constant Collateral in Bitcoin-Compatible Payment-Channel Networks

Matteo Maffei

<https://diyhpl.us/wiki/transcripts/scalingbitcoin/tel-aviv-2019/atomic-multi-channel-updates/>

<https://twitter.com/kanzure/status/1230929981011660800>

# Introduction

Matteo got sick and couldn't come. His coauthors couldn't come either. So a talk was pre-recorded and will be played now. Our work is about realizing atomic multi-channel updates with constant collateral in bitcoin.

# Scalability issues

We all know that blockchains have scalability issues. Public verifiability means we have to store each transaction on the blockchain. The transaction rate of bitcoin is far from being satisfactory. We can reach up to about 10 transactions/second in bitcoin. Contrasted to centralized systems like Visa, there's a difference of at least a few orders of magnitude. This is a severe issue that undermines the widespread deployment of blockchain technology.

Some work has been done to solve this problem. We can classify existing proposals into two categories. The on-chain approach aims to design better consensus protocols like sharding which allows parallel processing of transactions on different blockchains. On the other hand, we have off-chain approaches that use off-chain protocols like lightning network and raiden network. Do we really need to store each transaction on the blockchain to achieve public verifiability? Maybe users can exchange messages off-chain p2p and then resort to the blockchain only in the event of disputes. This is the basis for ideas like lightning network, raiden network, bolt, perun, liquidity network, etc. Payment channels and payment channel networks are the research field that I am going to concentrate on in this talk.

