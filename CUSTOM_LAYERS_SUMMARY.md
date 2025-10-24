# 独自レイヤー追加まとめ / Custom Layers Summary

## 概要図 / Overview Diagram

```
地理院地図アプリケーション / GSI Maps Application
├── index.html (メインアプリケーション)
└── layers_txt/ (レイヤー定義ディレクトリ)
    ├── layers.txt ★ メインファイル（他のファイルを参照）
    │   └── 参照 → layers0.txt (ベースマップ)
    │   └── 参照 → layers1.txt (年代別写真など)
    │   └── 参照 → layers2.txt (災害情報など)
    │   └── 参照 → [あなたのカスタムファイル.txt] ← ここに追加！
    │
    ├── layers_custom_example.txt (参考例)
    └── [あなたのカスタムファイル.txt] ← ここを作成！
```

## クイックリファレンス / Quick Reference

### 最小構成 / Minimal Configuration

```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "unique_id",
      "title": "表示名",
      "url": "https://example.com/tiles/{z}/{x}/{y}.png"
    }
  ]
}
```

### フル構成例 / Full Configuration Example

```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "my_layer",
      "title": "私のレイヤー",
      "iconUrl": "https://example.com/icon.png",
      "url": "https://example.com/tiles/{z}/{x}/{y}.png",
      "cocotile": true,
      "minZoom": 5,
      "maxZoom": 18,
      "maxNativeZoom": 16,
      "html": "<div class='layer_text'>説明</div>",
      "legendUrl": "https://example.com/legend.html",
      "errorTileUrl": "./image/map/no-data.png"
    }
  ]
}
```

## 手順 / Steps

### 1. レイヤー定義ファイルを作成 / Create Layer Definition File

場所 / Location: `layers_txt/layers_my_custom.txt`

```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "my_custom_layer",
      "title": "カスタムレイヤー",
      "url": "https://tile.openstreetmap.org/{z}/{x}/{y}.png",
      "minZoom": 0,
      "maxZoom": 19
    }
  ]
}
```

### 2. メインファイルに参照を追加 / Add Reference to Main File

ファイル / File: `layers_txt/layers.txt`

```json
[
  {
    "url": "./layers_my_custom.txt"  ← 追加！
  },
  {
    "url": "./layers1.txt"
  },
  ...
]
```

### 3. テスト / Test

```bash
npm start
# ブラウザで http://localhost:8080 を開く
```

## よく使うプロパティ / Common Properties

| プロパティ | 必須 | 説明 | 例 |
|----------|------|------|-----|
| type | ✅ | "Layer" または "LayerGroup" | "Layer" |
| id | ✅ | 一意の識別子 | "my_layer_001" |
| title | ✅ | 表示名 | "私のレイヤー" |
| url | ✅ | タイルURL | "https://.../tiles/{z}/{x}/{y}.png" |
| minZoom | ❌ | 最小ズーム (0-18) | 5 |
| maxZoom | ❌ | 最大ズーム (0-18) | 18 |
| cocotile | ❌ | キャッシュ使用 | true |
| html | ❌ | 説明HTML | "<div>説明</div>" |

## レイヤータイプ / Layer Types

### 1. タイルレイヤー / Tile Layer

```json
{
  "type": "Layer",
  "id": "tile_layer",
  "title": "タイルレイヤー",
  "url": "https://example.com/{z}/{x}/{y}.png"
}
```

**用途 / Use Cases:**
- PNG/JPG タイル画像
- 標準的な地図タイル
- 外部タイルサーバー

### 2. GeoJSONレイヤー / GeoJSON Layer

```json
{
  "type": "Layer",
  "id": "geojson_layer",
  "title": "GeoJSONレイヤー",
  "url": "https://example.com/{z}/{x}/{y}.geojson",
  "maxNativeZoom": 15
}
```

**用途 / Use Cases:**
- ベクトルデータ
- ポイント、ライン、ポリゴン
- 動的データ表示

### 3. レイヤーグループ / Layer Group

```json
{
  "type": "LayerGroup",
  "title": "グループ",
  "toggleall": true,
  "entries": [
    { "type": "Layer", "id": "layer1", ... },
    { "type": "Layer", "id": "layer2", ... }
  ]
}
```

**用途 / Use Cases:**
- 複数レイヤーの整理
- カテゴリ別分類
- 階層構造

## データソース例 / Data Source Examples

### OpenStreetMap

```json
{
  "url": "https://tile.openstreetmap.org/{z}/{x}/{y}.png",
  "maxZoom": 19
}
```

### カスタムタイルサーバー / Custom Tile Server

```json
{
  "url": "https://your-server.com/tiles/{z}/{x}/{y}.png",
  "minZoom": 5,
  "maxZoom": 18
}
```

### GeoJSONタイル / GeoJSON Tiles

```json
{
  "url": "https://your-server.com/vector/{z}/{x}/{y}.geojson",
  "maxNativeZoom": 15
}
```

## トラブルシューティング / Troubleshooting

### ❌ レイヤーが表示されない

1. **JSON構文チェック**
   ```bash
   python3 -m json.tool layers_txt/your_file.txt
   ```

2. **ブラウザコンソールを確認**
   - F12キーで開発者ツールを開く
   - コンソールタブでエラーを確認

3. **URLを確認**
   - タイルURLが正しいか
   - CORSが許可されているか

### ❌ サーバーが起動しない

```bash
# ポート確認
lsof -i :8080

# 再インストール
rm -rf node_modules
npm install
```

## チェックリスト / Checklist

- [ ] レイヤー定義ファイルを作成した
- [ ] JSON構文が正しい
- [ ] IDが一意である
- [ ] URLが正しい
- [ ] layers.txt に参照を追加した
- [ ] ローカルでテストした
- [ ] ブラウザコンソールにエラーがない

## リソース / Resources

### ドキュメント / Documentation
- 📖 [CUSTOM_LAYERS_GUIDE.md](CUSTOM_LAYERS_GUIDE.md) - 詳細ガイド
- 🚀 [QUICK_START_CUSTOM_LAYERS.md](QUICK_START_CUSTOM_LAYERS.md) - クイックスタート
- 📁 [layers_txt/README.md](layers_txt/README.md) - ディレクトリ説明

### 例 / Examples
- 💡 [layers_custom_example.txt](layers_txt/layers_custom_example.txt) - サンプルコード
- 🧪 [layers_test_custom.txt](layers_txt/layers_test_custom.txt) - テスト設定

### 外部リンク / External Links
- 🌐 [レイヤー定義規約](https://github.com/gsi-cyberjapan/layers-dot-txt-spec)
- 🛠️ [レイヤー編集ツール](https://gsi-cyberjapan.github.io/gsimaps/config.html)
- 🗾 [地理院地図](https://maps.gsi.go.jp/)

## FAQ

### Q1: 複数のレイヤーを一度に追加できますか？

**A:** はい。一つのファイルに複数のレイヤーを定義できます：

```json
{
  "layers": [
    { "type": "Layer", "id": "layer1", ... },
    { "type": "Layer", "id": "layer2", ... },
    { "type": "Layer", "id": "layer3", ... }
  ]
}
```

### Q2: 既存のレイヤーファイルを編集しても良いですか？

**A:** 可能ですが、新しいファイルを作成することを推奨します。既存ファイルを編集すると、リポジトリの更新時に競合が発生する可能性があります。

### Q3: GUIツールはありますか？

**A:** はい。レイヤー定義編集ツールが利用可能です：
https://gsi-cyberjapan.github.io/gsimaps/config.html

### Q4: 外部タイルサーバーを使用できますか？

**A:** はい。ただし、以下の点に注意してください：
- CORSが適切に設定されている必要があります
- サーバーの利用規約を確認してください
- 著作権表示が必要な場合があります

### Q5: ベクトルデータ（GeoJSON）も使用できますか？

**A:** はい。`url` に `.geojson` を指定してください：

```json
{
  "type": "Layer",
  "url": "https://example.com/data/{z}/{x}/{y}.geojson"
}
```

---

## 最小の例 / Minimal Example

これだけで動作します / This is all you need:

**ファイル / File:** `layers_txt/layers_hello.txt`
```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "hello_world",
      "title": "Hello World",
      "url": "https://tile.openstreetmap.org/{z}/{x}/{y}.png"
    }
  ]
}
```

**参照追加 / Add Reference:** `layers_txt/layers.txt`
```json
[
  {"url": "./layers_hello.txt"},
  {"url": "./layers1.txt"},
  ...
]
```

**完了！ / Done!** 🎉
