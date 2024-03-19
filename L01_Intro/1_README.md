# Math & Cryptography introduction

## Math Intro

- Modular Arithmetic *(see [this](https://github.com/0xkzam/cryptography?tab=readme-ov-file#contents))*
- Group Theory
- Finite Fields and Generators
- Group Homomorphisms
- Roots of Unity
- Polynomials

## Cryptography Background
- Hash Functions
- Verifiable Random Functions
- Encryption *(see [this](https://github.com/0xkzam/cryptography?tab=readme-ov-file#contents))*
- Elliptic Curves

## Proving Systems

Actors in a Proving System
- Creator - optional, maybe combined with the prover
- Prover 
- Verifier 

A proof should have,
- Completeness: An honest prover should be able to convince an honest verifier of the correctness of the proof with very high probability. 
- Soundness: No dishonest prover should be able to convince an honest verifier of its incorrect proofs regardless of computational limits.

#### Interactive vs. Non-Interactive Proofs
- Interactive proofs: Multiple rounds of communication between the prover and the verifier is needed to establish the proof's validity.
- Non-Interactive proofs: Only one round of communication. No further interactions needed after the prover generates and publishes a proof. 

#### Succinctness
- Efficiency of the proof in terms of space (storage size) and verification time.

#### Proof of knowledge vs Proof
- A proof is merely a demonstration of the truthfulness of a statement.
- Proof of knowledge implies that it possesses certain information beyond merely a proof. 

#### Argument vs Proof
- According to the soundness property, a proof should be independent of its prover's computational power, hence it provides a stronger form of soundness. 
- An argument provides **computational** soundness as it depends on the prover's computational power i.e., the correctness of the argument relies on computational assumptions.