# Drive VLC Secure Player｜試算表設定 + 按鈕修正版

## 修正內容

這版修正前一版「按鈕失效」問題。原因是前端 JS 裡的按鈕字串引號衝突，導致整段 JavaScript 沒有執行。

這版也改成：

- 不需要在 `Code.gs` 填 `INITIAL_LOGIN_KEY`
- 管理登入密鑰放在試算表「系統設定」的 `admin_login_key`
- 預設管理密鑰：`123456`
- 限定播放清單網址放在試算表「播放清單網址管理」
- 前端按鈕改成 `addEventListener`，不再用容易壞掉的 inline onclick 字串

## 已預填

GAS_API_URL：

```txt
https://script.google.com/macros/s/AKfycbziC1SpE1GgYdGLPKTigihBL6DZhIccS7dkAUI9ZFrzZFgDpvEs3-diWm4kviaLgn-U/exec
```

ROOT_FOLDER_ID：

```txt
1z4K04Dt6irjsgNrtcaoGC6H6e7YVIlmW
```

## 更新步驟

1. 用這包的 `Code.gs` 覆蓋 GAS。
2. 儲存。
3. 執行：

```js
setupDriveVlcSystem()
```

4. 重新部署 GAS Web App。
5. 用這包的 `index.html` 覆蓋 GitHub Pages。
6. 打開：

```txt
https://edn869728-jpg.github.io/drive-vlc-secure-player/?admin=1&v=fix1
```

## 登入密鑰在哪裡

執行 `setupDriveVlcSystem()` 後會建立試算表：

```txt
Drive VLC 系統設定與播放清單管理
```

裡面有工作表：

```txt
系統設定
```

找到：

```txt
admin_login_key
```

預設值是：

```txt
123456
```

你可以直接在試算表改成自己的密鑰。

## 關掉網址

工作表：

```txt
播放清單網址管理
```

把該列的 `status` 改成：

```txt
disabled
```

該分享網址就會失效。


## Token 直進修正

這版已修正：

```txt
https://edn869728-jpg.github.io/drive-vlc-secure-player/#session=sess_xxxxx
```

會直接進管理頁，不會再要求輸入管理密鑰。

規則：

```txt
沒有 sessionToken → 才顯示管理登入
有 sessionToken → 直接進管理頁
sessionToken 過期或無效 → 才重新登入
```

更新後請用清快取網址測試：

```txt
https://edn869728-jpg.github.io/drive-vlc-secure-player/?admin=1&v=directfix1
```
