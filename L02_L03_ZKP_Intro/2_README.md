## ZKP intro

### 1. Complexity Theory

Complexity theory is used to analyze resourse usage such as time and space so solve a computational problem.


#### Complexity Classes
- P(Polynomial Time)
- NP(Nondeterministic Polynomial Time)
- NP-complete
- NP-hard
- IP(Interactive Proofs)

Big O notation is used to describe the complexity (usually the upper bound complexity) in algebric terms for a solution to a computational problem.

| | Snarks | Starks  | Bulletproofs |
|---|---|---|---|
| Algorithmic Complexity: Prover | O(N*log(N))  | O(N* poly-log(N))  | O(N*log(N)) |
| Algorithmic Complexity: Verifier | ~O(1) | O(poly-log(N))  | O(N) |
| Communicational Complexity | ~O(1) | O(poly-log(N))  | O(log(N)) |
||||


### 2. ZKP Theory

#### 2.1 Argument Systems: $(P ,V)$
- Main components and parameters
  - Prover ($P$)
  - Verifier ($V$)
  - Circuit ($C$)
  - Public input ($x$) where $x∈F$
  - Secret witness ($w$) where $w∈F$
- The statement that the prover $P$ wants to prove to the verifier $V$ is represented as an arithmetic circuit $C$.
  - $C(x, w) = true/false$
- $P$ knows $x$ and $w$.
- $V$ knows only $x$.
- The goal is for $P$ to convince $V$ that it knows a $w$ such that $C(x,w)=true$, without revealing $w$.
- The prover/verifier communication can be interactive or non-interactive.


#### 2.2 Preprocessing Argument Systems: $(S, P, V)$
- Additional preprocessing (aka Setup) procedure $S(C)$ is involved here.
- The circuit $C$ is preprocessed to produce 2 public parameters $S_p$ and $S_v$
  - $S(C) \rightarrow (S_p, S_v)$
- $P$ takes $S_p$, $x$ and $w$: $P(S_p, x, w) \rightarrow proof \;  \pi$
- $V$ takes $S_v$ and $x$: $V(S_v, x, \pi)\rightarrow true/false$
- NOTE: $S_p$ and $S_v$ are also called proving key and verification key respectively.


#### 2.3 SNARK: A Succinct preprocessing argument system
- Succinct means the proof  $\pi$ should be short and fast to verify.
- i.e.
  - proof size: $O(log(|C|))$
  - verification time: $O(log(|C|))$


#### 2.4 Types of setup:
1. Trusted setup per circuit: $S(C,r)$
   - In addition to the circuit $C$, the setup also takes in some random bits $r$.
   - A new random $r$ should be generated for each circuit.
   - $r$ should be kept secret from the prover and discarded safely after use. If the prover somehow learns about $r$, it can produce fake proofs.  
   - NOTE: $r$ is also called **toxic waste**.
2. Trusted but universal setup: $S(C,r)$
   - $r$ is generated only once and discarded after the first run. Same as above, the prover should not learn about the $r$.
3. Transparent setup: $S(C)$
   - This type of setup does not use secret data.


#### 2.5 Commonly used SNARK implementations

| | Proof size | type |
|---|---|---|
|Groth 16| 200 bytes| trusted setup per circuit|
|Plonk|400 bytes| universal trusted setup|
||||


> [!NOTE]
> watch [ZK Whiteboard Sessions - Module One: What is a SNARK? by Dan Boneh](https://youtu.be/h-94UhJLeck?si=amIpASm8MjtNjpb0)


### 3. Zokrates
- Used to create proofs on Ethereum and verify proofs in Solidity.
- *see* [Docs](https://zokrates.github.io/)


### 4. Polynomials in ZKPs
- The circuit is represented as a polynomial.
- The algebric properties of polynomials can be used in proving and verification computations.


### 5. Homomorphic Encryption
- *see* [HE](https://github.com/0xkzam/cryptography?tab=readme-ov-file#7-homomorphic-encryption)


### 6. Homomorphic Hiding
- *see* [Homomorphic Hidings](https://electriccoin.co/blog/snark-explain/)



## ZKP Systems and Usecases

*see* [Comparison of the most popular ZKP systems](https://github.com/matter-labs/awesome-zero-knowledge-proofs#comparison-of-the-most-popular-zkp-systems)

#### Other techniques that can be used instead of SNARKS/STARKS
- Blind signatures
- Accumulators
- Pedersen commitments
- Sigma protocols

#### ZKP usecases
- Privacy coins: [Zcash](https://z.cash/learn/), Monero, TonadoCash, ZKDai
- [Filecoin zk-SNARK network](https://research.protocol.ai/sites/snarks/)
- ZK rollups
- Privacy Preserving Financial Systems: Aztec
- Games: [Dark Forest](https://zkga.me/)
- Authentication, DID, KYC, Tax, Legal Evidence, Digital Forensics, etc.