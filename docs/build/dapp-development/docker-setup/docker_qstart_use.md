---
标题: 运行命令
顺序: 23
---

# 运行命令

当您启动 **waxdev** bash 会话后， 您可以使用常见的命令与容器进行交互。例如，要查看容器中的文件和目录，您可以使用 `ls` 命令。

```shell
ls
```

控制台输出：

```shell
bin  boot  dev  etc  home  lib  lib32  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var  wax
```

上面的列表包含了您在启动 **wax** 容器时共享的 **waxdev** 目录。 当你准备好 [创建智能合约](/build/dapp-development/smart-contract-quickstart/dapp_hello_world)，可以进入此目录。

:::提示
通过将您的本地主机文件夹与waxdev Docker容器共享，您可以在主机和Docker容器上创建相同的目录，从而轻松地使用Docker构建和部署智能合约。
:::

## 用户指南

在我们的 dApp 开发部分，我们将列出运行区块链命令和构建智能合约所需的各种步骤。例如：

1. 命令行使用 `cleos` 命令获取 WAX 主网的链信息。
   
```shell
cleos -u https://wax-api-url get info
```
*检查 https://validate.eosnation.io/wax/reports/endpoints.html获取最新的 API 端点 URL*
<p>&nbsp;</p>

当您启动一个交互式的bash会话时，*命令行* 就是您在Docker容器中的bash提示符：

![](/assets/images/dapp-development/docker-setup/docker_root.jpg)

当你按下 `Enter` 运行命令时， 控制台会在您的Docker容器中直接打印一个JSON响应：

![](/assets/images/dapp-development/docker-setup/docker_results.jpg)

