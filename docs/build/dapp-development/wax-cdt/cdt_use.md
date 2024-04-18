---
标题: WAX-CDT 合约示例
顺序: 52
---

# WAX-CDT 合约示例

WAX-CDT 会有一个 **wax-cdt/examples** 目录， 其中包含以下智能合约示例：

- Hello World
- multi_index 示例
- Inline Transaction 示例

每个项目都包含两个 **CMakeLists.txt** 文件： 一个在根目录中，另一个在**src** 目录中。 您可以使用这些文件自动生成示例项目的WASM和ABI文件。

在本教程中，您将学习如何使用 **make** 脚本构建 Hello World 示例。

:::警告
<strong>注意：</strong> 这些示例是使用 **eosio-init** ( [WAX-CDT 选项](/build/tools/cdt_options) 工具套件的一部分)创建的。 请参阅 [创建智能合约](/build/dapp-development/wax-cdt/cdt_use.html#compile-hello-world) 来为您的智能合约选择脚本。
:::

## 编译 Hello World

要编译 Hello World 示例：

1. 从命令行导航至 **wax-cdt/examples/hello**。

    ```shell
    cd wax-cdt/examples/hello
    ```

2. 创建一个 **build** 目录。

    ```shell
    mkdir build
    ```

:::警告
    <strong>注意：</strong> 默认情况下， <strong>eosio-init</strong> 会创建一个 build 目录。 该目录是空的，所以不会上传至Git。 如果使用 <strong>eosio-init</strong> [创建智能合约](/build/dapp-development/wax-cdt/cdt_use.html#compile-hello-world)，您可以跳过这一步。 
:::

3. 导航至 **build** 目录。

    ```shell
    cd build
    ```

4. 在 **wax-cdt/examples/hello** 目录初始化cmake，将必要的开发文件写入 **build** 目录。.

    ```shell
    cmake ..
    ```

    控制台会输出以下开发任务：

    ```shell
    -- The C compiler identification is GNU 7.4.0
    -- The CXX compiler identification is GNU 7.4.0
    -- Check for working C compiler: /usr/bin/cc
    -- Check for working C compiler: /usr/bin/cc -- works
    -- Detecting C compiler ABI info
    -- Detecting C compiler ABI info - done
    -- Detecting C compile features
    -- Detecting C compile features - done
    -- Check for working CXX compiler: /usr/bin/c++
    -- Check for working CXX compiler: /usr/bin/c++ -- works
    -- Detecting CXX compiler ABI info
    -- Detecting CXX compiler ABI info - done
    -- Detecting CXX compile features
    -- Detecting CXX compile features - done
    -- Setting up Eosio Wasm Toolchain 1.6.1 at /usr/local/eosio.cdt
    CMake Warning (dev) in CMakeLists.txt:
      No cmake_minimum_required command is present.  A line of code such as

        cmake_minimum_required(VERSION 3.10)

      should be added at the top of the file.  The version specified may be lower
      if you wish to support older CMake versions for this project.  For more
      information run "cmake --help-policy CMP0000".
    This warning is for project developers.  Use -Wno-dev to suppress it.

    -- Configuring done
    -- Generating done
    -- Build files have been written to: waxblockchain/wax-blockchain/wax-cdt/examples/hello/build
    ```

4. 构建脚本

    ```shell
    make
    ```

    控制台会输出以下信息：

    ```shell
    [  5%] Performing build step for 'hello_project'
    [100%] Built target hello
    [ 11%] No install step for 'hello_project'
    [ 16%] No test step for 'hello_project'
    [ 22%] Completed 'hello_project'
    [ 50%] Built target hello_project
    [ 55%] Performing configure step for 'hello_tests_project'
    ```

现在应该能在**build/hello**目录中找到 **hello.wasm** 和 **hello.abi** 文件了。 

<!--## Modify the Scripts and Build Your Project

If you didn't use eosio-init to create a smart contracts template (recommended), you can still use the CMake scripts to build your smart contract by making just a few modifications.

In the example below, we'll use the following directory structure:

- A **mycontracts** root directory
- A **mycontracts/wax** folder that contains the following:

    - wax.cpp
    - wax.contracts.md (optional Ricardian contract)
    - wax.clauses.md (optional Ricardian clause)

To customize the build scripts:

1. Copy **wax-cdt/examples/hello/CMakeLists.txt** into **mycontracts** (your parent smart contract directory). 

2. From **mycontracts**, open **CmakeLists.txt** and modify the `ExternalProject_Add` method. 

**mycontracts/CMakeLists.txt:**

```
include(ExternalProject)
# if no cdt root is given use default path
if(EOSIO_CDT_ROOT STREQUAL "" OR NOT EOSIO_CDT_ROOT)
   find_package(eosio.cdt)
endif()

ExternalProject_Add(
   wax_project
   SOURCE_DIR ${CMAKE_SOURCE_DIR}/wax
   BINARY_DIR ${CMAKE_BINARY_DIR}/wax
   CMAKE_ARGS -DCMAKE_TOOLCHAIN_FILE=${EOSIO_CDT_ROOT}/lib/cmake/eosio.cdt/EosioWasmToolchain.cmake
   UPDATE_COMMAND ""
   PATCH_COMMAND ""
   TEST_COMMAND ""
   INSTALL_COMMAND ""
   BUILD_ALWAYS 1
)
```

Save the file.

3. Copy **wax-cdt/examples/hello/src/CMakeLists.txt** into **mycontracts/wax**. 

**mycontracts/wax/CMakeLists.txt:**

```
project(wax)

set(EOSIO_WASM_OLD_BEHAVIOR "Off")
find_package(eosio.cdt)

add_contract( wax wax wax.cpp )
target_include_directories( wax PUBLIC ${CMAKE_SOURCE_DIR} )
target_ricardian_directory( wax ${CMAKE_SOURCE_DIR} )
```

Save the file.

4. From the command line, navigate to **wax-cdt/mycontracts**.

```
cd wax-cdt/mycontracts
```

5. Create a **build** directory.

```
mkdir build
```

6. Navigate to the **build** directory.

```
cd build
```

7. Run `cmake` to write the necessary build files to the **build** directory.

```
cmake ..
```

8. Build the scripts. You might receive several warnings during this process.

```
make
```

You should now be able to locate the **wax.wasm** and **wax.abi** files in the **build/wax** directory. -->





