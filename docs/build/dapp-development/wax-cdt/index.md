---
标题: WAX 合约开发工具包
顺序: 50
---

# WAX 合约开发工具包

<a href="https://github.com/worldwide-asset-exchange/wax-cdt" target="_blank">WAX 合约开发工具包 (WAX-CDT)</a> 包含了 C/C++ API 和基于 <a href="https://clang.llvm.org/" target="_blank">Clang</a> 的一组工具，用于构建和部署您的智能合约。

WAX-CDT 工具包包含在 **waxteam/dev** Docker 镜像中， 我们还提供了一个单独的 **waxteam/cdt** Docker 镜像。要启动一个交互式的WAX-CDT容器，您需要使用以下命令：

```shell run -it --name waxcdt -v /var/share/wax:/wax waxteam/cdt bash```

请参阅我们的 [Docker 快速入门](/build/dapp-development/docker-setup/) 获取更多信息。

如果您想从本地驱动器访问我们的示例合约和脚本，或者选择安装WAX-CDT而不是使用Docker，您可以使用这个方法下载并选择性的构建WAX-CDT源代码。

:::警告
重要: 目前还没有提供预编译的软件包。如果您从源代码构建WAX-CDT，则无法获得帮助。
:::

## 包括什么

- 用于与WAX链通信的 [C/C++ API 库](/build/api-reference/cdt_api) 
- 只能合约示例，可以帮助您d开发App
- 用于创建新智能合约模版的工具 
- 使用CMake脚本构建优化，高性能的WASM文件
- 支持Ricardian文件格式

WAX-CDT 包括多种 **eosio** 命令， 基于<a href="https://clang.llvm.org/" target="_blank">Clang</a> 的前端和工具基础设施。该集合包括了多种工具，用于编译智能合约并创建智能合约模板。可以参考 [WAX-CDT Options](/build/tools/cdt_选项) 查看工具和参数列表：

-  示例合约和可自定义的**make**脚本，用于自动生成 WASM 和 ABI 文件。 
- 基于<a href="https://clang.llvm.org/" target="_blank">Clang</a> 的工具， 其中包括
  - **eosio-cpp:** C++ 编译器
  - **eosio-ld:** WebAssembly 链接器
  - **eosio-abigen:** C++ ABI 生成器

## 如何工作的

当您准备在本地开发环境或 WAX 主网上部署智能合约时，可以使用 <a href="https://github.com/worldwide-asset-exchange/wax-cdt" target="_blank">WAX 合约开发工具包 (WAX-CDT)</a> 将合约转化为 WebAssembly (WASM) 文件。同时， 也可以使用 WAX-CDT创建包含 [Ricardian Contracts](/build/tools/ricardian_contract) 和 [Ricardian Clauses](/build/tools/ricardian_clause)的应用程序二进制接口（ABI）文件。

- **WebAssembly (WASM) 文件:**WASM 文件是经过优化的二进制格式，存储着您的 C++ 智能合约，旨在提升执行速度和网络性能。WAX 链会使用这些文件来执行智能合约中定义的操作。 

- **应用程序二进制接口 (ABI) 文件:** ABI 文件是智能合约结构、类型、操作、表格以及其他定义的 JSON 描述，使得开发者和客户端接口能够轻易理解和解释合约功能。


    ### ABI示例
    该例包含了一个"hi"操作的 Ricardian合约以及一个针对合约的 Ricardian 条款。

    ```json
    {
        "____comment": "This file was generated with eosio-abigen. DO NOT EDIT Fri Jul 19 13:36:50 2019",
        "version": "eosio::abi/1.1",
        "structs": [
            {
                "name": "hi",
                "base": "",
                "fields": [
                    {
                        "name": "user",
                        "type": "name"
                    }
                ]
            }
        ],
        "types": [],
        "actions": [
            {
                "name": "hi",
                "type": "hi",
                "ricardian_contract": "### Parameters\nInput parameters:\n\n* `user` (string to include in the output)\n\nImplied parameters: \n\n* `account_name` (name of the party invoking and signing the contract)\n\n### Intent\nINTENT. The intention of the author and the invoker of this contract is to print output. It shall have no other effect.\n\n### Term\nTERM. This Contract expires at the conclusion of code execution."
            }
        ],
        "tables": [],
        "ricardian_clauses": [
            {
                "id": "Warranty",
                "body": "The invoker of the contract action shall uphold its Obligations under this Contract in a timely and workmanlike manner, using knowledge and recommendations for performing the services which meet generally acceptable standards set forth by EOS.IO Blockchain Block Producers."
            },
            {
                "id": "Default",
                "body": "The occurrence of any of the following shall constitute a material default under this Contract:"
            },
            {
                "id": "Remedies",
                "body": "In addition to any and all other rights a party may have available according to law, if a party defaults by failing to substantially perform any provision, term or condition of this Contract, the other party may terminate the Contract by providing written notice to the defaulting party. This notice shall describe with sufficient detail the nature of the default. The party receiving such notice shall promptly be removed from being a Block Producer and this Contract shall be automatically terminated."
            },
            {
                "id": "ForceMajeure",
                "body": "If performance of this Contract or any obligation under this Contract is prevented, restricted, or interfered with by causes beyond either party's reasonable control (\"Force Majeure\"), and if the party unable to carry out its obligations gives the other party prompt written notice of such event, then the obligations of the party invoking this provision shall be suspended to the extent necessary by such event. The term Force Majeure shall include, without limitation, acts of God, fire, explosion, vandalism, storm or other similar occurrence, orders or acts of military or civil authority, or by national emergencies, insurrections, riots, or wars, or strikes, lock-outs, work stoppages, or supplier failures. The excused party shall use reasonable efforts under the circumstances to avoid or remove such causes of non-performance and shall proceed to perform with reasonable dispatch whenever such causes are removed or ceased. An act or omission shall be deemed within the reasonable control of a party if committed, omitted, or caused by such party, or its employees, officers, agents, or affiliates."
            },
            {
                "id": "DisputeResolution",
                "body": "Any controversies or disputes arising out of or relating to this Contract will be resolved by binding arbitration under the default rules set forth by the EOS.IO Blockchain. The arbitrator's award will be final, and judgment may be entered upon it by any court having proper jurisdiction."
            },
            {
                "id": "Agreement",
                "body": "This Contract contains the entire agreement of the parties, and there are no other promises or conditions in any other agreement whether oral or written concerning the subject matter of this Contract. This Contract supersedes any prior written or oral agreements between the parties."
            },
            {
                "id": "Severability",
                "body": "If any provision of this Contract will be held to be invalid or unenforceable for any reason, the remaining provisions will continue to be valid and enforceable. If a court finds that any provision of this Contract is invalid or unenforceable, but that by limiting such provision it would become valid and enforceable, then such provision will be deemed to be written, construed, and enforced as so limited."
            },
            {
                "id": "Amendment",
                "body": "This Contract may be modified or amended in writing by mutual agreement between the parties, if the writing is signed by the party obligated under the amendment."
            },
            {
                "id": "GoverningLaw",
                "body": "This Contract shall be construed in accordance with the Maxims of Equity."
            },
            {
                "id": "Notice",
                "body": "Any notice or communication required or permitted under this Contract shall be sufficiently given if delivered to a verifiable email address or to such other email address as one party may have publicly furnished in writing, or published on a broadcast contract provided by this blockchain for purposes of providing notices of this type."
            },
            {
                "id": "WaiverOfContractualRight",
                "body": "The failure of either party to enforce any provision of this Contract shall not be construed as a waiver or limitation of that party's right to subsequently enforce and compel strict compliance with every provision of this Contract."
            },
            {
                "id": "ArbitratorsFeesToPrevailingParty",
                "body": "In any action arising hereunder or any separate action pertaining to the validity of this Agreement, both sides shall pay half the initial cost of arbitration, and the prevailing party shall be awarded reasonable arbitrator's fees and costs."
            },
            {
                "id": "ConstructionAndInterpretation",
                "body": "The rule requiring construction or interpretation against the drafter is waived. The document shall be deemed as if it were drafted by both parties in a mutual effort."
            },
            {
                "id": "InWitnessWhereof",
                "body": "In witness whereof, the parties hereto have caused this Agreement to be executed by themselves or their duly authorized representatives as of the date of execution, and authorized as proven by the cryptographic signature on the transaction that invokes this contract."
            }
        ],
        "variants": [],
        "abi_extensions": []
    }
    ```



<!--A Ricardian Contract is a cryptographically signed and verified digital document that lists your smart contracts actions, intentions, terms, and conditions. Like any standard legal document, it provides a digital agreement between two parties (e.g., you and your customer), and your smart contract is the execution of this agreement.-->
