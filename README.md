教學文:
https://ithelp.ithome.com.tw/articles/10216236

這個程式可以用來獲得 LINE 官方帳號好友的 user id

聊天機器人的 qr code:
<img src="https://qr-official.line.me/sid/L/755qerhg.png"></img>

# 使用方法:

1. 首先要建立一個 LINE 官方帳號管理頁面的帳號
2. 建立 channel(channel 就是官方帳號)
3. 複製 channelAccessToken 與 channelSecret 到 env.sh
4. \$ npm start
5. 開啟另外一個 terminal，執行 \$ ngrok http 1234 (建立一個臨時伺服器，7~8 小時會失效)
6. 複製顯示在 terminal 的網址，並且加上/callback: https://308e7bc8109e.ngrok.io/callback
7. 貼在 LINE 官方帳號管理頁面的 設定->Messaging API->Webhook 網址
8. 設定->回應設定->回應模式把 聊天機器人 & Webhook 打勾
9. 用 LINE 加入你第一步建立的 channel，並且隨便發一個訊息
10. 假如有人傳訊息，index.js 內的 handleEvent 函式會收到 event，資料結構如下:

```json
{
  "type": "message",
  "replyToken": "1cdabb80b237457d94ccc8e866308986",
  "source": {
    "userId": "U12cf5a7d53acb513bbe5498aeb1b46a5",
    "type": "user"
  },
  "timestamp": 1600511373898,
  "mode": "active",
  "message": {
    "type": "text",
    "id": "12707100757790",
    "text": "你好"
  }
}
```

11. 可以用 event.source.userId 去獲得 userId
