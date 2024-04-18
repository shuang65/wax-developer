---
标题: 智能合约基础
顺序: 61
---

# 智能合约基础

WAX 智能合约包括一系列的操作、类型定义和持久化存储，使得您的 dApp 能够在 WAX 区块链上签署交易。当您从前端应用程序调用一个智能合约时：

- 一个操作（ACTION）被初始化
- 信息被推送至WAX主网
- 操作完成后，继续执行下一个操作（如果需要）

## 如何工作的

智能合约通常包括头文件、类继承、操作、权限、持久化数据、操作分发器和类型定义。

### 头文件

C++ 头文件包含全局声明。因为 WAX 使用的是EOS 的分叉版本（Antelope），所有 WAX 智能合约都将继承自 EOS 的合约和类。 每个合约必须包含 <a href="https://github.com/worldwide-asset-exchange/wax-cdt/blob/master/libraries/eosiolib/eosio.hpp" target="_blank">eosio.hpp</a> 头文件， 并且每个合约都继承自 <a href="https://github.com/worldwide-asset-exchange/wax-cdt/blob/master/libraries/eosiolib/contract.hpp" target="_blank">eosio::contract</a> 类。

```
  #include <eosio/eosio.hpp>
```

这样可以让您的智能合约使用 WAX 的 C/C++ API，从而定义操作和结构，使得您的智能合约能够与 WAX 链进行通信。详细信息请参考 [WAX-CDT API](/build/api-reference/cdt_api) 。

### Actions

Actions定义了智能合约的核心功能。当一个Action执行时，事件将被写入到 WAX 链。

Actions 包含以下属性：

- **权限等级:**  您可以为每个操作设置不同的权限。
- **代码:** 这是您智能合约的账户。
- **Action:** action的名称。
- **数据:** Actions 支持各种数据类型和数据结构。
  
#### 交易

一笔交易是指在同一个区块中执行的一个或多个操作的列表。

Actions 在一个独立的代码块中运行，通常从您的前端客户端调用。如果您的某个Actions需要调用另一个Actions，您可以创建一个智能合约 **Transaction**。

交易使用两种模型进行通信：内联（inline）和延迟（deferred）。

- **内联（Inline）:** 内联交易是一种类似于同步通信的模型，它在同一事务范围内执行。这些操作保证按顺序执行，并且在调用原始操作时同时执行。如果交易失败，您可以撤销之前操作所做的更改。

  要更多了解内联交易的示例，请参考 EOS Network 的指南 <a href="https://docs.eosnetwork.com/docs/latest/" target="_blank">添加内联操作</a>。

- **延迟:** 延迟操作是指计划在未来执行的操作，类似于异步调用。这些交易不保证一定会被执行（有可能会被节点丢弃）。当操作运行时，原始（调用）操作将被应用到 WAX 区块链上，并且如果延迟交易失败，则无法撤销原始操作。

:::警告
从 Leap 3.1 开始，已不再使用延迟交易。
:::

### 权限

智能合约和 WAX 链账户之间将通过您的智能合约中定义的操作进行通信。可以使用 WAX 账户权限来保护您的操作。通过在您的操作中包含 `require_auth()` 的方法，可以验证一个操作调用是否由您的智能合约账户发起。也可以使用 `require_auth()` 方法来保护 WAX 用户特定的操作，比如更新用户记录。要求用户在特定操作上进行身份验证可以确保只有您的用户能执行此操作。

权限也可以让您的智能合约处理通知，并使用 `eosio.code` 权限来调用其他智能合约的操作。

查看 EOS Network的指南 <a href="https://docs.eosnetwork.com/docs/latest/" target="_blank">Accounts and Permissions</a> 获取更多信息。

### 保留数据


每当您在应用程序中调用智能合约的一个功能时，就会新建一个智能合约的实例。这个新的实例并不知道之前的合约状态。当这个功能完成时，这个实例也就不再存在了。

要在一个或多个智能合约的操作之间保留数据， 您需要使用 **multi_index** 表功能。

:::提示 📝 注意	
持久化数据存储在 WAX 节点的 RAM 中，会影响您需要抵押到智能合约中的 WAX 数量。
:::

更多请参考 EOS Network的指南 <a href="https://docs.eosnetwork.com/docs/latest/" target="_blank">Data Persistence</a> 获取更多信息。

### WAX 分发器

分发器宏是一个操作处理器，用于监听传入的请求。可以使用这个宏来注册智能合约中的所有操作。

### 基本结构

这是一个典型的智能合约模板示例，包含了常见的元素。

```
#include <eosio/eosio.hpp>

using namespace eosio;

CONTRACT mycontract : public eosio::contract {
public:
	using contract::contract;

	ACTION action1(name user) {
		require_auth(user);
	}

private:
	TABLE customer {
		name key;
		std::string first_name;
		std::string last_name;

		uint64_t primary_key() const { return key.value; }
	};

	typedef eosio::multi_index<"customers"_n, customer> customer_index;

};
EOSIO_DISPATCH(mycontract, (action1))

```
