---
标题: 在WAX上部署您的dApp
顺序: 70
---

# 在WAX上部署您的dApp

要在WAX上部署您的dApp，您需要使用 [WAX-CDT](/build/dapp-development/wax-cdt/)and [区块链工具](/build/tools/blockchain_tools)，进行以下操作:

- 编译您的智能合约
- 为每个合约创建一个WAX账户
- 部署您的智能合约到WAX链

WAX提供两种部署方式。您可以使用我们的自定义 **make** 脚本 (适合 EOS 开发者) ，也可以在本地Docker容器或安装中使用WAX-CDT工具。下面是各种方式的优势和要求。

## 自定义部署脚本

 WAX源代码存储库中有一个名为<a href="https://github.com/worldwide-asset-exchange/wax-blockchain" target="_blank">WAX 源代码存储库</a>  **hello-world** 的示例合约， 还包含了 **make** 脚本， 可以方便自动化地构建和部署智能合约。这些脚本使用WAX Docker开发镜像来完成：

- 生成WASM和ABI文件
- 为您的智能合约创建一个WAX链账户
- 将您的智能合约部署到WAX
- 在WAX链上测试您的智能合约

### 优势

- 您可以通过Docker容器部署智能合约，无需安装WAX源代码。（您只需从 <a href="https://github.com/worldwide-asset-exchange/wax-blockchain" target="_blank">WAX 源代码存储库下载</a> **hello-world**源代码和脚本即可)。
- 您可以直接在智能合约的目录中运行可定制的 **make** 脚本，而无需提供WASM和ABI文件的路径。

### 你需要准备什么：

- Docker 必须已安装并配置为无需 sudo 权限运行。Linux 用户，请参考 <a href="https://docs.docker.com/install/linux/linux-postinstall/" target="_blank">Linux后续安装步骤 
 </a> 获取更多信息。

  :::注意
  <strong>Windows Subsystem for Linux 用户:</strong> Docker 的配置和安装要求会根据你的 WSL 版本而变化。仅建议高级 Docker/Windows 用户使用。如果你正在使用 WSL 2，请参考  <a href="https://docs.docker.com/docker-for-windows/wsl-tech-preview/" target="_blank">Docker Desktop WSL 2 Tech Preview</a> 获取更多信息。
  :::

- make (VERSION 3.9 +)
- 一个自主管理的WAX链账户及其私钥（用于合约部署）。
  
## 部署Docker (WAX-CDT)


当然，您可以使用WAX-CDT工具从命令行轻松部署您的智能合约。


### 优势

- 这种方法让您可以更灵活地控制构建和部署过程中的参数。详细了解 [WAX-CDT 选项](/build/tools/cdt_options)。
- 如果您使用 **eosio-init** 来 [创建智能合约](/build/dapp-development/wax-cdt/cdt_use.html#compile-hello-world/)并部署到本地区块链，那么这可能是一个不错的选择。
- 兼容 Windows 用户。

### 你需要准备什么：
当使用这个选项时，您需要：

- 完成我们的 [Docker 快速入门](/build/dapp-development/docker-setup/)(推荐) 或者使用 [WAX链设置](/build/dapp-development/wax-blockchain-setup/)从源代码构建。
- 使用 [WAX 合约开发工具包 (WAX-CDT)](/build/dapp-development/wax-cdt/)来编译您的智能合约。

## 开始之前：

无论您选择哪种部署方式，您都需要：

- 创建一个自主管理的WAX链账户。
- 确保您的账户中有足够的WAX质押，以便分配资源。
  
<ChildTableOfContents :max="2" title="More inside this section" />
