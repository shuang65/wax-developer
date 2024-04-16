---
标题: WAX-CDT API
顺序: 25
---

# WAX-CDT API

你所有的智能合约都继承自 [WAX 合约开发工具包 (WAX-CDT)](/build/dapp-development/wax-cdt/)库中的 C++ API 文件。 这些文件用于定义你的智能合约的操作、结构和数据类型。  

这个智能合约的 API 可以分为三个关键模块：

* **合约:** 这是主要用于与 WAX  链通信的 C++ 合约 API。这个库定义了操作、调度器、权限等内容。 
* **核心:** 这个库处理数据流，  **name** 数据类型， 序列化对象等。 
* **数据类型:** 这个库定义了基础合约、数据布局、数据结构等内容。 

所有这些库都在 **wax-cdt/libraries/eosiolib** 文件夹里。只要在智能合约里加上  **<eosio/eosio.hpp>** 大部分功能就可以用了。建议查看这些文件，帮助您了解智能合约的构建方式。

## WAX API 的重载和自定义 

### 方法名称： verify_rsa_sha256_sig

**源代码：** <a href="https://github.com/worldwide-asset-exchange/wax-cdt/blob/master/libraries/eosiolib/core/eosio/crypto.hpp#L283" target="_blank">WAX GitHub 代码库</a>

**描述：** 使用 RSA 256 算法验证签名。这个方法采用原生代码实现，比标准的 WASM 验证快大约 15 倍。详细信息请参考 <a href="https://www.emc.com/collateral/white-papers/h11300-pkcs-1v2-2-rsa-cryptography-standard-wp.pdf" target="_blank">RSA 加密标准</a>。

**输入参数：**

| 参数 | 描述
| --- | -------------------------- |
| 信息 | 要验证的信息内容。 |
| 信息长度 | 信息缓冲区的长度。 |
| 签名 | 签名为十六进制字符串。 |
| 指数 |公钥指数的十六进制字符串。 |
| 系数  |系数以十六进制字符串表示（不允许有前导零）。 |

**示例用法** 这个方法用于我们的 WAX RNG 服务，用于验证从 WAX RNG oracle 返回的 RSA 签名（随机值）是否有效。

```
 eosio_assert(verify_rsa_sha256_sig(&signing_value, sizeof(signing_value), 
    random_value, pub_key->exponent, pub_key->modulus),
    "Could not verify signature.");
```


**返回值：** 布尔值。如果验证成功，则为 True；如果失败，则为 False。

## 数据类型

布尔值。如果验证成功，则为 True；如果失败，则为 False。

* bool
* string
* int8
* int16
* int32
* int64
* int128
* uint8
* uint16
* uint32
* uint64
* uint128
* varint32
* varuint32
* float32
* float64
* float128
* time_point
* time_point_sec
* block_timestamp_type
* bytes
* checksum160
* checksum256
* checksum512
* name
* public_key
* private_key
* signature
* symbol
* symbol_code
* asset

Refer to EOSIO's <a href="https://eosio.github.io/eosio.cdt/1.6.0/group__types.html" target="_blank">Types</a> for more information.

## Type Definitions

WAX-CDT also includes a custom library of type definitions:

* typedef uint64_t account_name;
* typedef uint64_t action_name;
* typedef uint64_t permission_name;
* typedef uint64_t scope_name;
* typedef uint64_t table_name;
* typedef uint32_t time;
* typedef uint16_t weight_type;
* typedef struct checksum256 transaction_id_type;
* typedef struct checksum256 block_id_type;

## Additional Information

For a complete list of features available from the smart contract C++ API, refer to EOSIO's <a href="https://eosio.github.io/eosio.cdt" target="_blank">C/C++ API</a>.
