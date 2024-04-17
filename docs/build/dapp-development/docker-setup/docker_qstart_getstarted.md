---
标题: 运行 WAX 容器
顺序: 22
---

# 运行 WAX 容器

运行 **waxteam/dev** Docker 镜像：

1. 安装 <a href="https://www.docker.com/get-started" target="_blank">Docker</a> (如果尚未安装)。

:::提示
<strong>Linux 用户：</strong> 我们建议您将 Docker 配置为无需 sudo 运行，这样您就可以使用所有基于 Docker 的 make 脚本。您可以查看 <a href="https://docs.docker.com/install/linux/linux-postinstall/" target="_blank">Linux后续安装步骤</a> 获取更多信息。
:::

2. 创建一个名为 **wax**的新目录。您可以使用这个文件夹来存储 WAX 链源代码、示例以及您的 WAX 智能合约目录。这个目录将在您的操作系统和 Docker 容器之间共享。您将能够在任何环境中使用您喜欢的 IDE 编辑源代码。

3. 当您运行以下命令时，你会在容器内启动一个交互式的 WAX 容器，并且共享主机上的 **wax** 目录， 这样您就可以在容器内运行 bash 会话了：


    **Linux**

    ```shell
    docker run -it --name waxdev -v /c/wax:/wax waxteam/dev bash
    ```

    ```shell
    docker run -it --name waxcdt -v /c/wax:/wax waxteam/cdt bash
    ```

    **Windows 10**

    ```shell
    docker run -it --name waxdev -v c:\wax:/wax waxteam/dev bash
    ```

    ```shell
    docker run -it --name waxcdt -v c:\wax:/wax waxteam/cdt bash
    ```

    The console prints something similar to:

    ```shell
    root@b6e444e3cc33:/#
    ```

现在您应该有一个正在运行的容器，并且里面有一个已激活的 bash 会话。您可以使用这个 bash 会话来跟随我们的快速入门指南和教程。



