---
标题: 在WAX上部署一个EOS dApp 
顺序: 10
---

# 在WAX上部署一个EOS dApp 

WAX与EOS智能合约完全兼容，并提供免费的区块链账户和更低的费用。本指南概述了如何将您的EOS dApps部署到WAX主网。

## 区块链账户

1. 要在WAX主网上部署您的智能合约，您需要创建一个自主管理的WAX链账户。
   
3. 确保您的账户有足够的WAX抵押来分配资源。

4. 如果您的dApp需要与账户进行交互，您的客户也需要创建一个免费的、经过验证的WAX链账户。您可以将他们引导到以下链接：

    <a href="https://all-access.wax.io" target="_blank">http://<span></span>all-access.wax.io</a>

    Cloud Wallet账户会自动为您的客户创建WAX链账户，并允许您将WaxJS集成到您的dApps中。详细信息请参阅 [Cloud Wallet  快速入门](/build/cloud-wallet/waxjs/waxjs_qstart)。

## 开发环境

如果您想在WAX上测试您的智能合约，您可以：

* 完成我们的 [Docker 快速入门](/build/dapp-development/docker-setup/)(推荐) 或使用 [WAX 链设置](/build/dapp-development/wax-blockchain-setup/)从源代码构建。
* 使用 [WAX 合约开发工具包 (WAX-CDT)](/build/dapp-development/wax-cdt/ 来构建您的合约。
* [设置本地 dApp 环境](/build/dapp-development/setup-local-dapp-environment/。
* 部署到 [WAX 测试网](/build/dapp-development/testnet-quickstart/。

:::警告
在本地开发环境中设置WAX源代码会覆盖当前的EOS安装。如果您想保留EOS环境，如果您想保留EOS环境，请使用Docker、虚拟机或另一个独立的开发环境。
:::

## 部署到您的智能合约

您必须使用 [WAX 合约开发工具包 (WAX-CDT)](/build/dapp-development/wax-cdt/来编译您的智能合约。

如果您不想安装WAX源代码，您可以使用我们的 [Docker 快速入门](/build/dapp-development/docker-setup/)或自定义脚本来部署您的智能合约。有关更多信息，请查阅 [在 WAX上部署您的dApp](/build/dapp-development/deploy-dapp-on-wax/).
