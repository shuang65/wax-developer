---
标题: WalletConnect Developer Guide
顺序: 1
---

# WalletConnect 开发者指南

<br />

## 1. 获取密钥

- 输入与WalletConnect相关联的账户名
- 点击 “获取可用密钥” 按钮。

![](/assets/images/build/wallet-connect/wallet-connect-8.png)


## 2. 序列化交易

输入所需的操作。示例可能如下所示：

![](/assets/images/build/wallet-connect/wallet-connect-9.png)

![](/assets/images/build/wallet-connect/wallet-connect-10.png)

## 3. 签署交易:

- 输入第一步中的密钥和第二步中的序列化数据。 
- 使用提供的交易示例，并用你的个人信息修改它。
- 点击 WAX_SIGN_TRANSACTION。

完成后，请在 Cloud 钱包上批准交易弹出窗口，发送 dApp 的签名交易请求。dApp 将确认交易批准。

![](/assets/images/build/wallet-connect/wallet-connect-11.png)

![](/assets/images/build/wallet-connect/wallet-connect-12.png)

## 4. 消息签名

- 输入密钥 (来自第一步)。
- 输入给定的消息样本
- 点击 WAX_SIGN_MESSAGE。

经批准后，dApp 将会给出确认。

![](/assets/images/build/wallet-connect/wallet-connect-13.png)


## 5. 推送交易签名

- 使用第一步中的密钥和第二步中的序列化数据。
- 使用你的个人信息修改给定的交易示例。
- 按下 “WAX_SIGN_PUSH_TRANSACTION”.

![](/assets/images/build/wallet-connect/wallet-connect-14.png)

当您批准后，dApp将发送确认。

![](/assets/images/build/wallet-connect/wallet-connect-15.png)


WalletConnect 和 dApp 集成提供了管理数字交易的简单方式。按照上述步骤进行操作，将确保连接和交易体验的顺畅。始终保持更新最新版本和补丁，以修复已报告的任何错误。


**Join the WAX Community**

[Twitter](https://twitter.com/WAX_io) | [Discord](https://go.wax.io/discord) | [WAX.io](https://www.wax.io/)


