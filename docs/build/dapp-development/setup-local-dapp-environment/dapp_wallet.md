---
标题: 创建一个钱包
顺序: 43
---

# 创建一个钱包

WAX钱包是一个具有名称的加密存储库，其中包含公钥和私钥对的文件，这些文件存储在您的本地服务器上（而不是区块链上）。您需要创建一个开发钱包：

- 创建本地WAX链账户
- 对于在本地区块链上执行的操作进行签名

## 如何工作

要在本地区块链上创建账户，需要一个已经生成的 owner 公钥（必须的），以及一个 active 公钥（可选的）。您可以使用本地开发钱包来创建和保存这些公钥。 

### 默认钱包内容 - 公钥/私钥对
```shell
[[
    "EOS4yxqE5KYv5XaB2gj6sZTUDiGzKm42KfiRPDCeXWZUsAZZVXk1F",
    "5JTZaN1zabi5wyC3LcdeZG3AzF7sLDX4JFqMDe68ThLC3Q5nYez"
  ],[
    "EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV",
    "5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3"
  ]
]
```

您的钱包将使用这些密钥来对智能合约的操作进行签名，并将签名广播到您的本地网络。如果网络确认交易有效，则将其包含在链上的一个区块中。 

:::提示
钱包不存储代币，只存储与该链账户相关联的密钥对。 
:::

在这个指南中，您将使用 **cleos** 工具来创建、打开和解锁一个新的钱包。

:::警告
<strong>注意:</strong> 在完成这些步骤时，无需运行 <strong>nodeos</strong> 。 如果**kleos**尚未运行，它将自动启动。
:::


## 创建一个默认钱包

要创建一个新的钱包，请使用 `wallet create` 命令：

```shell
cleos wallet create --to-console
```

这个命令创建了一个名为 **default**的钱包， 并将其保存到本地路径 (例如， "/home/username/eosio-wallet/default.wallet")。

:::提示
您还可以使用 --name 参数来制定一个钱包的名称： `cleos wallet create --name mywallet --to-console`。
:::

`--to-console` 参数会将您的密码输出到控制台上。请确保将此密码存放在安全的地方（需要它来解锁您的钱包）。

```shell
warn  2019-07-16T22:39:39.847 thread-0  wallet.cpp:223                save_wallet_file     ] saving wallet to file /home/username/eosio-wallet/./default.wallet
Creating wallet: default
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"PW5KRXKVx25yjL3FvxxY9YxYxxYY9Yxx99yyXTRH8DjppKpD9tKtVz"
```

:::提示
要查看 cleos wallet 的完整子命令和参数列表，请参考 <a href="https://docs.eosnetwork.com/leap/latest/cleos/command-reference/wallet/" target="_blank">Cleos 参考 指南</a>。
:::

## 打开并解锁您的钱包

钱包在默认情况下是关闭的 (在启动 **keosd** 实例时)。 要打开您的钱包， 请使用 `wallet open` 命令：

```shell
cleos wallet open
```

控制台会输出您 **default** 钱包已打开的消息： `Opened: default`。

:::提示
您还可以使用 --name参数根据名称打开一个钱包： `cleos wallet open --name named-wallet`。
:::

现在您的钱包已经打开，需要解锁。可以使用 `cleos wallet open --name named-wallet` 命令来解锁。使用在创建钱包时输出到控制台的密码。

```shell
cleos wallet unlock --password PW5KRXKVx25yjL3FvxxY9YxYxxYY9Yxx99yyXTRH8DjppKpD9tKtVz
```

控制台会输出您的 **default** 钱包已解锁的消息: `cleos wallet open --name named-wallet`。

:::提示
默认情况下， **keosd** 会在不使用的15分钟后自动锁定您的钱包。 要禁用此功能，您需要修改，**/home/username/eosio-wallet/config.ini** 文件中的一个数据，将其设置为一个比较大的数字。将其设置为0会导致 keosd 一直锁定您的钱包。
:::


要确定您的钱包是否已锁定/解锁，您可以使用以下命令：


```shell
cleos wallet list
```

控制台会输出您的钱包名称，并使用星号 (*) 来表示您的钱包已解锁：

```shell
Wallets:
[
  "default *"
]
```

:::提示
如果您稍后回到这一步骤（在终止 **kleos** 实例后），并且您的 **default** 钱包未列出： `cleos wallet open --name named-wallet`，则需要再次打开并解锁您的钱包。
:::


## 导入本地开发密钥

出于开发需要，WAX 链包含一个名为 eosio 的默认系统用户。该账户用于设置本地链，通过加载系统合约来规定治理和共识机制。 

在您的本地开发环境中， **eosio** 用户将模拟您的 WAX 链账户。您可以使用 **eosio** 用户创建新账户，并将您的智能合约推送到本地区块链，而无需担心关于抵押WAX的问题。

为了代表 **eosio**  系统用户签署交易，需要将 **eosio** 的开发密钥导入到您的钱包中。 

:::提示
重要: 这个开发密钥 **对于所有 WAX 和 Antelope 开发者都是相同的**。 不要将此密钥用于注册 WAX 账户！ 这样做肯定会导致您无法访问自己的账户。
:::


```shell
cleos wallet import --private-key 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3
```

The console prints that your development key has been imported for: (your private wallet key).

```shell
imported private key for: EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
```
