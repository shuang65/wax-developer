---
标题: 部署您的 WAX RNG 智能合约
顺序: 85
---

# 部署您的 WAX RNG 智能合约

在该例中，我们将使用WAX-CDT工具来部署您的幸运数字生成器智能合约。更多信息请参考 [WAX-CDT 部署](/build/dapp-development/deploy-dapp-on-wax/deploy_source) 。

1. 首先，我们需要在测试网或主网上创建一个账户来部署智能合约。在该例中，我们假设账户名为 *mywaxrngtest*。

**注意:** 您可以使用 [WAXSweden](https://waxsweden.org/testnet/) 团队的工具来创建测试网账户，并为其提供所需资金以购买智能合约部署所需的Ram。
:::

2. 在Docker中，我们打开并解锁在 [如何创建开发环境](/build/dapp-development/setup-local-dapp-environment/dapp_wallet)教程中创建的钱包。

```shell
cleos wallet open -n mywallet && cleos wallet unlock -n mywallet --password {wallet.pwd}
```
然后导入 mywaxrngtest的 active密钥 

```shell
cleos wallet import --private-key {mywaxrngtest_active_private_key}
```

3. 为了在**orng.wax**智能合约上执行内联 **requestrand** 操作， 您需要新的 **mywaxrngtest@active**权限添加额外的 **eosio.code** 权限。 这个权限能提升安全性，并允许您的智能合约发送内联操作。请从命令行运行 `cleos set account permission` 命令， 并包含 `--add-code` 参数。

```shell
cleos -u [chain-api-url] set account permission mywaxrngtest active --add-code
```

验证新的权限，请使用 `cleos get account` 命令：

```shell
cleos -u [chain-api-url] get account mywaxrngtest
```

4. 购买一些RAM以部署智能合约：

```shell
cleos -u [chain-api-url] push action eosio buyram '["mywaxrngtest", "mywaxrngtest", "200.00000000 WAX"]' -p mywaxrngtest@active  
```

5. 最后，使用`cleos set contract`命令设置您的智能合约：

```shell
cleos -u [chain-api-url] set contract mywaxrngtest mycontracts/rngtest/build/rngtest -p mywaxrngtest@active
```
