# Circom

A Circom program is a form of an arithmetic circuit which consists of 
- A witness generation program (output computation)
- A constraint system (the set of polynomials)

Refer [here](https://docs.circom.io/circom-language/signals/) for Circom Language syntax.


## Basic steps of writing and proving circuits

#### 1. Write the circuit and save as a .circom file (e.g. hello.circom)

1. All constraints must be of the form A*B + C = 0, where A, B and C are linear combinations of signals.
2. The arithmetic circuits operate on signals.
3. `template` defines the shape of the circuit.



#### 2. Compile the circom file

```shell
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

```shell
cd hello_js

node generate_witness.js hello.wasm ../input.json witness.wtns

cd ..
```

#### 5. Trusted setup: phase 1

This phase is independent of the circuits we've written.

Start the ceremony and make the first contribution.
```bash
snarkjs powersoftau new bn128 12 pot12_0000.ptau -v
snarkjs powersoftau contribute pot12_0000.ptau pot12_0001.ptau --name="First contribution" -v
```


#### 5. Trusted setup: phase 2

This phase depends on the circuits we've written.


Start phase 2, generate a .zkey file that contains both proving and verification keys together and make the contribution.
```bash
snarkjs powersoftau prepare phase2 pot12_0001.ptau pot12_final.ptau -v
snarkjs groth16 setup hello.r1cs pot12_final.ptau hello_0000.zkey
snarkjs zkey contribute hello_0000.zkey hello_0001.zkey --name="Kz" -v
```

Export the verification key
```bash
snarkjs zkey export verificationkey hello_0001.zkey verification_key.json
```

#### 6. Proof Generation and Verification

Generating a Proof
```bash
snarkjs groth16 prove hello_0001.zkey hello_js/witness.wtns proof.json public.json

//Output
[INFO]  snarkJS: EXPORT VERIFICATION KEY STARTED
[INFO]  snarkJS: > Detected protocol: groth16
[INFO]  snarkJS: EXPORT VERIFICATION KEY FINISHED
```

Verifying the proof
```bash
snarkjs groth16 verify verification_key.json public.json proof.json

//Output
[INFO]  snarkJS: OK!
```