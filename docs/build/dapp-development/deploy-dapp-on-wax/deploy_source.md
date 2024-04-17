---
标题: 部署WAX-CDT 
顺序: 73
---

# 部署WAX-CDT 

在本指南中， 您将使用 `cleos set contract` 命令将您的智能合约部署到WAX主网。

开始之前， 您需要编译您的智能合约，并准备好您的WASM和ABI文件。有关更多信息，请参阅 [智能合约快速入门](/build/dapp-development/smart-contract-quickstart/)或 [WAX-CDT 构建 工具](/build/dapp-development/wax-cdt/cdt_cpp) 。

您还需要：

* 确保您已经创建了一个自主管理的WAX链账户。 
* 确保您的账户中有足够的WAX去抵押来分配资源。 

要将您的智能合约部署到WAX主网：

1. 打开并解锁您的钱包。 

    ```shell
    cleos wallet open -n mywallet && cleos wallet unlock -n mywallet --password {wallet.pwd}
    ```

2. 生成一对公钥/私钥对，用于创建您的智能合约的账户。从命令行使用 `cleos create key` 命令：

    ```shell
    cleos wallet create_key -n mywallet
    ```

:::注意
您也可以使用 EOSIO 兼容的钱包 (例如， Scatter)。
:::

3. 要创建您的智能合约账户，请在命令行中使用 `cleos system newaccount` 命令。 运行此命令时，您需要具有适当的权限，这意味着您的主账户所在的钱包必须打开并解锁。 

    <table>
    <thead>
    <tr>
    <th style="width: 25%">参数</th>
    <th>示例</th>
    <th>描述</th>
    </tr>
    </thead>

    <tbody>
    <tr>
    <td>-u</td>
    <td>-u <a href="/operate/wax-infrastructure/#public-and-free-api-service-providers">chain-api-url</a></td>
    <td>This is the WAX Blockchain URL.</td>
    </tr>

    <tr>
    <td>system</td>
    <td>system</td>
    <td>Sends the system contract action to the WAX Blockchain.</td>
    </tr>

    <tr>
    <td>newaccount</td>
    <td>newaccount</td>
    <td>Command to create a new account.</td>
    </tr>

    <tr>
    <td>primaryAccount</td>
    <td>waxdappacct1</td>
    <td>Your self-managed WAX Blockchain Account with staked WAX tokens.</td>
    </tr>

    <tr>
    <td>contractAccount</td>
    <td>HelloWorld10</td>
    <td>Name of your smart contract's account. Exactly 12 characters from (a-z1-5).</td>
    </tr>

    <tr>
    <td>newPublicKey</td>
    <td>EOS7jEb46pDiWvA39faCoFn3jUdn6LfL51irdXbvfpuSko86iNU5x</td>
    <td>This is the public key you created in Step 1.</td>
    </tr>

    <tr>
    <td>stake-net</td>
    <td>--stake-net '0.50000000 WAX'</td>
    <td>Amount of WAX to stake for NET.</td>
    </tr>

    <tr>
    <td>stake-cpu</td>
    <td>--stake-cpu '0.50000000 WAX'</td>
    <td>Amount of WAX to allocate for CPU.</td>
    </tr>

    <tr>
    <td>buy-ram-kbytes</td>
    <td>--buy-ram-kbytes 32</td>
    <td>Amount of RAM to allocate.</td>
    </tr>
    </tbody>
    </table>

    ### 示例
    ```shell
    cleos -u chain-api-url system newaccount waxdappacct1 HelloWorld10 EOS7jEb46pDiWvA39faCoFn3jUdn6LfL51irdXbvfpuSko86iNU5x --stake-net '0.50000000 WAX' --stake-cpu '0.50000000 WAX' --buy-ram-kbytes 32
    ```

:::注意
每个合约都需要您重复执行第1步和第2步。 
:::

4. **部署.** F命令行中，使用 `cleos set contract` 设置您的合约： 

    | 参数 | 示例 | 描述
    | --- | ----------- | -------------------------- |
    | -u | -u [chain-api-url](/operate/wax-infrastructure/#public-and-free-api-service-providers/)| This is the WAX Blockchain URL. |
    | contractAccount| HelloWorld10 | Your smart contract's account (created in Step 2). |
    | fullPath | d/wax-blockchain/wax-cdt/mycontracts/wax/build | The full path to your WASM and ABI files. |
    | wasmName | wax | Name of your WASM file. |
    | abiName | wax | Name of your ABI file. |

    ```shell
    cleos -u chain-api-url set contract HelloWorld10 d/wax-blockchain/wax-cdt/mycontracts/wax/build wax.wasm wax.abi
    ```

您的dApp现在已经在WAX上上线啦！ 

:::注意
根据您的dApp的注册流程，您的客户可能需要在WAX上创建一个WAX账户才能使用您的dApp。
:::
