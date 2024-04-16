---
标题: WaxJS 概述
---

# wax.js

**WaxJS** 是一个 JavaScript 库，用于连接 Cloud Wallet，以便为用户签名并执行智能合约交易，无需外部钱包（例如 Scatter）。类似于标准的 OAuth 2.0 流程，用户只需授权您的 dApp 访问其 WAX 链账户。一旦您的 dApp 获得授权，用户就可以从其 Cloud Wallet 账户批准您的智能合约交易。

开始使用时， 您只需导入我们的 [WaxJS](https://github.com/worldwide-asset-exchange/waxjs) 库，并在您的客户端进行几个简单的调用。如果您希望直接查看代码并运行我们的实时 WaxJS 示例， 请参阅 [WaxJS Demo](waxjs_demo.md).
## 工作原理

**WaxJS** 使用 Cloud Wallet 和 [EOSIO/eosjs](https://github.com/EOSIO/eosjs)  Javascript API，为您的用户和 WAX 区块链之间提供了一个易于使用的接口。




要使用 **WaxJS**， 您只需:

1. 将 **WaxJS** 库添加至您的客户端
2. 使用 `wax.login` 可以让用户通过 Cloud Wallet登录  (支持自动登录功能)

![WaxJS Login](/assets/images/wax-cloud-wallet/waxjs/waxjs_login.png)

3. 使用 `wax.api` 将您的交易发送到WAX链
![WaxJS Sign](/assets/images/wax-cloud-wallet/waxjs/waxjs_sign.png)

在接下来的部分，您将学习如何安装和使用 **WaxJS**.
