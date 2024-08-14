# zkSNARK Verifier Project

This project demonstrates a complete workflow for zkSNARK circuits, including circuit implementation, proof generation, contract deployment, and proof verification.

## Project Overview

To successfully complete the Final Challenge, your project should:

1. Write a correct `circuit.circom` implementation.
2. Compile the circuit to generate intermediaries.
3. Generate a proof using inputs `A=0` and `B=1`.
4. Deploy a Solidity verifier to the Sepolia testnet.
5. Call the `verifyProof()` method on the verifier contract and assert the output is `true`.

## Circuit Implementation

The circuit is implemented in `circuit.circom` with the following logic:

```plaintext
pragma circom 2.0.0;

template myCircuit() {
   signal input a;
   signal input b;
   signal x;
   signal y;
   signal output q;

   component andGate = AND();
   component notGate = NOT();
   component orGate = OR();

   andGate.a <== a;
   andGate.b <== b;
   notGate.in <== b;

   x <== andGate.out;
   y <== notGate.out;

   orGate.a <== x;
   orGate.b <== y;

   q <== orGate.out;
}

template AND() {
    signal input a;
    signal input b;
    signal output out;

    out <== a * b;
}

template NOT() {
    signal input in;
    signal output out;

    out <== 1 + in - 2 * in;
}

template OR() {
    signal input a;
    signal input b;
    signal output out;

    out <== a + b - a * b;
}

component main = myCircuit();

### Installation

1. Clone the repository and navigate to the project directory.
2. Install dependencies:

   ```bash
   npm install
2. Deployment
   ```bash
   npx hardhat circom
   npx hardhat run scripts/deploy.ts --network sepolia

## Features

1. **Performing Logical Operations:** The zkSNARK circuit performs AND, OR, and NOT operations to demonstrate basic logical gate functionality.
2. **Creating a zkSNARK Circuit:** Implementation of a zkSNARK circuit using `circom` to verify logical operations.

### License
This project is licensed under the MIT License. 

### Author
Divyansh Sandhu