---
标题: 访问本地 API
顺序: 42
---

# 访问本地 API

WAX主网提供了一组 **nodeos** API 端点 (RPC API)， 允许您与 WAX 链进行交互。这些端点通常被称为 [chain-api-url](/operate/wax-infrastructure/#public-and-free-api-service-providers) 。


当您在本地开发服务器上运行一个本地节点时，您可以通过本地 IP 地址: `http://127.0.0.1:8888`访问这些端点。 这个 API 端点是在您向 **nodeos**传递 `plugin eosio 传递 chain_api_plugin`参数时初始化的。

测试本地 RPC API，请在命令行中使用 **curl**向 `get_info` 端点发出请求:

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_info \
  --header 'content-type: application/x-www-form-urlencoded; charset=UTF-8'
```

您应该会收到以下 JSON 响应：

```
{
   "server_version":"448287d5",
   "chain_id":"cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f",
   "head_block_num":1937,
   "last_irreversible_block_num":1936,
   "last_irreversible_block_id":"000007905e94a4406ef34a227cf815154ac6886bf54deaa2d35db606cb4b667d",
   "head_block_id":"00000791a899e1751e60a13b77817f7243496cdd68010cd84505023200fd9e8a",
   "head_block_time":"2019-07-16T21:43:19.500",
   "head_block_producer":"eosio",
   "virtual_block_cpu_limit":1384557,
   "virtual_block_net_limit":7271761,
   "block_cpu_limit":199900,
   "block_net_limit":1048576,
   "server_version_string":"v1.7.3"
}
```

:::提示
请注意 "head_block_producer":"eosio" 参数。 在本地， <strong>eosio</strong> 是系统账户。 如果您向 WAX 主网 API 发出请求，它会返回一个实际的区块生产者 (例如， "head_block_producer": "strongblock1").
:::

要调用此端点，**nodeos**  必须正在运行。否则，您将收到以下消息：

```
curl: (7) Failed to connect to 127.0.0.1 port 8888: Connection refused
```

## 附加信息

请参考 [WAX RPC API](/build/api-reference/rpc_api) 获取更多信息。
