# Building Smart Contracts

### Install cargo-contract

To build the Substrate smart contract project we will need CLI utility

```bash
rustup component add rust-src --toolchain nightly
```

```bash
cargo install cargo-contract --vers ^0.8 --force --locked
```

### 🧪 Test

To test the smart contract, run the following command

```bash
cargo +nightly test
```

### 🏗️ Build

To compile the smart contract, run the following command

```bash
cargo +nightly contract build
```

### 

