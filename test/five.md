---
title: ROAST - Robust asynchronous Schnorr threshold signatures
transcript_by: Bryan Bishop via tstbtc --needs-revi
categories: ['core-dev-tech']
speakers: ['Tim Ruffing']
tags: ['schnorr', 'FROST']
date: 2022-10-14
---

paper: <https://ia.cr/2022/550>

slides: <https://slides.com/real-or-random/roast-tabconf22/>

Hey. Hello. My name is Tim and I work at Blockstream. This is some academic work in joint with some of my coworkers.

# Schnorr signatures in Bitcoin

We recently got support for Schnorr signatures in bitcoin, introduced as part of bip340 which was activated as part of the taproot soft-fork. There are three main reasons why we want Schnorr signatures and prefer them over ECDSA bitcoin signatures which can still be used: one is that Schnorr signatures have provable security and give the theory guys more confidence; Schnorr signatures are more efficient; and the main thing is that we can get easier constructions of advanced signing protocol

