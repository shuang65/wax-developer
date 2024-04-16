---
标题: WaxJS 演示
顺序: 4
---

# WaxJS 演示

以下是 WaxJS 功能的基本示例。要使用此演示，请点击 "WAX 登录"（如果您没有自动登录），然后再点击 "签署交易"。

**自动登录功能**
<p>如果您的区块链信息在下方显示，那么您已经自动登录到 WaxJS，无需再点击 WAX 登录。这样就省去了多次点击和弹出窗口的步骤！</p>
<p style="color:#ef9d47" id="autologin"></p>

**WAX 登录**
<p>如果您没有自动登录，请使用此功能。请注意，如果您已经自动登录，点击此功能不会打开弹出窗口，而是返回用户账户。
</p>

```html
<button class="text-md mt-4 border-black border-solid border-2 rounded px-4 py-2 w-40" id="login" onclick=login() >WAX Login</button>
```

<p style="color:#ef9d47" id="loginresponse"></p>
<p>&nbsp;</p>

**签署交易**
<p>在登录后点击一次</p>

```html
<button class="mt-4 border-black border-solid border-2 rounded px-4 py-2 w-40" id="sign" onclick=sign() >Sign Transaction</button>
```


## 代码示例
要使用这些示例， 请从 GitHub 下载并保存  [WaxJS](https://raw.githubusercontent.com/worldwide-asset-exchange/waxjs/develop/dist-web/waxjs.js) 文件。

**简单登录**

```js
const wax = new waxjs.WaxJS({
    rpcEndpoint: 'https://wax.greymass.com'
});

autoLogin(); 

//checks if autologin is available and calls the normal login function if it is 
async function autoLogin() { 
    var isAutoLoginAvailable = await wax.isAutoLoginAvailable(); 
    if (isAutoLoginAvailable) { 
        login(); 
    } 
} 

//normal login. Triggers a popup for non-whitelisted dapps
async function login() { 
    try { 
        const userAccount = await wax.login();  
    } catch(e) { 

    } 
} 
```

**完整的演示**

要运行上面的演示， 请将以下代码复制到 **index.html**文件中:

```html
<!DOCTYPE html>
<html>
<script src='waxjs.js'></script>

<body>

以下是 WaxJS 功能的基本示例。要使用此演示，请点击 WAX 登录（如果您没有自动登录），然后再点击签署交易。

<strong>Auto-login Feature</strong>
<p>If your blockchain information displays below, you're automatically logged in to WaxJS, and you don't need to click WAX Login. This eliminates the need for multiple clicks and popups!</p>
<p style="color:#ef9d47" id="autologin"></p>

<strong>WAX Login</strong>
<p>Use this if you're not automatically logged in. Note that if you are auto-logged in, clicking this does not open a popup and the userAccount is still returned.</p>
<button id="login" onclick=login()>WAX Login</button>
<p style="color:#ef9d47" id="loginresponse"></p>
<p>&amp;nbsp;</p>
<strong>Sign Transaction</strong>
<p>Click once you're logged in.</p>
<button id="sign" onclick=sign()>Sign Transaction</button>
<pre><code id="response">Transaction Response
</code></pre>


<script>
    const wax = new waxjs.WaxJS({
        rpcEndpoint: 'https://wax.greymass.com'
    });

    //automatically check for credentials
    autoLogin();

    //checks if autologin is available 
    async function autoLogin() {
        let isAutoLoginAvailable = await wax.isAutoLoginAvailable();
        if (isAutoLoginAvailable) {
            let userAccount = wax.userAccount;
            let pubKeys = wax.pubKeys;
            let str = 'AutoLogin enabled for account: ' + userAccount + '<br/>Active: ' + pubKeys[0] + '<br/>Owner: ' + pubKeys[1]
            document.getElementById('autologin').insertAdjacentHTML('beforeend', str);
        }
        else {
            document.getElementById('autologin').insertAdjacentHTML('beforeend', 'Not auto-logged in');
        }
    }

    //normal login. Triggers a popup for non-whitelisted dapps
    async function login() {
        try {
            //if autologged in, this simply returns the userAccount w/no popup
            let userAccount = await wax.login();
            let pubKeys = wax.pubKeys;
            let str = 'Account: ' + userAccount + '<br/>Active: ' + pubKeys[0] + '<br/>Owner: ' + pubKeys[1]
            document.getElementById('loginresponse').insertAdjacentHTML('beforeend', str);
        } catch (e) {
            document.getElementById('loginresponse').append(e.message);
        }
    } 

    async function sign() {
    if(!wax.api) {
        return document.getElementById('response').append('* Login first *');
    }

    try {
        const result = await wax.api.transact({
        actions: [{
            account: 'eosio',
            name: 'delegatebw',
            authorization: [{
            actor: wax.userAccount,
            permission: 'active',
            }],
            data: {
            from: wax.userAccount,
            receiver: wax.userAccount,
            stake_net_quantity: '0.00000001 WAX',
            stake_cpu_quantity: '0.00000000 WAX',
            transfer: false,
            memo: 'This is a WaxJS/Cloud Wallet Demo.'
            },
        }]
        }, {
        blocksBehind: 3,
        expireSeconds: 30
        });
        document.getElementById('response').append(JSON.stringify(result, null, 2))
    } catch(e) {
        document.getElementById('response').append(e.message);
    }
    }

</script>
</body>
</html>

```
