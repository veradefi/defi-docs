# Building Smart Contracts

## Install cargo-contract

To build the Substrate smart contract project we will need CLI utility

```bash
$ rustup component add rust-src --toolchain nightly
```

```bash
$ cargo install cargo-contract --vers ^0.11 --force --locked
```

## ๐งช Test

To test your smart contract, run the following command

```bash
$ cargo test
```

## ๐๏ธ Build

To compile your smart contract, run the following command

```bash
$ cargo +nightly contract build
```

