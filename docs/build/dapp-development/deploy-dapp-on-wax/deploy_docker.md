---
标题: Docker Deploy
顺序: 72
---

# 部署Docker 

在本指南中， 您将学习如何自定义 **hello-world** 的构建脚本，以便将您的智能合约部署到WAX主网。

开始之前:

* 确保 Docker 已配置为无需sudo即可运行。 
* 下载 <a href="https://github.com/worldwide-asset-exchange/wax-blockchain" target="_blank">WAX 链源代码</a>。 更多信息，请参阅 [WAX Blockchain Setup](/build/dapp-development/wax-blockchain-setup/) 。
* 确保您拥有WAX链账户的公钥/私钥。
* 确保您的账户中有足够的WAX抵押来分配资源。 

:::提示
您无需构建WAX源代码即可完成这些步骤。 
:::

## 修改脚本

要修改 **hello-world** 脚本以部署您的智能合约，请按照以下步骤

1. 命令行界面中，导航至 <a href="https://github.com/worldwide-asset-exchange/wax-blockchain" target="_blank">WAX 链源代码库</a>中的**hello-world**文件夹

    ```shell
    cd wax-blockchain/samples/hello-world
    ```

3. 将 **hello-world** 文件夹的内容复制到您智能合约的目录中。 在这个示例中， 我们将使用 **wax_deploy**文件夹。

4. 在 **wax_deploy**文件夹中， 打开 **CMakeLists.txt**。 这个文件存储了您的项目名称和智能合约文件名称。

    a. 在第25行输入您的合约名称。
    ```shell
    project(waxcontract)
    ```

    b. 在第29行输入您的合约文件名。

    ```shell
    add_contract(${PROJECT_NAME} ${PROJECT_NAME} waxcontract.cpp)
    ```

    保存文件。 

5. 然后， 打开 **Makefile**。这个文件包含运行 `cleos` 和WAX Docker开发镜像的脚本。

    a. 在第23行输入您的合约名称。
    ```shell
    CONTRACT_NAME = waxcontract
    ```

    b. 如果需要，您可以在第87行更新您的智能合约的WAX分配。
    ```shell
    --stake-net '0.50000000 WAX' --stake-cpu '0.50000000 WAX' --buy-ram-kbytes 32"
    ```

    c. 要测试您的智能合约，您可以更新第48行以运行您的操作：

    ```shell
    push action ${CONTRACT_ACCOUNT} greet '[]' -p ${CONTRACT_ACCOUNT}@active"
    ```

    保存文件。

:::提示
`NODEOS_URL` 是唯一的可选参数。 默认情况下是主网部署地址 [chain-api-url](/operate/wax-infrastructure/#public-and-free-api-service-providers/.  
:::

完成这些更改后，您就可以使用 `make` 脚本来构建和部署您的智能合约了。

## 部署您的智能合约

要在WAX链上启动您的WAX智能合约：

1. **构建您的智能合约.** 在命令行中， 从 **wax_deploy** 文件夹运行以下脚本:

    ```shell
    make build
    ```

    这将在**wax_deploy**文件夹中创建 `wax.wasm` 和 `wax.abi` 文件。

2. **为您的智能合约生成密钥.** 从命令行运行：

    ```shell
    make create-key
    ```

    这将为您的智能合约账户创建一对私钥/公钥（并将控制台响应保存在安全的地方，您稍后会需要使用它们）。

4. **创建WAX合约账户.** 要为您的智能合约创建一个账户，请运行：

    <table>
    <thead>
    <tr>
    <th style="width: 28%">Parameter</th>
    <th>Example</th>
    <th>Description</th>
    </tr>
    </thead>

    <tbody>
    <tr>
    <td>WAX_ACCOUNT</td>
    <td>waxprimary</td>
    <td>Your dApp Developer Account name.</td>
    </tr>

    <tr>
    <td>WAX_PRIVATE_KEY</td>
    <td>5JTZaN1zabi5wyC3LcdeZG3AzF7sLDX4JFqMDe68ThLC3Q5nYez</td>
    <td>Private key for your dApp Developer Account.</td>
    </tr>

    <tr>
    <td>CONTRACT_ACCOUNT</td>
    <td>waxsc1</td>
    <td>Specify a new name for your smart contract account. Account names must be less than 13 characters and only contain letters [a-z] and numbers [1-5].</td>
    </tr>

    <tr>
    <td>CONTRACT_PUBLIC_KEY</td>
    <td>EOS4yxqE5KYv5XaB2gj6sZTUDiGzKm42KfiRPDCeXWZUsAZZVXk1F</td>
    <td>New public key that you created in Step 2.</td>
    </tr>
    </tbody>
    </table>
 
    ```shell
    make create-account WAX_ACCOUNT=waxprimary WAX_PRIVATE_KEY=5JTZaN1zabi5wyC3LcdeZG3AzF7sLDX4JFqMDe68ThLC3Q5nYez CONTRACT_ACCOUNT=waxsc1 CONTRACT_PUBLIC_KEY=EOS4yxqE5KYv5XaB2gj6sZTUDiGzKm42KfiRPDCeXWZUsAZZVXk1F
    ```

5. **部署到您的合约.** 从命令行运行: 

    <table>
    <thead>
    <tr>
    <th style="width: 28%">Parameter</th>
    <th>Example</th>
    <th>Description</th>
    </tr>
    </thead>

    <tbody>
    <tr>
    <td>CONTRACT_ACCOUNT</td>
    <td>waxsc1</td>
    <td>The name you specified for your smart contract's account.</td>
    </tr>

    <tr>
    <td>CONTRACT_PRIVATE_KEY</td>
    <td>9X5KRXKVx25yjL3FvxxY9YxYxxYY9Yxx99yyXTRH8DjppKpD9tKtVz</td>
    <td>Private key for your smart contract's account (that you created in Step 2).</td>
    </tr>
    </tbody>
    </table>

    ```shell
    make deploy CONTRACT_ACCOUNT=waxsc1 CONTRACT_PRIVATE_KEY=9X5KRXKVx25yjL3FvxxY9YxYxxYY9Yxx99yyXTRH8DjppKpD9tKtVz
    ```

    This deploys your smart contract to the mainnet. You only need to pass your smart contract's account name and private key.

5. **测试您的智能合约.** 从命令行运行:

    ```shell
    make test CONTRACT_ACCOUNT=waxsc1
    ```

您的dApp现在已经在WAX上成功上线啦！ 

:::注意
根据您的dApp的注册流程，您的用户可能需要创建一个WAX账户才能在WAX上使用您的dApp。
:::

