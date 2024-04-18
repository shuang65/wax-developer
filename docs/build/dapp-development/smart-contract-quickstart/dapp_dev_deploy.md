---
标题: 将智能合约部署到链上
顺序: 65
---

# 将智能合约部署到链上

<!--To deploy your smart contract to your local development blockchain, you'll need to:

- Compile your smart contract
- Create a blockchain account for your smart contract.-->

在此指南中， 将使用 **cleos** 来部署和测试您在 [创建智能合约](/build/dapp-development/wax-cdt/cdt_use.html#compile-hello-world) 教程中创建和编译的 WAX 智能合约。 

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
- 您的钱包必须打开并处于解锁状态
    ```shell
    cleos wallet open
    ```

    ```shell
    cleos wallet unlock --password PW5KRXKVx25yjL3FvxxY9YxYxxYY9Yxx99yyXTRH8DjppKpD9tKtVz
    ```
- 如果您还没有为智能合约创建一个WAX账户，则必须先完成账户创建， 请参阅 [创建账户](/build/dapp-development/smart-contract-quickstart/dapp_account) 进行操作。

## 部署您的智能合约

要把您的智能合约的 WASM 文件部署到本地区块链，可以用命令行里的 `cleos set contract`：

| 参数 | 示例 | 描述
| --- | ----------- | -------------------------- |
| account | waxsc1 | 您的智能合约账户 |
| path | /users/wax-blockchain/wax-cdt/mycontracts/wax | 您的 WASM 文件的完整路径。 |
| permission | -p waxsc1@active | 您的智能合约账户的active权限或owner权限。 |

```shell
cleos set contract waxsc1 /users/wax-blockchain/wax-cdt/mycontracts/wax -p waxsc1@active
```

控制台将输出以下信息:

```shell
Reading WASM from /users/wax-blockchain/wax-cdt/mycontracts/wax/wax.wasm...
Publishing contract...
executed transaction: 8a79664a3f0457513fabaa5753c41b18588cb2994cd5e3164328eafc9663f7a8  2832 bytes  57440 us
#         eosio <= eosio::setcode               {"account":"waxsc1","vmtype":0,"vmversion":0,"code":"0061736d01000000013a0b60017f0060027f7f0060037f7...
#         eosio <= eosio::setabi                {"account":"waxsc1","abi":"0e656f73696f3a3a6162692f312e3100010567726565740000010000000080acd46505677...
warning: transaction executed locally, but may not be confirmed by the network yet         ]
```

您的智能合约现在已经部署在本地区块链上。

## 测试您的智能合约
要测试您的智能合约， 请在命令行使用`cleos push action` ：
| 参数 | 示例 | 描述
| --- | ----------- | -------------------------- |
| account | waxsc1 | 您的智能合约账户 |
| action | hi | action名称 |
| datastream | '["YourName"]' | 输入您的名字或其他字符串 |
| permission | -p waxsc1@active | 智能合约账户的active权限或owner权限。 |

```shell
cleos push action waxsc1 hi '["YourName"]' -p waxsc1@active
```

控制台将输出以下信息:

```shell
executed transaction: 6a0b1489d903f2cacc6480830358f07aaf65b20bf1d7e855dc20097f4d64dc52  104 bytes  1727 us
#        waxsc2 <= waxsc2::hi                   {"nm":"YourName"}
>> Name : YourName
warning: transaction executed locally, but may not be confirmed by the network yet         ]
```

如果收到交易超时的错误，请再次运行  `cleos push action` 。 如果还是有错误，请尝试重新启动  **nodeos**。

```shell
Error 3080006: Transaction took too long
Error Details:
deadline exceeded
pending console output:
```
