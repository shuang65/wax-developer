---
标题: Ricardian 条款
顺序: 112
---

# Ricardian Clauses

与 [Ricardian合约](/build/tools/ricardian_contract)类似，Ricardian条款是一份数字文档，用于规定整个智能合约的条款，而不仅仅是每个操作的条款。 

要将Ricardian条款与您的智能合约关联，需要编写一个Markdown文件。 

* 该文件的命名必须与您的智能合约相同。例如，如果您的智能合约名称为 **wax.cpp**， 则您的 Ricardian markdown 文件必须命名为： wax.clauses.md.
* 每个 **```<h1>```** 标签必须有 "clause" 类: ```<h1 class="clause">```。

您存储Ricardian Markdown文件的位置也很重要（与您的智能合约C++文件相关）。这取决于您如何编译您的合约。

## 使用 WAX-CDT

如果您使用 **eosio-init** 来创建智能合约模板，一个文件夹会自动在您的项目目录下创建（例如，wax/ricardian）。默认情况下，此文件夹不包含Ricardian条款。需要创建一个，例如wax.clauses.md。

CMake脚本会自动包含 **ricardian** 目录中列出的文件。

请参阅 [创建智能合约](/build/dapp-development/smart-contract-quickstart/) 以获取更多信息。

## 使用 eosio-cpp

如果您使用eosio-cpp，Ricardian条款必须与wax.cpp文件在同一个目录中，并且文件名必须相同：wax.clauses.md。

```shell
eosio-cpp -abigen wax.cpp -o wax.wasm
```

## Ricardian 条款示例

要包含 Ricardian 条款：

1. 创建一个名为 **your-contract.clauses.md**的文件 (例如， wax.clauses.md)。
2. 在 ```<h1>``` 标签中包含"clause"类。
3. 请将以下Markdown内容复制粘贴到您的条款文件中。

```html
<hr style="height:1px; border:none; color:#000; background-color:#000; width:100%; text-align:left; margin: 0 auto 0 0;">

<h1 class="clause">Warranty</h1>

The invoker of the contract action shall uphold its Obligations under this Contract in a timely and workmanlike manner, using knowledge and recommendations for performing the services which meet generally acceptable standards set forth by WAX.IO Blockchain Block Producers. 

<h1 class="clause">Default</h1>

The occurrence of any of the following shall constitute a material default under this Contract: 

<h1 class="clause">Remedies</h1>

In addition to any and all other rights a party may have available according to law, if a party defaults by failing to substantially perform any provision, term or condition of this Contract, the other party may terminate the Contract by providing written notice to the defaulting party. This notice shall describe with sufficient detail the nature of the default. The party receiving such notice shall promptly be removed from being a Block Producer and this Contract shall be automatically terminated. 

<h1 class="clause">ForceMajeure</h1>

If performance of this Contract or any obligation under this Contract is prevented, restricted, or interfered with by causes beyond either party's reasonable control ("Force Majeure"), and if the party unable to carry out its obligations gives the other party prompt written notice of such event, then the obligations of the party invoking this provision shall be suspended to the extent necessary by such event. The term Force Majeure shall include, without limitation, acts of God, fire, explosion, vandalism, storm or other similar occurrence, orders or acts of military or civil authority, or by national emergencies, insurrections, riots, or wars, or strikes, lock-outs, work stoppages, or supplier failures. The excused party shall use reasonable efforts under the circumstances to avoid or remove such causes of non-performance and shall proceed to perform with reasonable dispatch whenever such causes are removed or ceased. An act or omission shall be deemed within the reasonable control of a party if committed, omitted, or caused by such party, or its employees, officers, agents, or affiliates. 

<h1 class="clause">DisputeResolution</h1>

Any controversies or disputes arising out of or relating to this Contract will be resolved by binding arbitration under the default rules set forth by the WAX.IO Blockchain. The arbitrator's award will be final, and judgment may be entered upon it by any court having proper jurisdiction. 

<h1 class="clause">Agreement</h1>

This Contract contains the entire agreement of the parties, and there are no other promises or conditions in any other agreement whether oral or written concerning the subject matter of this Contract. This Contract supersedes any prior written or oral agreements between the parties. 

<h1 class="clause">Severability</h1>

If any provision of this Contract will be held to be invalid or unenforceable for any reason, the remaining provisions will continue to be valid and enforceable. If a court finds that any provision of this Contract is invalid or unenforceable, but that by limiting such provision it would become valid and enforceable, then such provision will be deemed to be written, construed, and enforced as so limited. 

<h1 class="clause">Amendment</h1>

This Contract may be modified or amended in writing by mutual agreement between the parties, if the writing is signed by the party obligated under the amendment. 

<h1 class="clause">GoverningLaw</h1>

This Contract shall be construed in accordance with the Maxims of Equity. 

<h1 class="clause">Notice</h1>

Any notice or communication required or permitted under this Contract shall be sufficiently given if delivered to a verifiable email address or to such other email address as one party may have publicly furnished in writing, or published on a broadcast contract provided by this blockchain for purposes of providing notices of this type. 

<h1 class="clause">WaiverOfContractualRight</h1>

The failure of either party to enforce any provision of this Contract shall not be construed as a waiver or limitation of that party's right to subsequently enforce and compel strict compliance with every provision of this Contract. 

<h1 class="clause">ArbitratorsFeesToPrevailingParty</h1>

In any action arising hereunder or any separate action pertaining to the validity of this Agreement, both sides shall pay half the initial cost of arbitration, and the prevailing party shall be awarded reasonable arbitrator's fees and costs. 

<h1 class="clause">ConstructionAndInterpretation</h1>

The rule requiring construction or interpretation against the drafter is waived. The document shall be deemed as if it were drafted by both parties in a mutual effort. 

<h1 class="clause">InWitnessWhereof</h1>

In witness whereof, the parties hereto have caused this Agreement to be executed by themselves or their duly authorized representatives as of the date of execution, and authorized as proven by the cryptographic signature on the transaction that invokes this contract.

```
