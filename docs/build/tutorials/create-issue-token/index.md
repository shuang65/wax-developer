---
标题: 创建并铸造一个同质化代币
顺序: 10
---

# 创建并铸造一个同质化代币

在这篇教程中，您将学习如何在WAX主网上创建并铸造一个同质化代币。

## 开始之前

* 您需要完成我们的 [Docker快速入门](/build/dapp-development/docker-setup/) (推荐) ，并使用 [WAX 链开发指南](/build/dapp-development/) 从源代码构建。

* 要编译和部署您的智能合约，需要使用 [WAX 合约开发工具包 (WAX-CDT)](/build/dapp-development/wax-cdt/)。

* 要在WAX主网或WAX测试网上部署您的智能合约，需要创建一个自主管理的WAX链账户。

## 从GitHub克隆智能合约

1. 从WAX的GitHub存储库中克隆fungible asset（可替换资产）智能合约：

    ```shell
    git clone https://github.com/worldwide-asset-exchange/wax-system-contracts.git
    ```

2.进入智能合约目录：

    ```shell
    cd wax-system-contracts/contracts/eosio.token
    ```

:::重要提醒
接下来的操作中，需要解锁钱包
```shell
cleos wallet unlock
```
:::

:::提示 注意
将这些变量替换为您想输入的值。
- `<TOKEN_ACCOUNT_NAME>`: Name of the fungible asset token account (Will be the owner of the fungible asset token).
- `<OWNER_PUBLIC_KEY>`: Public key of the fungible asset token account.
- `<ACTIVE_PUBLIC_KEY>`: Active public key of the fungible asset token account.
- `<ACTIVE_PRIVATE_KEY>`: Active private key of the fungible asset token account.
- `<MAX_ISSUE>`: Maximum amount of fungible asset tokens to mint.
- `<SYMBOL>`: Symbol of the fungible asset token.
- `<AMOUNT>`: Amount of fungible asset tokens to mint (issue) or to send (transfer). The total of minted tokens cannot exceed the `<MAX_ISSUE>` value.
:::


3. 为同质化代币创建一个账户。

     ```shell
    cleos create account eosio <TOKEN_ACCOUNT_NAME> <OWNER_PUBLIC_KEY> <ACTIVE_PUBLIC_KEY>
    ```

5. 将同质化代币账户添加至钱包。

    ```shell
    cleos wallet import --private-key <ACTIVE_PRIVATE_KEY>
    ```

6. 编译智能合约：

    ```shell
    mkdir build
    cd build
    cmake ..
    make
    ```
7. 在WAX主网部署智能合约：

    ```shell
    cleos set contract eosio.token ../ --abi eosio.token.abi -p <TOKEN_ACCOUNT_NAME>@active
    ```
8. 铸造同质化代币：

    ```shell
    cleos push action <TOKEN_ACCOUNT_NAME> create '["<TOKEN_ACCOUNT_NAME>", "<MAX_ISSUE> <SYMBOL>"]' -p <TOKEN_ACCOUNT_NAME>@active
    ```

9. 验证同质化代币是否已正确铸造：
    ```shell
    cleos get currency stats <TOKEN_ACCOUNT_NAME> <SYMBOL>
    ```
10. 铸造更多的同质化代币：

    ```shell
    cleos push action <TOKEN_ACCOUNT_NAME> issue '["<TOKEN_ACCOUNT_NAME>", "<AMOUNT> <SYMBOL>", "memo"]' -p <TOKEN_ACCOUNT_NAME>@active
    ```
11.验证其他的同质化代币是否已正确铸造：
    ```shell
    cleos get currency stats <TOKEN_ACCOUNT_NAME> <SYMBOL>
    ```

12. 将同质化代币转移至另一个账户：

     ```shell
    cleos push action <TOKEN_ACCOUNT_NAME> transfer '["<TOKEN_ACCOUNT_NAME>", "<RECIPIENT_ACCOUNT_NAME>", "<AMOUNT> <SYMBOL>", "memo"]' -p <TOKEN_ACCOUNT_NAME>@active
    ```
  
14. 验证同质化代币是否已正确转移：

     ```shell  
    cleos get currency balance <TOKEN_ACCOUNT_NAME> <RECIPIENT_ACCOUNT_NAME> <SYMBOL>
    ```

恭喜！您已在WAX主网上创建并铸造了同质化代币。
