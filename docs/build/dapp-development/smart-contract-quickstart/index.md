---
标题: 智能合约快速入门
顺序: 60
---

# 智能合约快速入门

WAX 智能合约是一个经过 WASM 编译的 C++ 文件，在 WAX 链上执行操作，并将数据永久存储在每个 WAX 全节点的 RAM 中。

在该教程中， 你将学习如何在本地开发环境中创建、编译和部署一个 WAX 智能合约。

## 开始之前

- 您需要先完成我们的 [Docker 快速入门](/build/dapp-development/docker-setup/) (推荐) 或使用 [WAX 链设置](/build/dapp-development/wax-blockchain-setup/) 从源代码构建。
- 确保您的本地开发环境已准备好。更多信息请参考 [Set Up a Local dApp Environment](/build/dapp-development/) 。
- 要在本地编译和部署您的智能合约， 您需要使用 [WAX 合约开发工具包 (WAX-CDT)](/build/dapp-development/wax-cdt/) ，并且对于一些基本概念，如 WASM 和 ABI 文件的生成需要有一定了解。

<ChildTableOfContents :max="2" title="More inside this section" />
