---
标题: WAX 链设置
顺序: 30
---

# WAX 链设置

当要建设和使用WAX链时， 建议您使用我们的 <a href="https://hub.docker.com/u/waxteam" target="_blank">waxteam - Docker Images</a>。 我们的Docker镜像能起到快速、完全支持的作用，能在几秒钟内运行节点。有关更多信息，请参阅[Docker Quickstart](/build/dapp-development/docker-setup/) 获得更多信息。

Docker镜像包含了来自 <a href="https://github.com/worldwide-asset-exchange/wax-blockchain" target="_blank">WAX 链源代码库</a>中的所有内容， 这样您就可以运行WAX节点，构建和部署智能合约。

如果您想从本地驱动器访问我们的示例合约和脚本，或者需要安装WAX链而不是使用Docker，您可以使用这个方法下载并选择性的构建WAX链源代码。

:::警告
重要： 目前没有提供预编译的软件包。 如果您选择从源代码构建WAX区块链，我们将无法提供帮助。
:::

## 包含什么

WAX链是基于 <a href="https://docs.eosnetwork.com/" target="_blank">EOS (Antelope)</a>的一个分支。这个 <a href="https://github.com/worldwide-asset-exchange/wax-blockchain" target="_blank">WAX 链源代码库</a> 包含并安装了以下内容：

- WAX 链源代码
- 依赖项
- [区块链工具](/build/tools/blockchain_tools), 包括, nodeos, 和 cleos
- 示例合约

您可以使用这些组件来管理本地钱包、创建账户、与WAX链进行交互等操作。

:::警告
<strong>EOS 开发者:</strong> 构建WAX源代码库将会覆盖之前的EOS的库。
:::

### Docker Quick Deploy

WAX 源代码库包含一个Hello World示例，可以快速构建和部署WAX智能合约到WAX链上。更多信息请参考 [Docker 快速部署](/build/dapp-development/deploy-dapp-on-wax/deploy_docker) 。

### 依赖项

<p>要查看完整的依赖项列表，请参考 <a href="https://github.com/worldwide-asset-exchange/wax-blockchain/tree/develop/scripts" target="_blank">wax-blockchain/scripts</a> 并找到适用于您操作系统的 `wax_build_` 文件。</p>

## 系统要求

如果没有使用我们的Docker镜像，您需要：

- 请查看 [支持的操作系统](/build/tools/os) ，以确保您的操作系统符合要求。

  :::警告
  <strong>Ubuntu 18.04 用户:</strong> 在要开始WAX链设置之前，请参考 [已知问题](/build/troubleshooting/)。
  :::

- 至少需要有 7 GB 的空置内存。

- 至少还有20 GB 的硬盘空间。
