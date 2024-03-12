## Circom

#### 1. Write the circuit and save as a .circom file (e.g. hello.circom)

1. All constraints must be of the form A*B + C = 0, where A, B and C are linear combinations of signals.
2. The arithmetic circuits operate on signals.
3. `template` defines the shape of the circuit.



#### 2. Compile the circom file

```zsh
circom hello.circom --r1cs --wasm --sym --c
```

- `--r1cs`: Generates the file `hello.r1cs` that contains the R1CS constraint system of the circuit in binary format.
- `--wasm`: Generates the directory `hello_js` that contains the Wasm code (`hello.wasm`) and other files needed to generate the witness.
- `--sym` : Generates the file `hello.sym `, a symbols file required for debugging or for printing the constraint system in an annotated mode.
- `--c` : Generates the directory `hello_cpp` that contains several files needed to compile the C code to generate the witness.



#### 3. Create input.json file.

input.json contains the inputs for the circuit in standard json format.<br>
Note: I'm creating the input.json file in the src directory where hello.circom file is.
```js
{"in1": "2", "in2": "3"} 
```

#### 4. Compute the witness with WebAssembly

Navigate to the hello_js dir and run the following to compute the `witness.wtns` binary file.

```zsh
node generate_witness.js hello.wasm ../input.json witness.wtns
```

#### 5. Trusted setup: phase 1

This phase is independent of the circuits we've written.

Start the ceremony
```bash
snarkjs powersoftau new bn128 12 pot12_0000.ptau -v
```

Make the first contribution
```bash
snarkjs powersoftau contribute pot12_0000.ptau pot12_0001.ptau --name="First contribution" -v
```


#### 5. Trusted setup: phase 2

This phase depends on the circuits we've written.


Start phase 2
```bash
snarkjs powersoftau prepare phase2 pot12_0001.ptau pot12_final.ptau -v
```

Generate a .zkey file that contains both proving and verification keys together
```bash
snarkjs groth16 setup hello.r1cs pot12_final.ptau hello_0000.zkey
```

Contribute to the phase 2
```bash
snarkjs zkey contribute hello_0000.zkey hello_0001.zkey --name="Kz" -v
```

Export the verification key
```bash
snarkjs zkey export verificationkey hello_0001.zkey verification_key.json
```

#### Generating a Proof

```bash
snarkjs groth16 prove hello_0001.zkey hello_js/witness.wtns proof.json public.json
```