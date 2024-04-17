---
标题: boost.wax
---

# boost.wax

该合约记录了其他合约，让它们能够让 WAX 对其 Cloud Wallet用户的 CPU 和网络进行扩展管理。 

部署到: [boost.wax](https://wax.bloks.io/account/boost.wax)


## Cloud Wallet  资源模型

Cloud Wallet账户的资源分配模型基于账户活动设计。与在创建时为每个Cloud Wallet账户分配资源不同，新的资源模型在执行和签署交易时为每个账户分配必要的资源，然后将这些资源收回。这个新模型允许从活跃度较低的账户中汇集资源，用于增强活跃账户的活动。该新提升系统设计为分层资源池系统，在用户需要提供资源之前，首先检查两个资源层的可用带宽。

### dApp Boost 提升资源池层级

在24小时内，Cloud Wallet将为每个dApp分配高达5秒的CPU时间和5M字节的NET带宽；这相当于每个dApp在该时间段内进行约10000次提升操作，假设平均动作资源成本为0.5毫秒。dApp提升资源池的参数可能会随着时间调整，以便更好地利用数据。
   
另外，每个dApp可以通过投入自己的WAXP来增加其dApp提升资源池。 ddApp智能合约必须具有一个名为paybw的权限，并且必须链接到boost.wax#noop动作。此外，它必须具有使用账户@权限boost.wax@paybw的1对1权限。例如，请查看 [test.wax@paybw permission](https://wax.bloks.io/account/test.wax#keys).
   

当初始dApp的提升资源池层级被超出时，Cloud Wallet将会代表dApp用户进行签名，前提是Cloud Wallet的合约账户有足够的CPU和NET分配。 每个dApp还需要通过boost.wax智能合约的 [这个操作](https://wax.bloks.io/account/boost.wax?loadContract=true&tab=Actions&account=boost.wax&scope=boost.wax&limit=100&action=reg) 来配置每个用户的dApp提升资源池分配。

如果dApp池有可用资源，Cloud Wallet会使用dApp池中的资源来增强用户的交易，并相应地减少池中的资源。
   
Cloud Wallet团队保留在特定dApp中禁用dApp提升资源池的权利。

### 用户提升资源池层级

在给定的24小时时间段内，Cloud Wallet会为每个用户分配高达5毫秒的CPU时间和5千字节的NET带宽。这相当于每个用户在该时间段内进行约10次提升操作，假设平均动作资源成本为0.5毫秒。用户提升资源池的参数可能会随着更多利用数据的可用性而调整。

当dApp提升资源池层级和用户提升资源池层级都有足够资源时，Cloud Wallet新的资源机制才能提升操作。如果dApp或用户提升资源池中的资源用尽，Cloud Wallet将转而使用dApp自身的抵押资源；同时，如果用户超过了dApp配置的24小时带宽限制，Cloud Wallet将使用用户的抵押资源。

::: 信息
![alt text](https://github.com/worldwide-asset-exchange/boost.wax/blob/master/BoostDecisionTree.png?raw=true)
:::

这个提升系统可以控制资源使用，确保每个用户有足够的资源，可以参与基于NFT的活动，如卡包发放、开启、制作、NFT的购买、销售和交易，而不受网络上当前资源成本的影响。

### RAM Boost

WCW创建新账户时，会提供刚好足够成功创建一个账户所需的最少RAM。这样，即使用户需要执行需要RAM的交易，WCW也会为在由WAX支付的带宽提升层级下成功提升带宽的交易增加RAM。目前，WAX将资助最多4096字节的账户RAM，包括账户创建所需的RAM。未来，RAM提升将适用于dApp付费层级，如果一笔交易不符合WAX支付/用户提升层级下的提升条件，则由相关dApps支付。

## API

* [`reg(name contract, uint64_t cpu_us_per_user, uint64_t net_words_per_user, bool use_allow_list, vector<name> allowed_contracts)`](https://wax.bloks.io/account/boost.wax?loadContract=true&tab=Actions&account=boost.wax&scope=boost.wax&limit=100&action=reg)

   请注册您的合约以进行带宽管理。  
   * `contract`: 必须是调用此操作的账户本身来注册合约账户。  
   * `cpu_us_per_user`: 您可以为用户在24小时内提供的CPU时间量，单位是微秒。  
   * `net_words_per_user`: 您可以为用户在24小时内提供的NET带宽量，单位是微秒。  
   * `use_allow_list`: 切换白名单执行的开关。
   * `allowed_contracts`: 以下是允许出现在您合约伴随交易中的合约名称的向量。这些合约必须设置 use_allow_list 为 true 才会被执行。这样做的目的是防止一些dApp滥用您合约的行为，将它们偷偷放入自己的交易中，以占用您的带宽配额。 当您在合约中列出接受的合约时，只有包含在这个列表中的所有交易合约，才会由您自己的cpu+net支付。  
   
  ::: 注意
    当您的合约超出免费层级时，WAX后端会为您的用户签名，前提是您的合约账户有足够的CPU和NET。为此，您的合约必须有一个名为 **paybw**的权限， 链接到 **boost.wax**的**noop** 动作。 并且必须具有1对1的权限，使用账户@权限 `boost.wax@paybw`。 您可以参考 [test.wax@paybw permission](https://wax.bloks.io/account/test.wax#keys)。
  :::
   
* **[`dereg(name contract`)](https://wax.bloks.io/account/boost.wax?loadContract=true&tab=Tables&account=boost.wax&scope=boost.wax&limit=100&action=dereg)**: 

   取消您合约的带宽管理注册。  
   
* **[`noop()`](https://wax.bloks.io/account/boost.wax?loadContract=true&tab=Tables&account=boost.wax&scope=boost.wax&limit=100&action=noop)**: 

   在满足带宽管理条件的Cloud Wallet交易中，会插入一个空操作。（No-op action）  

* **`boost(name from, name to, asset cpu, asset net)`**: *Deprecated*
* **`updateboost(name from, name to, asset cpu_to, asset net_to)`**: *Deprecated*
* **`unboost(name from, name to)`**: *Deprecated*
* **`boosterdel (name booster)`**: *Deprecated*
