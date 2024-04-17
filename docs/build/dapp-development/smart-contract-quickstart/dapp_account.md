---
标题: 创建 账户
顺序: 63
---

# 创建 账户

WAX账户储存在链上，用于识别您的智能合约和dApp用户。在本地生产环境中，发送或接收有效交易到链上都需要使用账户。 

## 如何工作

您需要创建几种不同类型的账户来部署智能合约：

- **主账户:** 您的WAX主账户， 用于抵押WAX获取CPU和RAM资源。 在本地开发环境中，此账户是通过 **eosio** 系统用户模拟的。您可以使用此系统用户在本地开发环境中创建各种类型的账户。在生产环境中，所有WAX账户都是免费的。
- **智能合约账户:** 每个智能合约都需要一个独立的账户。 
- **客户账户** 这些账户用于与您的智能合约进行交互。在本地开发环境中，您可以创建无数个客户账户。

在这个指南中，您将使用 **cleos** 创建一个 WAX 链账户，用于部署您的智能合约。

:::提示
要查看 cleos create account 的所有子命令和选项， 请参考 <a href="https://docs.eosnetwork.com/leap/latest/cleos/command-reference/create/account" target="_blank">Cleos 参考指南:创建账户</a>.
:::

## 开始之前

- **节点** 必须正在运行 
    ```shell
    nodeos -e -p eosio \
        --plugin eosio::producer_plugin \
        --plugin eosio::chain_api_plugin \
        --plugin eosio::http_plugin \
        --access-control-allow-origin='*' \
        --contracts-console \
        --http-validate-host=false \
        --verbose-http-errors >> nodeos.log 2>&1 &
    ```
- 您的钱包必须是打开并处于解锁的状态
    ```shell
    cleos wallet open
    ```

    ```shell
    cleos wallet unlock --password PW5KRXKVx25yjL3FvxxY9YxYxxYY9Yxx99yyXTRH8DjppKpD9tKtVz
    ```

<!--"/usr/opt/eosio/1.7.3/bin/keosd" launched
Failed to connect to nodeos at http://127.0.0.1:8888/; is nodeos running?

Error 3120006: No available wallet
Ensure that you have created a wallet and have it open
Error Details:
You don't have any wallet!-->

## 生成公/私钥

每个 WAX 账户都需要至少一个公钥。公钥有两种类型，根据账户权限而定：

- **Owner Key:** 必需的。这是主要的公钥，具有完整的权限和完全的控制权。在生产账户中，您不应将此公钥用于大多数交易。此公钥在您的本地钱包中有一个私钥/公钥记录
- **Active Key:** 可选的。这是次要的，该密钥可以由Owner密钥更改。它需要额外的私钥/公钥对，可以在您的本地钱包中找到。在生产中，可以使用此密钥进行投票、发送和接收交易。

当您要为智能合约创建一个账户时，需要在本地的开发钱包中生成一个公钥和私钥对。您可以通过钱包的 `create_key` 命令来完成:

:::提示
为了创建密钥对，您需要确保您的钱包已打开并解锁。
:::

```shell
cleos wallet create_key
```

控制台输出您的公钥:

```shell
warn  2019-07-16T23:16:23.435 thread-0  wallet.cpp:223                save_wallet_file     ] saving wallet to file /home/username/eosio-wallet/./default.wallet
Created new private key with a public key of: "EOS4yxqE5KYv5XaB2gj6sZTUDiGzKm42KfiRPDCeXWZUsAZZVXk1F"
```

把这个公钥存放在一个容易找到的地方（下一步会需要这个公钥）。

## 创建智能合约账户

要创建一个WAX智能合约账户，请使用 `create account` 命令:

| 参数 | 示例 | 描述
| --- | ----------- | -------------------------- |
| creator | eosio | 这个参数是用来创建新账户的主要账户名称。在生产环境中，这个主要账户就是您的 WAX 账户。 |
| name | waxsc1 | 新账户的名称。账户名称必须少于13个字符，并且只能包含字母[a-z]和数字[1-5]。 |
| OwnerKey | EOS4yxqE5KYv5XaB2gj6sZTUDiGzKm42KfiRPDCeXWZUsAZZVXk1F | 公钥是您从本地开发钱包生成的。 |

### 示例

```shell
cleos create account eosio waxsc1 EOS4yxqE5KYv5XaB2gj6sZTUDiGzKm42KfiRPDCeXWZUsAZZVXk1F 
```

**cleos** broadcasts the `create account` command to your local blockchain and your wallet signs this transaction with a HASH.

```shell
executed transaction: 4ebdc2eabcd545c7f26679e95d729893ebd0df919850791daa79a10e4865f702  200 bytes  15013 us
#         eosio <= eosio::newaccount            {"creator":"eosio","name":"waxsc1","owner":{"threshold":1,"keys":[{"key":"EOS4yxqE5KYv5XaB2gj6sZTUDi...
warning: transaction executed locally, but may not be confirmed by the network yet         ]
```

You should now have a WAX Blockchain Account to associate with your smart contract.

## 验证您的新账户

要查看新账户的信息，请使用  `get account` 命令:

```shell
cleos get account waxcustomer
```

控制台输出您新账户的详细信息。 请注意，因为我们在创建账户时没有更改active公钥，所以owner和active的密钥是相同的。

```shell
created: 2019-07-22T20:22:16.000
permissions:
     owner     1:    1 EOS4yxqE5KYv5XaB2gj6sZTUDiGzKm42KfiRPDCeXWZUsAZZVXk1F
        active     1:    1 EOS4yxqE5KYv5XaB2gj6sZTUDiGzKm42KfiRPDCeXWZUsAZZVXk1F
memory:
     quota:       unlimited  used:      2.66 KiB

net bandwidth:
     used:               unlimited
     available:          unlimited
     limit:              unlimited

cpu bandwidth:
     used:               unlimited
     available:          unlimited
     limit:              unlimited
```



