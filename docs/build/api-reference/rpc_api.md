---
标题: WAX-RPC API
顺序: 20
---

# WAX-RPC API

WAX链RPC API提供了公共端点，可用于获取区块信息、区块历史、节点信息以及节点生产者信息。这些端点通过 **nodeos** 插件提供，在WAX主网和本地开发环境中均可使用。

:::提示
如果您正在进行本地请求， 则必须运行<strong>nodeos</strong>。
:::


|环境 | URL |
| --- | ----------- |
| WAX 主网 | 在[https://validate.eosnation.io/wax/reports/endpoints.html](https://validate.eosnation.io/wax/reports/endpoints.html) 检查节点可用性|
| 本地测试网 | http://127.0.0.1:8888 |

您可以直接向区块链端点发出API请求：

```
curl --request POST \
  --url http://127.0.0.1:8888/v1/chain/get_info \
  --header 'content-type: application/x-www-form-urlencoded; charset=UTF-8'
```

您还可以使用 **cleos** 命令调用这些端点：

```
cleos -u [api-url] get info
```

## 附加信息和第三方工具

请参阅 <a href="https://docs.eosnetwork.com/leap/latest/nodeos/rpc_apis/" target="_blank">RPC API 文档 </a> 获取API调用列表。

<a href="https://github.com/eosnetworkfoundation/mandel-eosjs" target="_blank">eosjs</a> 是一个 JavaScript API SDK，用于与 WAX RPC API 进行简单通信。为了简化开发，您可以使用这个工具来访问区块链端点。
