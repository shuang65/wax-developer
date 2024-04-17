---
标题: 启动本地节点
顺序: 41
---

# 启动本地节点

要在开发服务器上启动本地 WAX 节点，您可以按照以下步骤进行操作：

1.  命令行中输入以下命令来初始化 **keosd**。

```shell
keosd &
```

控制台将输出以下信息：

```shell
info  2019-07-16T21:22:39.501 thread-0  wallet_plugin.cpp:42          plugin_initialize    ] initializing wallet plugin
info  2019-07-16T21:22:39.513 thread-0  http_plugin.cpp:622           add_handler          ] add api url: /v1/keosd/stop
info  2019-07-16T21:22:39.519 thread-0  http_plugin.cpp:622           add_handler          ] add api url: /v1/node/get_supported_apis
info  2019-07-16T21:22:39.520 thread-0  wallet_api_plugin.cpp:73      plugin_startup       ] starting wallet_api_plugin
info  2019-07-16T21:22:39.521 thread-0  http_plugin.cpp:622           add_handler          ] add api url: /v1/wallet/create
info  2019-07-16T21:22:39.523 thread-0  http_plugin.cpp:622           add_handler          ] add api url: /v1/wallet/create_key
info  2019-07-16T21:22:39.525 thread-0  http_plugin.cpp:622           add_handler          ] add api url: /v1/wallet/get_public_keys
info  2019-07-16T21:22:39.527 thread-0  http_plugin.cpp:622           add_handler          ] add api url: /v1/wallet/import_key
info  2019-07-16T21:22:39.544 thread-0  http_plugin.cpp:622           add_handler          ] add api url: /v1/wallet/list_keys
info  2019-07-16T21:22:39.546 thread-0  http_plugin.cpp:622           add_handler          ] add api url: /v1/wallet/list_wallets
info  2019-07-16T21:22:39.549 thread-0  http_plugin.cpp:622           add_handler          ] add api url: /v1/wallet/lock
info  2019-07-16T21:22:39.552 thread-0  http_plugin.cpp:622           add_handler          ] add api url: /v1/wallet/lock_all
info  2019-07-16T21:22:39.555 thread-0  http_plugin.cpp:622           add_handler          ] add api url: /v1/wallet/open
info  2019-07-16T21:22:39.558 thread-0  http_plugin.cpp:622           add_handler          ] add api url: /v1/wallet/remove_key
info  2019-07-16T21:22:39.561 thread-0  http_plugin.cpp:622           add_handler          ] add api url: /v1/wallet/set_timeout
info  2019-07-16T21:22:39.563 thread-0  http_plugin.cpp:622           add_handler          ] add api url: /v1/wallet/sign_digest
info  2019-07-16T21:22:39.565 thread-0  http_plugin.cpp:622           add_handler          ] add api url: /v1/wallet/sign_transaction
info  2019-07-16T21:22:39.567 thread-0  http_plugin.cpp:622           add_handler          ] add api url: /v1/wallet/unlock
```

2.接下来，将以下内容粘贴到命令行以开始生成区块：

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

这将初始化所有基本插件，设置服务器地址（您的），并添加合约调试和日志记录功能。 


:::警告
重要提示: --access-control-allow-origin='*' 参数启用了跨源资源共享（CORS）。绝对不要在公共节点上启用此选项。     
:::

可以更加优化吗？方便更好理解

```shell
[2] 4529.
```

3. 验证 **nodeos** 是否正在生产区块，请在命令行中使用 **tail** 令查看日志：

```shell
tail -f nodeos.log
```

控制台会输出您的区块信息：

```shell
info  2019-07-16T21:36:14.501 thread-0  producer_plugin.cpp:1597      produce_block        ] Produced block 0000043f8f7c37a1... #1087 @ 2019-07-16T21:36:14.500 signed by eosio [trxs: 0, lib: 1086, confirmed: 0]
info  2019-07-16T21:36:15.001 thread-0  producer_plugin.cpp:1597      produce_block        ] Produced block 00000440315e6c27... #1088 @ 2019-07-16T21:36:15.000 signed by eosio [trxs: 0, lib: 1087, confirmed: 0]
```


:::提示
请注意 "signed by eosio" 签名 - 这是本地系统账户。
:::

您现在在开发服务器上运行了一个本地 WAX 节点。按下 Ctrl + c 可以关闭日志 (**nodeos** 会继续在后台运行)。

## 停止本地节点

停止 **nodeos**:

1. 在命令行中，运行 `pkill`:

```shell
pkill nodeos
```

2. 要验证 **nodeos** 是否不再生成区块，请运行 `tail` 命令查看日志：

```shell
tail -f nodeos.log
```

在最后一行，控制台会输出： "nodeos 成功登出"。

```shell
info  2019-07-16T21:45:43.501 thread-0  producer_plugin.cpp:1597      produce_block        ] Produced block 000008b10f51d1ae... #2225 @ 2019-07-16T21:45:43.500 signed by eosio [trxs: 0, lib: 2224, confirmed: 0]
info  2019-07-16T21:45:44.001 thread-0  producer_plugin.cpp:1597      produce_block        ] Produced block 000008b26fca2675... #2226 @ 2019-07-16T21:45:44.000 signed by eosio [trxs: 0, lib: 2225, confirmed: 0]
info  2019-07-16T21:45:44.450 thread-0  main.cpp:148                  main                 ] nodeos successfully exiting
```



