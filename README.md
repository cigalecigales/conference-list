# :blush: conference-list

:yellow_heart: [conference-list.com](http://conference-list.com/)

## :blush: About
日本国内で開催されるカンファレンス等の大型イベント一覧用のウェブサイトです。

## :blush: Contribute
カンファレンス情報を `src/data/items.json` に追記してプルリクエストをお願いします。

```js
[
  // ...省略
  {
    "id": 22, // 既存データのidの最大値＋1
    "name": "Sample Conference 20XX", // カンファレンス名
    "eventDate": ["2099/01/01", "2099/01/02", "2099/01/03"], // 開催日
    "url": "http://example.com", // ウェブサイトのURL
    "description": "○○の情報を共有するためのカンファレンス。", // カンファレンスの説明
    "tags": ["sample"] // タグ
  }
]
```

