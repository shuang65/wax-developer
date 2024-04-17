---
标题: 安装Docker 
顺序: 21
---

# 安装Docker 

[Docker](https://www.docker.com/)  是一个类似于虚拟机的容器平台。它可以让你在一个独立的环境中运行软件、应用，甚至像 Ubuntu 这样的操作系统。想要了解更多信息，请参考Docker的 [Overview](https://www.docker.com/why-docker) 概述指南。

我们的开发和生产 Docker 镜像让您能够在几分钟内快速、轻松地运行 WAX 区块链。此外，您还可以使用我们的 Docker 镜像来构建和部署智能合约。

使用我们的 Docker 环境具有以下优点：

- 为您的开发工作提升了速度并增添了便利性。
- 无需管理源代码。
- 无需符合我们 [支持的操作系统](/build/tools/os) 要求。
- 不会覆盖已安装了的 Leap。
- 使得升级和尝试新功能变得简单。
- 可以轻松切换生产和开发环境。

## 包括什么

以下是我们核心 Docker 镜像的列表。要查看完整列表，请参考 [waxteam - Docker Repositories](https://hub.docker.com/u/waxteam).

| Docker 镜像 | 描述 |
|--------------|-------------|
| [waxteam/dev](https://hub.docker.com/r/waxteam/dev) | 这个 **开发** 镜像 包含了启动和运行 WAX 区块链所需的所有内容。 您可以使用此镜像来运行 WAX 节点，创建本地开发环境，并使用 [WAX 合约开发工具包 (WAX-CDT)](/build/dapp-development/wax-cdt/)来创建或编译智能合约。
| [waxteam/cdt](https://hub.docker.com/r/waxteam/cdt) | 使用此镜像可以使用 [WAX 合约开发工具包 (WAX-CDT)](/build/dapp-development/wax-cdt/)来创建和编译智能合约。 此镜像 **不** 支持运行WAX节点或使用 [区块链工具](/build/tools/blockchain_tools)。 |
| [waxteam/production](https://hub.docker.com/r/waxteam/production) | 建议您使用我们的 [production docker 镜像](https://hub.docker.com/r/waxteam/production) 来运行节点。有关更多信息，请参阅 [Running a WAX node](https://github.com/worldwide-asset-exchange/wax-blockchain/tree/develop/samples/mainnet) 。 |

<ChildTableOfContents :max="2" title="More inside this section" />
