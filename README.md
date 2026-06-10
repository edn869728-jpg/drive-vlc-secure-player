# Drive VLC Secure Player｜iOS 捷徑流動 token 版

這包是最新 ZIP，可直接覆蓋前端與 GAS。

## 必改

### Code.gs

```js
const ROOT_FOLDER_ID = '你的影音資料夾ID';
const INITIAL_LOGIN_KEY = '你的管理登入密鑰';
```

你已經建立過 token 檔案就不用再執行 setup。若改登入密鑰，執行：

```js
resetDriveVlcLoginKey()
```

### index.html

```js
GAS_API_URL: '你的 GAS Web App /exec 網址',
```

## iOS 捷徑流程

第一次登入：

```txt
GAS_URL?action=adminLogin&includeData=0&loginKey=你的管理密鑰
```

保存回傳：

```txt
sessionToken
```

之後換新 token：

```txt
GAS_URL?action=refreshSession&sessionToken=目前token
```

保存回傳：

```txt
nextSessionToken
```

重點：每次成功驗證後，舊 token 立即失效，捷徑一定要把 nextSessionToken 覆蓋舊 token。

## 網頁接收 token

```txt
https://你的GitHub頁面/#session=你的token
```

也可以用：

```txt
https://你的GitHub頁面/?admin=1
```

強制進管理登入。
