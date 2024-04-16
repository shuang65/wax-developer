---
标题: 使用 WaxJS
顺序: 2
---

# 使用 WaxJS

 **WaxJS** 库公开了四个组件:

- **wax.userAccount.** 当您调用 wax.login() 时返回的 WAX 账户用户名。
- **wax.pubKeys.** 用户的活跃密钥和所有者密钥。这些密钥在用户登录后或者在 WaxJS 构造函数中传递的情况下可用。
- **wax.api.** 使用这个功能可以执行标准的 eosjs 交易。
- **wax.rpc.** 使用这个功能可以向 WAX 链发出 API 调用。要了解更多信息，请参考 [WAX RPC API](/build/api-reference/) 。

使用 **WaxJS**:

1. 导入库。如果您正在使用 npm 或 yarn 构建 React 风格的应用程序，可以通过以下方式导入库：
   
   ```js
   import * as waxjs from "@waxio/waxjs/dist";
   ```

  
您也可以从 GitHub 下载并保存 [WaxJS](https://raw.githubusercontent.com/worldwide-asset-exchange/waxjs/develop/dist-web/waxjs.js) ，然后在网页中引入该文件：

   ```js
   <script src="waxjs.js"></script>
   ```

3. 根据您对用户的信息，有多种实例化 WaxJS 构造函数的方式。构造函数的参数包括：
   
   - 要连接的RPC 服务器的 URL（必填）
   - 用户的 WAX 链账户名称（可选）
   - 特定账户的公钥数组（可选）
   - 自动登录的布尔值 (可选)

   您可以通过简单传递一个 RPC URL 让 WaxJS 分配适当的用户值：

   ```js
   const wax = new waxjs.WaxJS({
     rpcEndpoint: "https://wax.greymass.com",
   });
   ```

   ::: 提示
   WaxJS 的构造函数在 1.0 版本中有所更改。如果您正在从之前的版本进行更新，您将需要更改构造函数。
   :::

   如果您有用户账户和公钥信息，也可以使用这些信息实例化库。只需将这些信息传递给 WaxJS 构造函数即可。
   ```js
   const wax = new waxjs.WaxJS({
     rpcEndpoint: "https://wax.greymass.com",
     userAccount: "3m1q4.wam",
     pubKeys: [
       "EOS6rjGKGYPBmVGsDDFAbM6UT5wQ9szB9m2fEcqHFMMcPge983xz9",
       "EOS7wTCoctybwrQWuE2tWYGwdLEGRXE9rrzALeBLUhWfbHXysFr9W",
     ],
   });
   ```

   ::: 注意
   如果您传递了这些额外的参数，就不需要调用 autoLogin 方法了。
   :::

5. 在您的 dApp 中开始签署交易之前，用户必须先登录。WaxJS 包含一个 `isAutoLoginAvailable` 函数，它用于判断：

   - 安全地验证 Cloud Wallet 的凭据
   - 检查您的 dApp 是否已列入白名单

   如果这两个条件都为真，用户的用户账户和公钥将会在您的 WaxJS 对象中设置， 这样您就不需要调用 `login()` 函数。 同时，您还将可以访问 wax.userAccount 和 wax.pubKeys。

   ```js
   //if true, popup won't be triggered; user is now logged in
   var isAutoLoginAvailable = await wax.isAutoLoginAvailable();
   var userAccount = wax.userAccount;
   var pubKeys = wax.pubKeys;
   ```

   如果没有自动登录，你可以直接用 `login()` 函数，让用户通过 Cloud Wallet 来登录或注册。

   ```js
   //normal login. Triggers a popup for non-whitelisted dapps
   async function login() {
     try {
       const userAccount = await wax.login();
       const pubKeys = wax.pubKeys;
     } catch (e) {}
   }
   ```

   用户点击登录 `login()` 时，会在新的浏览器窗口打开 Cloud Wallet。用户会看到您的 dApp 请求“了解您的 WAX 账户名”的提示。点击批准后，用户会被重新导向回您的 dApp。

  成功登录后会返回用户账户 (例如， jq3ao.wam)， 您也可以通过调用 `wax.userAccount`属性来访问这个信息。

6. 发送一笔交易

   现在您有了用户的 WAX 账户名，可以使用 `wax.api` 对象来构建您的交易。

::: 注意
在您执行登录用户操作或者将用户信息传递给 WaxJS 构造函数之前， `wax.api` 是未初始化的。
:::

```js
const result = await wax.api.transact(
  {
    actions: [
      {
        account: "eosio.token",
        name: "transfer",
        authorization: [
          {
            actor: wax.userAccount,
            permission: "active",
          },
        ],
        data: {
          from: wax.userAccount,
          to: "eosio",
          quantity: "0.00000001 WAX",
          memo: "",
        },
      },
    ],
  },
  {
    blocksBehind: 3,
    expireSeconds: 1200,
  }
);
```

::: 注意
 `wax.api` 方法是 **eosjs** 对象的一个实例， 并提供了相同的功能， 请参考 [eosjs](https://eosio.github.io/eosjs/latest) 文档以获得更多信息。
:::

`wax.api.transact()` 函数会在新的浏览器窗口中启动 Cloud Wallet。在这个界面上，用户可以查看交易详情，并选择“批准”或“拒绝”交易。用户如果点击“批准”，交易将在 WAX 链上签名，用户将被重定向回您的 dApp。
