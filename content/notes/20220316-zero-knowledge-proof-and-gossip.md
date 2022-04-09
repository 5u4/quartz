---
title: Zero knowledge proof & gossip
date: 2022-03-16
tags:
  - cryptography
---

Zero knowledge (zk) is a way to prove someone knows a certain secret but without revealing any information to the validator and the outside world.

Zero knowledge proof has three characteristics:

- **Completeness**: if the prover knows some secret, verifier can verify they indeed know the secret by doing some steps.
- **Soundness**: if the prover does not know the secret, no matter how they fake the steps, the verifier would reject.
- **Zero-knowledge**: While proving, the prover will leak no information about the secret.

## Some random thinking about zk and gossip

While I was browsing Weibo, I found people like to share some hearsay to satisfy their vanity
but are afraid of leaking the critical information.

Just some random thinking; a zk proof is excellent for this use case if it can be somehow proved. 🤔
