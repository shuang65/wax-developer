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

    a. Type your contract name on line 25.
    ```shell
    project(waxcontract)
    ```

    b. Type your contract's filename on line 29.

    ```shell
    add_contract(${PROJECT_NAME} ${PROJECT_NAME} waxcontract.cpp)
    ```

    Save the file. 

5. 然后， 打开 **Makefile**。这个文件包含运行 `cleos` 和WAX Docker开发镜像的脚本。

    a. Type your contract name on Line 23.
    ```shell
    CONTRACT_NAME = waxcontract
    ```

    b. Update the WAX allocations for your smart contract on Line 87, if required.
    ```shell
    --stake-net '0.50000000 WAX' --stake-cpu '0.50000000 WAX' --buy-ram-kbytes 32"
    ```

    c. To test your smart contract, you can update line 48 to run your action:

    ```shell
    push action ${CONTRACT_ACCOUNT} greet '[]' -p ${CONTRACT_ACCOUNT}@active"
    ```

    Save the file.

:::提示
`NODEOS_URL` 是唯一的可选参数。 默认情况下是主网部署地址 [chain-api-url](/operate/wax-infrastructure/#public-and-free-api-service-providers/.  
:::

Once these changes have been made, you're ready to use the `make` scripts to build and deploy your smart contract.

## Deploy Your Smart Contract

To launch your WAX smart contract on the WAX Blockchain:

1. **Build your smart contract.** In the command line, run the following script from the **wax_deploy** folder:

    ```shell
    make build
    ```

    This creates `wax.wasm` and `wax.abi` in the **wax_deploy** folder.

2. **Generate keys for your smart contract's account.** From the command line, run:

    ```shell
    make create-key
    ```

    This creates a pair of private/public keys for your smart contract's account (save the console response in a safe place, you'll need to use them later).

4. **Create a WAX Contract Account.** To create a blockchain account for your smart contract, run:

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

5. **Deploy your contract.** From the command line, run: 

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

5. **Test your smart contract.** From the command line, run:

    ```shell
    make test CONTRACT_ACCOUNT=waxsc1
    ```

Your dApp is now live on WAX! 

:::tip
Depending on how your dApp's onboarding process is built, your customers may need to create a WAX Account to use your dApp on WAX.
:::

