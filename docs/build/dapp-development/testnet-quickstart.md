---
标题: WAX 测试网快速入门
顺序: 66
---

在这篇指南中，您将学习如何创建测试网账户并将智能合约部署到WAX测试网。

:::提示
每个智能合约都需要一个账户。建议您根据智能合约的功能来命名账户（例如， mywaxnftgame)。 账户名必须是12个字符，并且只能包含字母 [a-z] 和数字 [1-5]。
:::

## 创建并给测试网账户提供资金

1. <a href="https://waxsweden.org/testnet/" target="_blank">创建一个测试网账户</a>。将您的私钥和公钥保存在安全的地方。 

2. 从测试网主页获取免费的WAX代币以此您的新账户提供资金。

3. 要部署智能合约，您需要使用公钥和私钥创建一个钱包。可以使用 <a href="https://local.bloks.io/wallet/transfer?nodeUrl=testnet.waxsweden.org&coreSymbol=WAX&corePrecision=8&systemDomain=eosio&hyperionUrl=https%3A%2F%2Ftestnet.waxsweden.org" target="_blank">Bloks.io</a>上的钱包功能，或者使用 [Docker 镜像](/build/dapp-development/docker-setup/)来管理钱包。 

   从Docker容器中创建钱包，请使用 `cleos wallet` 命令：

    ```shell
    cleos rm -f ~/eosio-wallet/{account.name}.wallet &&
    cleos wallet create -n {account.name} --to-console &&
    cleos wallet import -n {account.name} --private-key {active.privatekey} &&
    cleos wallet import -n {account.name} --private-key {owner.privatekey}
    ```

   将钱包密码存储在安全的地方，需要它来运行命令。

4. 当您的钱包配置好了测试网账户后，可以在Bloks.io或Docker容器中抵押NET、CPU和RAM。

    购买 RAM:

    ```shell
    cleos -u https://testnet.waxsweden.org system buyram {account.name} {account.name} "3.00000000 WAX"
    ```

    将NET和CPU质押到自己账户:

    ```shell
    cleos -u https://testnet.waxsweden.org system delegatebw {account.name} {account.name} "4.00000000 WAX" "5.00000000 WAX"
    ```

## 将智能合约部署到WAX测试网

:::提示
做这些这些步骤之前，请确保您的钱包已打开并处于解锁状态。有关更多信息，请参考接下来的故障排除部分。
:::

1. 在交互式的Docker bash会话中，导航至您的智能合约目录，并构建智能合约。

    ```shell
    eosio-cpp -abigen waxnft.cpp -o waxnft.wasm 
    ```

2. 如果智能合约需要调用外部合约的操作（例如， WAX RNG 或 Simple Assets)，请提升您的账户权限：

    ```shell
    cleos -u https://testnet.waxsweden.org set account permission {account.name} active --add-code
    ```

3. **部署.** 命令行中，使用 `cleos set contract` 设置您的合约：

    ```shell
    cleos -u https://testnet.waxsweden.org set contract {account.name} $(pwd) waxnft.wasm waxnft.abi   
    ```

您的智能合约现在已经在WAX测试网上部署成功！ 

## 故障排除

如果遇到钱包和/或授权错误，您可能需要打开并解锁您的钱包：

```shell
cleos wallet open -n {account.name} &&
cleos wallet unlock -n {account.name} --password {wallet.pwd}
```
