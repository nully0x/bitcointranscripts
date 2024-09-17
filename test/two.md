---
title: Lightning Network BOLT by BOLT
transcript_by: Gloria Zhao via tstbtc --needs-review
categories: ['meetup']
tag: ['lightning']
speakers: ['Jim Posen']
date: 2018-07-24
media: https://podcasters.spotify.com/pod/show/chaincode/episodes/Amiti-Uttarwar-and-the-P2P-network---Episode-15-e18v7oq
---


Topic: Lightning Network BOLT by BOLT

Location: LA Blockchain Meetup

Transcript by: glozow

## Introduction

It's an ordered transaction ledger. The defining properties in my opinion are: it's globally replicated computers around the world are constantly synchronizing these transactions with one another. You have this notion of probabilistic finality which means that a single computer when it's downloading the ledger at some point in time can make an assessment and say I am almost 100% certain that this transaction will never be reverted from the global state. This idea of probabilistic finality is really important, and it's censorship-resistant which means that if you are trying to make a transaction and you're willing to pay the fees, it doesn't matter what the contents of the transaction are. It will make it into the ledger eventually. In this talk, we'll be talking about the Bitcoin blockchain, but these are kind of general properties of blockchains.


It's an ordered transaction ledger. The defining properties in my opinion are: it's globally replicated computers around the world are constantly synchronizing these transactions with one another. You have this notion of probabilistic finality which means that a single computer when it's downloading the ledger at some point in time can make an assessment and say I am almost 100% certain that this transaction will never be reverted from the global state. This idea of probabilistic finality is really important, and it's censorship-resistant which means that if you are trying to make a transaction and you're willing to pay the fees, it doesn't matter what the contents of the transaction are. It will make it into the ledger eventually. In this talk, we'll be talking about the Bitcoin blockchain, but these are kind of general properties of blockchains.
