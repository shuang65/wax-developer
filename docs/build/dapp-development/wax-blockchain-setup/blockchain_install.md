---
标题: 安装 WAX 链
顺序: 31
---

# 安装 WAX 链

将GitHub上的WAX链源代码存储库会下载到 **wax-blockchain** 目录中。下载和构建过程可能需要几分钟到几个小时不等，这取决于您的网络、操作系统和硬件规格。

要下载WAX链源代码存储库：

1. 在命令行中，使用Git克隆存储库
    ```shell
    git clone https://github.com/worldwide-asset-exchange/wax-blockchain.git
    ```

2. 切换到 **wax-blockchain**目录。

    ```shell
    cd wax-blockchain
    ```

3. 更新 Git 子模块。

    ```shell
    git submodule update --init --recursive
    ```

## 构建WAX链

如果您正在使用我们的Docker镜像， 则 **无需** 完成这些步骤。

要从源代码上构建WAX链，可以使用以下步骤。如果已经安装了先前的版本，您需要先卸载它。请参考[卸载 WAX](/build/dapp-development/wax-blockchain-setup/blockchain_uninstall) for 获取更多信息。

:::警告
重要： 如果您在构建过程中遇到问题，请参考 [已知问题](/build/troubleshooting/) 。建议使用 [Docker 镜像](/build/dapp-development/docker-setup/) ，但不支持从源代码构建。 
:::

1. 执行构建脚本，并设置安装目录。 

    ```shell
    ./wax_build.sh -i ~/wax-blockchain
    ```

:::提示
会安装到 [区块链工具](/build/tools/blockchain_tools) to the <strong>wax-blockchain/bin</strong> 目录中。
:::

2. 将WAX安装到您在第4步中设置的目录中。
    ```shell
    ./wax_install.sh
    ```

3. 可选。 将区块链工具目录添加至您的环境变量中。

    ```shell
    echo "export PATH=~/wax-blockchain/bin:$PATH" >> ~/.bashrc && source ~/.bashrc
    ```







