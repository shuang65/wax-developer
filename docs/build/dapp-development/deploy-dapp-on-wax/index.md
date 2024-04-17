---
标题: 在WAX上部署您的dApp
顺序: 70
---

# 在WAX上部署您的dApp

要在WAX上部署您的dApp，您需要使用 [WAX-CDT](/build/dapp-development/wax-cdt/)and [区块链工具](/build/tools/blockchain_tools)，进行以下操作:

- 编译您的智能合约
- 为每个合约创建一个WAX账户
- 部署您的智能合约到WAX链

WAX提供两种部署方式。您可以使用我们的自定义 **make** 脚本 (适合 EOS 开发者) ，也可以在本地Docker容器或安装中使用WAX-CDT工具。下面是各种方式的优势和要求。

## 自定义部署脚本

The <a href="https://github.com/worldwide-asset-exchange/wax-blockchain" target="_blank">WAX Source Code Repository</a> includes a **hello-world** sample contract, along with **make** scripts that provide an easy, automated way to build and deploy your smart contracts. These scripts use the <a href="https://hub.docker.com/r/waxteam/dev" target="_blank">WAX Docker Development image</a> to:

- Create a WASM and ABI file
- Create a WAX Blockchain Account for your smart contract
- Deploy your smart contract to WAX
- Test your smart contract on the WAX Blockchain

### Advantages

- Allows you to deploy a smart contract from a Docker container, without installing any WAX source code (you'll still need to download the **hello-world** source code and scripts from the <a href="https://github.com/worldwide-asset-exchange/wax-blockchain" target="_blank">WAX Source Code Repository</a>).
- You can run the customizable **make** scripts from your smart contract's directory, without passing paths to your WASM and ABI files.

### What You'll Need:

- Docker must be installed and configured to run without sudo. Linux users, refer to <a href="https://docs.docker.com/install/linux/linux-postinstall/" target="_blank">Post-installation steps for Linux</a> for more information.

  :::tip
  <strong>Windows Subsystem for Linux Users:</strong> Docker configuration and installation requirements will vary depending on your WSL version. Recommended only for advanced Docker/Windows users. If you're running WSL 2, refer to <a href="https://docs.docker.com/docker-for-windows/wsl-tech-preview/" target="_blank">Docker Desktop WSL 2 Tech Preview</a> for more information.
  :::

- make (VERSION 3.9 +)
- A self-managed WAX Blockchain Account and its private key (to deploy the contract).

## Docker Depoy (WAX-CDT)

If you prefer, you can deploy your smart contracts from the command line using WAX-CDT tools.

### Advantages

- Allows more control over the build process and deployment parameters. Refer to [WAX-CDT Options](/build/tools/cdt_options)for more information.
- If you used **eosio-init** to [Create a Smart Contract](/build/dapp-development/wax-cdt/cdt_use.html#compile-hello-world/)and deploy to your local blockchain, this might be a good option for you.
- Compatible for Windows users.

### What You'll Need

To use this option, you'll need to:

- Complete our [Docker Quickstart](/build/dapp-development/docker-setup/)(recommended) or use the [WAX Blockchain Setup](/build/dapp-development/wax-blockchain-setup/)to build from source.
- Use the [WAX Contract Development Toolkit (WAX-CDT)](/build/dapp-development/wax-cdt/)to compile your smart contracts.

## Before You Begin

No matter which deployment option you choose, you'll need to:

- Create a self-managed WAX Blockchain Account.
- Make sure you have enough WAX staked in your account to allocate resources.

<ChildTableOfContents :max="2" title="More inside this section" />
