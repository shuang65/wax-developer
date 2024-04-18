---
标题: 验证您的安装
顺序: 32
---

# 验证您的安装

要验证您的安装，可以使用 **cleos** 调用 WAXBlockchain API上的`get info`端点。
<p>&nbsp;</p>

在命令行输入以下内容：

```shell
cleos -u https://wax-api-url get info
```
*查看https://validate.eosnation.io/wax/reports/endpoints.html 以获取最新的 API 端点 URL*
<p>&nbsp;</p>

如果 [区块链工具](/build/tools/blockchain_tools) 安装成功，这个端点将返回关于WAX链的各种信息，包括 `chain_id`，区块生产者和最新区块高度。

![](/assets/images/dapp-development/docker-setup/docker_results.jpg)

