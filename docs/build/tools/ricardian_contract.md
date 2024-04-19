---
标题: Ricardian 合约
顺序: 111
---

# Ricardian 合约

Ricardian合约是一种可供机器和人类阅读的数字协议，用于约定两方之间的关系（例如，您的应用程序和客户）。与标准法律文件类似，它包含您智能合约的操作、意图、条款和条件。 

Ricardian合约是针对每个操作定义的。每当您的智能合约的操作在WAX链上执行时，这个协议会被加密签名，并且通过哈希（每个操作）进行验证。 

要将Ricardian合约与每个操作关联起来，您需要创建一个Markdown文件。 

* 该文件的名称必须与您的智能合约相同。例如，如果您的智能合约名为 **wax.cpp**，则您的Ricardian Markdown文件必须命名为：wax.contracts.md。
* 每个 **```<h1>```** 标签必须具有 "contract" 类： ```<h1 class="contract"></h1>```。
*要将Markdown文件与操作关联， **```<h1>```** 标签的内容必须与操作名称匹配： ```<h1 class="contract">hi</h1>```。

存储Ricardian Markdown文件的位置与您如何编译智能合约有关。

## 使用 WAX-CDT

如果您使用 **eosio-init** 创建智能合约模板，它会在您的项目目录下自动创建一个文件夹（例如，wax/ricardian），里面包含一个示例的Ricardian合约：wax.contracts.md。

CMake脚本会自动包含 **ricardian** 目录中列出的文件。

请参阅[创建智能合约](/build/dapp-development/wax-cdt/cdt_use)以获取更多信息。

## 使用 eosio-cpp

如果您使用 [eosio-cpp](/build/dapp-development/wax-cdt/)来编译合约， 那么您的Ricardian markdown 文件必须与 wax.cpp文件在同一目录，并且文件名必须相同：wax.contracts.md。

```shell
eosio-cpp -abigen wax.cpp -o wax.wasm
```

##  Ricardian 合约示例

下面是一个智能合约，其中包含一个名为：**hi**的操作。

```cpp
ACTION wax::hi( name nm ) {
   /* fill in action body */
   print_f("Name : %\n",nm);
}
```

要将Ricardian合约与此操作关联：

1.创建一个名为 **your-contract.contracts.md** 的文件（例如，wax.contracts.md）。
2. 请将下面的Markdown内容复制粘贴到您的合约文件中。

:::提示
对于您的每个操作，请使用带有"contract"类的 ```<h1>``` 标签， 并将其内部内容设置为操作名称。
:::

```html
<h1 class="contract"> hi </h1> 
```

hi操作的Ricardian合约模板
