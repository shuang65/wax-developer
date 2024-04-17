---
标题: 区块链环境
顺序: 20
---

# 区块链环境

以下是 WAX 版本、URL 和开发环境信息。

| 服务 | 描述 |
|---------|-------------|
| [Docker Images](https://hub.docker.com/u/waxteam) | 使用 WAX Docker 镜像来运行本地节点、使用区块链工具，并编译您的智能合约。有关更多信息，请参考 [Docker 快速入门](/build/dapp-development/docker-setup/)。 |
| [waxjs](https://github.com/worldwide-asset-exchange/waxjs) |WaxJS 是用于与 Cloud Wallet 集成的 JavaScript API，可用于轻松让用户登录并从您的 dApp 向 WAX 链发送交易。详细信息请参考 [Cloud Wallet  快速入门](/build/cloud-wallet/waxjs/waxjs_qstart)。 |
| [wax-blockchain](https://github.com/worldwide-asset-exchange/wax-blockchain) | WAX 链的源文件。开始使用时，请参考 [WAX 链设置](/build/dapp-development/wax-blockchain-setup/) 。 |
| [wax-cdt](https://github.com/worldwide-asset-exchange/wax-cdt) | WAX 合约开发工具包。开始使用时， 请参考 [WAX 合约开发工具包 (WAX-CDT)](/build/dapp-development/wax-cdt/) 。 |

## WAX 主网

| 服务 | URL | 描述 |
|---------|-----|-------------|
| Blockchain URL | [chain-api-url](/operate/wax-infrastructure/#public-and-free-api-service-providers) |用于进行 API 调用并将您的智能合约部署到 WAX 主网。|
| Blockchain P2P | peers.wax.io:9876 | 用于同步生产者或完整节点（没有协议位于其前面）的对等端点。 |
| Blockchain Explorer | [https://waxblock.io](https://waxblock.io/) | waxblock.io 区块浏览器。 |
| WAX Account | (例如， Scatter) | 创建一个 WAX 链账户。 |

## WAX 公共测试网

[WAX sw/eden](https://waxsweden.org/) 提供了 WAX 测试网，您可以在这里创建测试账户、测试智能合约、使用 API 端点等功能。

| 服务 | URL | 描述 |
|---------|-----|-------------|
| Testnet Site | [WAX Testnet](https://waxsweden.org/testnet/) | 使用 WAX sw/eden 网站来创建测试账户、查找示例脚本等。 |
| Blockchain URL | [https://testnet.waxsweden.org](https://testnet.waxsweden.org) | 用于在 WAX 测试网络上进行 API 调用和部署您的智能合约。 |
| Public Endpoints | [endpoints.json](https://github.com/eosswedenorg/waxtestnet/tree/master/endpoints) | 其他的 P2P 和 API 端点 URL。 |
| Blockchain P2P | testnet.waxsweden.org:59876 | 用于同步生产者或完整节点（没有协议在其前面）的对等端点。 |
| Blockchain Explorer | [Bloks.io Testnet](https://local.bloks.io/?nodeUrl=testnet.waxsweden.org&coreSymbol=WAX&corePrecision=8&systemDomain=eosio&hyperionUrl=https%3A%2F%2Ftestnet.waxsweden.org) | Testnet block explorer. |
| Test Account | [https://waxsweden.org/create-testnet-account/](https://waxsweden.org/create-testnet-account/) | 使用 [Testnet首页上的 "创建测试账户"](https://waxsw

eden.org/testnet/) 或直接访问链接。 |

## WAX 本地测试网

当您 [设置本地 dApp 环境时](/build/dapp-development/)， 您可以使用以下 URL 对本地 API 进行调用。

| 服务 | URL | 描述 |
|---------|-----|-------------|
| Blockchain URL | [http://127.0.0.1:8888](http://127.0.0.1:8888) | 在您的本地开发环境中用来发起 API 调用。 |

## C++ 环境

您可以使用 C++ 编程语言编写 WAX 智能合约。不需要自定义语言，但您需要熟悉 WAX C/C++ API 库。该库包含与 WAX 链通信所需的核心文件。当您开始时，请参考：

- [WAX 合约开发工具包 (WAX-CDT)](/build/dapp-development/wax-cdt/)
- [WAX-CDT API](/build/api-reference/cdt_api)
- [智能合约快速入门](/build/dapp-development/smart-contract-quickstart/)

## 开发工具

您可以使用诸如 Sublime Text、Atom、CLion、Eclipse 或 Visual Studio 等产品的任何第三方 C++ 编辑器或集成开发环境（IDE）来编写您的智能合约。

[EOS Studio](https://www.eosstudio.io/) 是一个专为 EOSIO dApp 开发而设计的图形化集成开发环境（IDE），支持 Linux、Mac OS 和 Windows。它包含代码编辑器、合约检查器和网络管理器等工具。要将 WAX 与 EOS Studio 集成，可以参考我们的 [如何在 EOS Studio 中使用WAX文档](https://github.com/worldwide-asset-exchange/wax-blockchain/tree/develop/samples/eos-studio)。 我们提供了一个最小化集成脚本，并在 Ubuntu 18.04 上进行了开发和测试。

[eosjs](https://github.com/EOSIO/eosjs) 是一个 JavaScript API SDK，您可以使用它与 WAX 链 API 进行通信。有关更多信息，请参考 [WAX RPC API](/build/api-reference/rpc_api) 。

[dfuse](https://www.dfuse.io) 是一个强大的 API 套件，可以让您查询 WAX 链并实时流式传输数据。有关更多信息，请参考 [dfuse for WAX dApps](/build/api-reference/dfuse/) 。
