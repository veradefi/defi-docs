# Prerequisites

### Prepare a computer for Substrate development

{% embed url="https://substrate.dev/docs/en/knowledgebase/getting-started/" %}

{% hint style="info" %}
You can follow the detailed guide from [Substrate Developer Hub.](https://substrate.dev/docs/en/knowledgebase/getting-started/)
{% endhint %}

## 1. Install build tools & libraries

#### macOS

```bash
# Install Homebrew if necessary https://brew.sh/
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

# Make sure Homebrew is up-to-date, install openssl
brew update
brew install openssl
```

#### Ubuntu/Debian

```bash
sudo apt update
# May prompt for location information
sudo apt install -y git clang curl libssl-dev
```

#### Arch Linux

Run these commands from a terminal:

```text
pacman -Syu --needed --noconfirm curl git clang
```

#### Fedora

Run these commands from a terminal:

```text
sudo dnf update
sudo dnf install clang curl git openssl-devel
```

## 2. Setup Rust Developer Environment

Run this command from a terminal:

```bash
curl https://getsubstrate.io -sSf | bash -s -- --fast
```

