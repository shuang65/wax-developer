---
标题: 卸载 WAX-CDT
顺序: 95
---

# 卸载 WAX-CDT

如果您已经安装了旧版本的 WAX-CDT (版本 : wax-1.4.1-1.0.0)，需要先卸载它，然后才能安装最新版本。 

## 移除什么？

脚本将会移除以下工具：

* eosio-cpp
* eosio-cc
* eosio-ld
* eosio-init
* eosio-abidiff
* eosio-wasm2wast
* eosio-wast2wasm
* eosio-ranlib
* eosio-ar
* eosio-objdump
* eosio-readelf

:::提示
如果您在此目录中创建了文件夹或修改了任何文件，这些文件夹和文件在运行卸载脚本后将保持不变。这个脚本只会移除WAX-CDT工具。
:::


## 运行卸载脚本

卸载 WAX-CDT:

1. 命令行中导航至您的 WAX-CDT 文件夹 (例如， wax-blockchain/wax-cdt).

2. 运行卸载脚本

    ```
    sudo ./uninstall.sh
    ```

   输入您的密码， 然后输入1卸载 WAX-CDT.。

