---
title: Succinct Atomic Swap
transcript_by: Michael Folkson via tstbtc --needs-review
date: 2020-05-11
speakers: ['Ruben Somsen']
media: https://www.youtube.com/watch?v=TlCxpdNScCA
---

Topic: Succinct Atomic Swap (SAS)

Location: Ruben Somsen YouTube channel

SAS resources: https://gist.github.com/RubenSomsen/8853a66a64825716f51b409be528355f

# Intro

Happy halvening. Today I have a special technical presentation for you. Basically what we are going to do is cut atomic swaps in half. I call this succinct atomic swaps.

# Motivation

First let me tell you my motivation. I think Bitcoin is a very important technology. We need to find ways to utilize it at its maximum potential without sacrificing decentralization. In order to do that you need to come up with some smart ways to do more with less. That is the protocol design that I try to come up with. In line with that I came up with this.

# Going from four transactions….

What we are going to do is take atomic swaps which are a protocol where you have a UTXO on two chains and you want to swap them. Or maybe on the same chain. You could think Bitcoin to Litecoin or even two Bitcoin UTXOs where you want privacy and that is why you swap them. The protocol that works today is four transactions. You have a preparation transaction on the first chain. Then you have another preparation transaction on the other chain. It is generally a multisig in both cases. You have some kind of timelock. They do a swap. We are taking that and we are bringing it down to only two transactions. You might think how is that possible? You are going to find ou
