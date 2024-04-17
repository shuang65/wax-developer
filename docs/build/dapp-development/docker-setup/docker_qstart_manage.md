---
标题: 管理 容器
顺序: 24
---

# 管理 容器

要退出交互式的 bash 会话（不停止容器），请按 `ctrl-p` + `ctrl-q` 发送一个退出序列。控制台会打印出以下信息：

```shell
read escape sequence
```

上面的命令执行后，你将会返回到主机的命令提示符。你可以使用 `docker ps` 命令确认容器是否还在运行：

```shell
docker ps
```

要重新连接到您的 bash 会话，请使用 `docker attach` 命令。

```shell
docker attach waxdev
```

使用 `docker stop` 命令来停止您的容器。

```shell
docker stop waxdev
```

使用 `docker start` 命令来重新启动您的容器。

```shell
docker start waxdev
```

如果 `docker ps` 命令没有列出您的容器， 请使用 `-a` 参数重新运行该命令。 这样可以显示所有容器，包括那些当前没有运行的容器。

```shell
docker ps -a
```

当您完成了Docker环境的设置，就可以开始阅读本节的指南了。尽管完成下一个教程中的 [WAX 链设置](/build/dapp-development/wax-blockchain-setup/) 并不是必须的， 但我们仍建议您下载源代码以获取代码示例和 **make** 脚本。




