---
title: Lightning Network BOLT by BOLT
transcript_by: Gloria Zhao via tstbtc --needs-review
categories: ['meetup']
tag: ['lightning']
speakers: ['Jim Posen']
date: 2018-07-24
media: https://www.youtube.com/watch?v=Ysj2yobFMF4
---


Topic: Lightning Network BOLT by BOLT

Location: LA Blockchain Meetup

Transcript by: glozow

## Introduction

This is gonna be a fairly technical talk. We're going to break down the protocol specification that specifies how Lightning Network nodes communicate with each other. It's an 11 part spec. There's 11 BOLTs and so we're gonna go, piece by piece, BOLT by BOLT. Some of them will be more in depth than others. I know people are probably at different levels of understanding with this stuff so can I just kind of poll...

Very high level: what is a blockchain? It's an ordered transaction ledger. The defining properties in my opinion are: it's globally replicated computers around the world are constantly synchronizing these transactions with one another. You have this notion of probabilistic finality which means that a single computer when it's downloading the ledger at some point in time can make an assessment and say I am almost 100% certain that this transaction will never be reverted from the global state. This idea of probabilistic finality is really important, and it's censorship resistant which means that if you are trying to make a transaction and you're willing to pay the fees, it doesn't matter what the contents of the transaction are. It will make it into the ledger eventually. In this talk, we'll be talking about the Bitcoin blockchain, but these are kind of general properties of blockchains.
