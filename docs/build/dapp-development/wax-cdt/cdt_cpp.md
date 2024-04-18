---
标题: WAX-CDT 开发工具
顺序: 53
---

# WAX-CDT 开发工具

WAX-CDT 包含了各种<a href="https://clang.llvm.org/" target="_blank">Clang</a>前端和工具基础架构构建的 **eosio**命令。这个集合包括了多种工具，用于构建优化、高性能的WASM文件。有关更多信息，请参阅 [WAX-CDT Options](/build/tools/cdt_选项) 。

建议您使用 **eosio-init** 去 [创建智能合约](/build/dapp-development/wax-cdt/cdt_use.html#compile-hello-world)。这个工具提供了脚本，可以轻松组织和开发您的项目。 

如果这些脚本不符合您的需求，还可以使用 **eosi-cpp** 来编译智能合约。

## 使用 eosio-cpp

要为您的智能合约生成WASM和ABI文件：

1. 命令行中导航至智能合约文件夹

2. 运行 **eosio-cpp** 构建命令， 并使用 **-abigen** 参数。

:::提示
<strong>eosio-cpp</strong> 还会在 ABI 文件中包含Ricardian条款。可以查看 [Ricardian Contracts](/build/tools/ricardian_contract) 和 [Ricardian Clauses](/build/tools/ricardian_clause) 获取更多信息。
:::

```
eosio-cpp -abigen wax.cpp -o wax.wasm
```

将在合约目录中生成两个文件

* 编译后的二进制WASM文件 (wax.wasm)
* 生成的 ABI 文件 (wax.abi)

<!--## Use eosio-abigen to Generate an ABI

如果您只想生成一个ABI文件，可以使用 **eosio-abigen** 命令完成。 

要使用**eosio-abigen**， 请包含以下参数：

- 您合约的 C++ 文件名
- --contract (合约名称)
- --output (ABI文件名)

### 示例

```
eosio-abigen hello.cpp --contract=hello --output=hello.abi
```-->




