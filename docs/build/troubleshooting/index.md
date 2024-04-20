---
标题: 排除故障
顺序: 200
---

# 排除故障

以下是已知问题的列表及相关修复方法（如果发生了的话）：

## 函数 `fork_once_func'中的构建错误

**错误描述:** WAX 源代码库构建问题

在**Ubuntu 18.04**上运行`sudo ./wax_install.sh` 构建WAX源代码存储库时， 命令行报告了一个错误： "In function 'fork_once_func'" (大约在 [90%]左右):

```
Scanning dependencies of target test_cypher_suites
Scanning dependencies of target eosio_chain
[ 90%] Building CXX object libraries/fc/test/crypto/CMakeFiles/test_cypher_suites.dir/test_cypher_suites.cpp.o
[ 90%] Building CXX object libraries/chain/CMakeFiles/eosio_chain.dir/merkle.cpp.o
[ 90%] Building CXX object libraries/chain/CMakeFiles/eosio_chain.dir/name.cpp.o
[ 90%] Building CXX object libraries/chain/CMakeFiles/eosio_chain.dir/transaction.cpp.o
[ 90%] Linking CXX executable test_cypher_suites
/usr/lib/x86_64-linux-gnu/libcrypto.a(threads_pthread.o): In function `fork_once_func':
(.text+0x16): undefined reference to `pthread_atfork'
clang: error: linker command failed with exit code 1 (use -v to see invocation)
libraries/fc/test/crypto/CMakeFiles/test_cypher_suites.dir/build.make:113: recipe for target 'libraries/fc/test/crypto/test_cypher_suites' failed
make[2]: *** [libraries/fc/test/crypto/test_cypher_suites] Error 1
CMakeFiles/Makefile2:783: recipe for target 'libraries/fc/test/crypto/CMakeFiles/test_cypher_suites.dir/all' failed
make[1]: *** [libraries/fc/test/crypto/CMakeFiles/test_cypher_suites.dir/all] Error 2
make[1]: *** Waiting for unfinished jobs....
```

在收到这个错误后，构建过程停止，并显示以下消息：

```
MAKE构建 EOSIO 时出现了上述错误，并已退出。 
```

### 修复

以下内容是修复问题并继续构建WAX源代码存储库的步骤。

1. 命令行中，将目录更改为：

```
cd patches/fc
```

2. 在 <span class="sampleCode">patches/fc</span> 目录中运行以下命令：

```
./apply_patch.sh
```

3. 补丁完成后，请切换至以下目录：

```
cd ../../build
```

4. 在 **build** 目录中运行以下命令：

```
make -j $(nproc)
```

您现在能够继续构建了。
