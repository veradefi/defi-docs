# Build using Docker

## 🐋 Run the Docker container

Using this one command, you will have a ready-to-use environment.

```bash
docker run -it veradefi/substrate_env:latest
```

{% hint style="info" %}
This will start a terminal where you can get the contracts and build them using the command below
{% endhint %}

### 🏗️ Build

To compile the smart contract, run the following command

```bash
cargo +nightly contract build
```

### 

