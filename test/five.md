---
title: Misconceptions about segwit vbytes
transcript_by: Bryan Bishop via tstbtc --needs-review
categories: ['core-dev-tech']
tags: ['segwit', 'fees']
speakers: ['Mark Erhardt']
date: 2022-10-15
---

# Weighing transactions: The witness discount

You've already heard from someone that this presentation will be more interactive. I probably won't get through all of my material. If you have questions during the talk, please feel free to raise your hand and we can cover it right away. I'm going to try to walk you through a transaction serialization for both a non-segwit transaction and a segwit transaction. By the end of the talk, I hope you understand how the transaction weight is calculated and how the witness discount works. At the end, we might look at a few different output types at the end.
