# クイックスタート：独自レイヤーのテスト / Quick Start: Testing Custom Layers

## 日本語

### 前提条件

- Node.js がインストールされていること
- このリポジトリをクローンまたはダウンロード済みであること

### ステップ1: 依存パッケージのインストール

```bash
cd /path/to/gsimaps
npm install
```

### ステップ2: 開発サーバーの起動

```bash
npm start
```

サーバーが起動したら、ブラウザで以下のURLにアクセスします：
```
http://localhost:8080
```

### ステップ3: カスタムレイヤーの例を確認

このリポジトリには、カスタムレイヤーの例が含まれています：

```
layers_txt/layers_custom_example.txt
```

この例には以下が含まれています：
- 基本的なタイルレイヤー
- GeoJSONレイヤー
- 外部タイルサーバー（OpenStreetMap）の例
- ネストされたレイヤーグループ

### ステップ4: カスタムレイヤーを有効化（オプション）

カスタムレイヤーの例を地理院地図で表示するには：

1. `layers_txt/layers.txt` を編集
2. ファイルの先頭に以下を追加：
```json
{
  "url": "./layers_custom_example.txt"
},
```

3. ブラウザをリロード
4. 「情報」→「カスタムレイヤーの例」を確認

### ステップ5: 独自のカスタムレイヤーを作成

1. `layers_txt/` ディレクトリに新しいファイルを作成（例：`layers_my_custom.txt`）

2. レイヤーを定義：
```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "my_layer",
      "title": "私のレイヤー",
      "url": "https://your-tile-server.com/{z}/{x}/{y}.png",
      "minZoom": 0,
      "maxZoom": 18
    }
  ]
}
```

3. `layers_txt/layers.txt` に参照を追加：
```json
[
  {
    "url": "./layers_my_custom.txt"
  },
  ...
]
```

4. ブラウザをリロードして確認

### トラブルシューティング

#### レイヤーが表示されない場合

1. ブラウザの開発者ツールを開く（F12キー）
2. コンソールタブでエラーメッセージを確認
3. ネットワークタブで失敗したリクエストを確認
4. JSON構文が正しいか確認：
```bash
python3 -m json.tool layers_txt/your_file.txt
```

#### サーバーが起動しない場合

1. ポート8080が既に使用されていないか確認
2. Node.jsのバージョンを確認（推奨: v14以上）
3. `node_modules` を削除して再インストール：
```bash
rm -rf node_modules
npm install
```

### 詳細なドキュメント

詳しい情報は以下を参照してください：
- [CUSTOM_LAYERS_GUIDE.md](CUSTOM_LAYERS_GUIDE.md) - 包括的なガイド
- [layers_txt/README.md](layers_txt/README.md) - layers_txt ディレクトリの説明
- https://github.com/gsi-cyberjapan/layers-dot-txt-spec - レイヤー定義規約

---

## English

### Prerequisites

- Node.js installed
- This repository cloned or downloaded

### Step 1: Install Dependencies

```bash
cd /path/to/gsimaps
npm install
```

### Step 2: Start the Development Server

```bash
npm start
```

Once the server starts, open your browser and navigate to:
```
http://localhost:8080
```

### Step 3: Check the Custom Layer Examples

This repository includes custom layer examples:

```
layers_txt/layers_custom_example.txt
```

This example includes:
- Basic tile layers
- GeoJSON layers
- External tile server example (OpenStreetMap)
- Nested layer groups

### Step 4: Enable Custom Layers (Optional)

To display the custom layer examples in GSI Maps:

1. Edit `layers_txt/layers.txt`
2. Add the following at the beginning of the file:
```json
{
  "url": "./layers_custom_example.txt"
},
```

3. Reload your browser
4. Check "Information" → "Custom Layer Examples"

### Step 5: Create Your Own Custom Layers

1. Create a new file in the `layers_txt/` directory (e.g., `layers_my_custom.txt`)

2. Define your layers:
```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "my_layer",
      "title": "My Layer",
      "url": "https://your-tile-server.com/{z}/{x}/{y}.png",
      "minZoom": 0,
      "maxZoom": 18
    }
  ]
}
```

3. Add a reference in `layers_txt/layers.txt`:
```json
[
  {
    "url": "./layers_my_custom.txt"
  },
  ...
]
```

4. Reload your browser and verify

### Troubleshooting

#### Layers Not Displaying

1. Open browser developer tools (F12 key)
2. Check console tab for error messages
3. Check network tab for failed requests
4. Verify JSON syntax is correct:
```bash
python3 -m json.tool layers_txt/your_file.txt
```

#### Server Won't Start

1. Check if port 8080 is already in use
2. Verify Node.js version (recommended: v14 or higher)
3. Remove `node_modules` and reinstall:
```bash
rm -rf node_modules
npm install
```

### Detailed Documentation

For more information, please refer to:
- [CUSTOM_LAYERS_GUIDE.md](CUSTOM_LAYERS_GUIDE.md) - Comprehensive guide
- [layers_txt/README.md](layers_txt/README.md) - layers_txt directory description
- https://github.com/gsi-cyberjapan/layers-dot-txt-spec - Layer definition specifications
