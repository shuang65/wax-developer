---
标题: 创建一个智能合约
顺序: 62
---

# 创建一个智能合约

在这节中， 您会学到如何用 **eosio-init**写并编译一个 WAX 的智能合约。

## 如何工作的

**eosio-init** 是一个WAX-CDT 工具， 它会创建以下智能合约模板/目录结构：

- **include** 文件夹： 这里包含一个 **.hpp** 文件样例。
- **ricardian** 文件夹： 这里有一个Ricardian智能合约中markdown文件的示例。
- **src**文件夹： 这里有一个 **.cpp** 智能合约文件样例。

模板文件的名字会根据您在命令行中使用 **eosio-init** 时指定的项目名称来命名。 

## 使用 eosio-init

使用 **eosio-init**来创建您的第一个WAX智能合约：

1. 新建一个智能合约文件夹。在这个教程中，我们将使用一个名为 **mycontracts**的文件夹。

    ```shell
    mkdir mycontracts
    ```shell
    Navigate to this new directory:
    ```shell
    cd mycontracts
    ```

2. 命令中，使用 **eosio-init** 并带上 `-project` 参数。

    ```
    eosio-init -project wax
    ```

    **eosio-init** 使用 `-project` 参数来创建以下目录结构：
   
    - mycontracts/wax/include 
    - mycontracts/wax/ricardian 
    - mycontracts/wax/src 

4. 可选的。 添加 [Ricardian Clause](/build/tools/ricardian_clause)。 默认情况下已经有 [Ricardian Contract](/build/tools/ricardian_contract) 了。

您现在已经有一个智能合约模板了，其中包含一个样例智能合约文件 (mycontracts/wax/src/wax.cpp)。 该合约包含以下操作：

```
#include <wax.hpp>
ACTION wax::hi( name nm ) {
   /* fill in action body */
   print_f("Name : %\n",nm);
}
```

头文件 (mycontracts/wax/include/wax.hpp) 来自 **<eosio/eosio.hpp>**.

```
// Inherit your contract from eosio::contract. 
// This exposes the following data types (available to your smart contract):
// eosio::name receiver - the contract that receives an action (this contract)
// eosio::name code - the contract's blockchain account
// eosio::datastream - the data that's passed to the contract. In this example, it's  your name.
#include <eosio/eosio.hpp>
using namespace eosio;

CONTRACT wax : public contract {
   public:
      using contract::contract;

      // The ACTION keyword implements the behavior of your contract. 
      // ACTION is a shortcut for [[eosio::action]]  
      ACTION hi( name nm );

      //action_wrapper: first parameter = action to call
      //second parameter = pointer to the action function
      using hi_action = action_wrapper<"hi"_n, &wax::hi>;
};
```
:::提示
action_wrapper结构创建了一个基于特定操作的模板/指针。您可以使用 action_wrapper 来从一个合约调用另一个合约的操作。
:::


## 编译智能合约
要部署智能合约，您需要创建一个 `.wasm` 文件和 `.abi` 文件，您可以使用 WAX 合约开发工具包 (WAX-CDT)来完成。

1. 安装 [WAX-CDT](/build/dapp-development/wax-cdt/) (如果你还没有安装)。

2. 命令行中， 切换到 **mycontracts/wax** 的构建文件夹。

    ```shell
    cd wax/build
    ```

3. 使用 cmake 初始化，将重要的构建文件写入 **build** 目录。

    ```shell
    cmake ..
    ```

    控制台会输出以下构建任务：

    ```shell
    -- The C compiler identification is GNU 7.4.0
    -- The CXX compiler identification is GNU 7.4.0
    -- Check for working C compiler: /usr/bin/cc
    -- Check for working C compiler: /usr/bin/cc -- works
    -- Detecting C compiler ABI info
    -- Detecting C compiler ABI info - done
    ...
    -- Build files have been written to: waxblockchain/wax-blockchain/wax-cdt/examples/hello/build
    ```

4. 构建脚本。

    ```shell
    make
    ```

    控制台将会输出以下信息：
    ```shell
    Scanning dependencies of target wax
    [ 50%] Building CXX object CMakeFiles/wax.dir/wax.obj
    Warning, empty ricardian clause file
    [100%] Linking CXX executable wax.wasm
    [100%] Built target wax
    [ 77%] No install step for 'wax_project'
    [ 88%] No test step for 'wax_project'
    [100%] Completed 'wax_project'
    [100%] Built target wax_project
    ```

您可以在**build/wax**目录中找到 **wax.wasm** 文件和 **wax.abi** 文件。 

