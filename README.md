# Drive VLC 安全限定播放清單版

## 重點

這版用「後端 token 檔案」防止別人繞回完整清單。

- GitHub 前端不放管理 token
- 完整清單必須管理登入
- 登入成功後，後端才回傳 session token
- 每次成功驗證後，才回傳 nextSessionToken
- 前端確認成功才覆蓋舊 token
- 舊 token 在後端立即失效
- playlist token 只讓對方取得指定歌曲
- token 檔案建立在你的「我的雲端硬碟根目錄」
- token 檔案不放媒體資料夾，避免資料夾分享時一起公開

## 檔案

- index.html：放 GitHub Pages
- Code.gs：放 GAS
- README.md：說明

## GAS 設定

打開 Code.gs 改：

```js
const ROOT_FOLDER_ID = 'PASTE_YOUR_DRIVE_MEDIA_FOLDER_ID_HERE';
const INITIAL_LOGIN_KEY = 'CHANGE_THIS_LOGIN_KEY';
```

然後在 GAS 執行一次：

```js
setupDriveVlcTokenFile()
```

它會建立：

```txt
_drive_vlc_private_token_store.json
```

## GitHub 設定

打開 index.html 改：

```js
GAS_API_URL: 'PASTE_YOUR_GAS_WEB_APP_EXEC_URL_HERE',
```

填你的 GAS Web App /exec 網址。

## 忘記登入密鑰

1. 在 Code.gs 改 `INITIAL_LOGIN_KEY`
2. 執行：

```js
resetDriveVlcLoginKey()
```

舊 session token 會失效，但已建立的限定播放清單不會刪掉。

## 限定網址

管理模式勾選歌曲後，按「產生限定網址」。

網址會像：

```txt
https://你的github頁面/index.html?token=pl_xxxxx
```

對方只能看到 token 對應的歌曲。
