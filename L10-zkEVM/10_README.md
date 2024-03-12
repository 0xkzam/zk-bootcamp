## zkEVM

#### Intro Resources
1. [ZK Whiteboard Sessions – Module Ten: zkEVM with Jordi Baylina](https://www.youtube.com/watch?v=mrf9HjjL_38&list=PLj80z0cJm8QErn3akRcqvxUsyXWC81OGq&index=12)
2. [zkEVM](https://scroll.io/blog/zkevm), Scroll
3. [The different types of ZK-EVMs](https://vitalik.eth.limo/general/2022/08/04/zkevm.html), Vitalik Buterin

#### Timeline
- 2013 - TinyRAM
- 2018 - Spice
- 2020 - zkSync
- 2021 - Cairo VM
- 2022 - Polygon zkEVM / Scroll / Risc Zero
- 2023 - Powdr

#### Main Components of a  <u>zkVM</u> 
- Compiler: to compile high-level languages such as C++ and Rust into intermediate (IR) expressions for the ZK system to perform.
- ISA (Instruction Architecture) instruction set framework: to execute instructions about CPU operations and is a series of instructions used to instruct the CPU to perform operations

#### General workflow of a zkEVM
1. Receive a transaction
2. Execute the relevant bytecode
3. Make state changes and transaction receipts
4. Using the zkEVM circuits with the execution trace as input produce a proof of correct execution
5. Aggregate proofs for a bundle of transactions and submit them to L1
6. Submit data to the appropriate data availability layer.

 #### zkEVM types

 - Type 1 (fully Ethereum-equivalent)
 - Type 2 (fully EVM-equivalent)
 - Type 2.5 (EVM-equivalent, except for gas costs)
 - Type 3 (almost EVM-equivalent)
 - Type 4 (high-level-language equivalent)

#### zkEVM solutions
- zkSync 
- [Scroll](https://scroll.mirror.xyz/nDAbJbSIJdQIWqp9kn8J0MVS4s6pYBwHmK7keidQs-k)
- Polygon [Zero, Hermez, Maiden & Nightfall](https://www.alchemy.com/overviews/polygon-zk-rollups)
- Taiko
- [Kakarot](https://www.kakarot.org/#Understanding)
- [Linea](https://docs.linea.build/architecture)
