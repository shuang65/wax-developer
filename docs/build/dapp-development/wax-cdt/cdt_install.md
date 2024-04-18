---
标题: 安装 WAX-CDT
顺序: 51
---

# 安装 WAX-CDT

GitHub上的WAX-CDT存储库会下载到 **wax-cdt** 目录中，下载和构建过程的时间会根据您的网络、操作系统和硬件规格而不同，可能需要几分钟到几个小时。

要下载WAX-CDT源代码库，请将以下内容粘贴到命令行中：

```
git clone --recursive https://github.com/worldwide-asset-exchange/wax-cdt.git
```

## Build WAX-CDT

如果正在使用我们的Docker镜像，您 **不需要** 完成这些步骤。

从源代码构建WAX-CDT，需要按照以下步骤进行。如果您已安装了旧版本，首先需要卸载旧版本。有关更多信息，请参阅 [Uninstall WAX-CDT](/build/dapp-development/wax-cdt/cdt_uninstall)。

:::警告
重要: 不支持从源代码构建。如果在开发过程中遇到问题，可以使用我们的 [Docker 镜像](/build/dapp-development/docker-setup/) instead (推荐)。
:::

1. 将您的目录更改为 **wax-cdt**。

```
cd wax-cdt
```

2. 运行构建脚本。

```
./build.sh
```

3. 运行安装脚本。

```
sudo ./install.sh
```
