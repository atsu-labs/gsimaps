# 独自レイヤー追加ガイド / Custom Layers Guide

## 日本語

### 概要

地理院地図（gsimaps）では、独自のレイヤーを追加することができます。このガイドでは、カスタムレイヤーを追加する方法を説明します。

### レイヤー定義の仕組み

地理院地図のレイヤーは、JSON形式のテキストファイル（layers.txt）で定義されています。これらのファイルは `layers_txt/` ディレクトリに配置されています。

### レイヤー定義ファイルの構造

#### 基本構造

レイヤー定義ファイルは、以下の基本構造を持ちます：

```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "ユニークなID",
      "title": "レイヤーの表示名",
      "url": "タイルのURL",
      "minZoom": 最小ズームレベル,
      "maxZoom": 最大ズームレベル,
      "html": "レイヤーの説明",
      "iconUrl": "アイコンのURL（オプション）"
    }
  ]
}
```

#### レイヤータイプ

1. **Layer（レイヤー）**: 単一のタイルレイヤー
2. **LayerGroup（レイヤーグループ）**: 複数のレイヤーをグループ化

### 独自レイヤーの追加方法

#### 方法1: 新しいレイヤー定義ファイルを作成

1. `layers_txt/` ディレクトリに新しいファイルを作成します（例：`layers_custom.txt`）

2. レイヤーを定義します：

```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "my_custom_layer",
      "title": "私のカスタムレイヤー",
      "url": "https://example.com/tiles/{z}/{x}/{y}.png",
      "minZoom": 0,
      "maxZoom": 18,
      "html": "<div class='layer_text'>これはカスタムレイヤーです。</div>"
    }
  ]
}
```

3. `layers_txt/layers.txt` に新しいファイルへの参照を追加します：

```json
[
  {
    "url": "./layers_custom.txt"
  },
  {
    "url": "./layers1.txt"
  },
  ...
]
```

#### 方法2: 既存のレイヤー定義ファイルに追加

既存のレイヤー定義ファイル（例：`layers1.txt`）を編集して、新しいレイヤーを追加することもできます。

### レイヤー定義の例

#### 基本的なタイルレイヤー

```json
{
  "type": "Layer",
  "id": "my_tile_layer",
  "title": "タイルレイヤーの例",
  "url": "https://example.com/tiles/{z}/{x}/{y}.png",
  "cocotile": true,
  "minZoom": 5,
  "maxZoom": 18,
  "html": "<div class='layer_text'>説明文</div>",
  "legendUrl": "https://example.com/legend.html",
  "errorTileUrl": "./image/map/no-data.png"
}
```

#### レイヤーグループ

```json
{
  "type": "LayerGroup",
  "title": "カスタムレイヤーグループ",
  "iconUrl": "https://example.com/icon.png",
  "toggleall": false,
  "html": "<div class='layer_text'>このグループには複数のレイヤーが含まれます。</div>",
  "entries": [
    {
      "type": "Layer",
      "id": "layer1",
      "title": "レイヤー1",
      "url": "https://example.com/layer1/{z}/{x}/{y}.png",
      "minZoom": 0,
      "maxZoom": 18
    },
    {
      "type": "Layer",
      "id": "layer2",
      "title": "レイヤー2",
      "url": "https://example.com/layer2/{z}/{x}/{y}.png",
      "minZoom": 0,
      "maxZoom": 18
    }
  ]
}
```

#### GeoJSONレイヤー

```json
{
  "type": "Layer",
  "id": "geojson_layer",
  "title": "GeoJSONレイヤー",
  "url": "https://example.com/data/{z}/{x}/{y}.geojson",
  "cocotile": true,
  "minZoom": 10,
  "maxZoom": 18,
  "maxNativeZoom": 15
}
```

### 重要なプロパティ

- **id**: レイヤーの一意の識別子（必須）
- **title**: レイヤーの表示名（必須）
- **url**: タイルまたはデータのURL（必須）
  - `{z}`: ズームレベル
  - `{x}`: タイルのX座標
  - `{y}`: タイルのY座標
- **type**: "Layer" または "LayerGroup"（必須）
- **minZoom**: 最小ズームレベル（オプション、デフォルト: 0）
- **maxZoom**: 最大ズームレベル（オプション、デフォルト: 18）
- **maxNativeZoom**: ネイティブタイルの最大ズームレベル（オプション）
- **cocotile**: タイルキャッシュを使用するか（オプション、デフォルト: false）
- **html**: レイヤーの説明HTML（オプション）
- **legendUrl**: 凡例ページのURL（オプション）
- **iconUrl**: レイヤーアイコンのURL（オプション）
- **errorTileUrl**: エラータイルの画像URL（オプション）
- **toggleall**: グループ内の全レイヤーを一括切り替えボタンを表示（LayerGroupのみ、オプション）
- **entries**: 子レイヤーの配列（LayerGroupのみ、必須）

### レイヤー定義編集ツール

地理院地図には、レイヤー定義ファイルを編集するためのWebツールが含まれています：

https://gsi-cyberjapan.github.io/gsimaps/config.html

このツールを使用すると、GUIでレイヤー定義を作成・編集できます。

### テストとデバッグ

1. ローカルWebサーバーを起動します：
```bash
npm start
```

2. ブラウザで `http://localhost:8080` を開きます

3. 地図上で新しいレイヤーが表示されることを確認します

4. ブラウザの開発者ツールのコンソールでエラーを確認します

### 注意事項

- レイヤーIDは一意である必要があります
- URLは有効なタイルサーバーを指している必要があります
- 外部タイルサーバーを使用する場合は、CORSの設定に注意してください
- タイルのズームレベル範囲が適切に設定されていることを確認してください

### 参考資料

- レイヤー定義規約: https://github.com/gsi-cyberjapan/layers-dot-txt-spec
- 地理院地図: https://maps.gsi.go.jp/
- 地理院地図デモ: https://gsi-cyberjapan.github.io/gsimaps/

---

## English

### Overview

GSI Maps (gsimaps) allows you to add custom layers. This guide explains how to add custom layers to the application.

### How Layer Definitions Work

Layers in GSI Maps are defined in JSON text files (layers.txt) located in the `layers_txt/` directory.

### Layer Definition File Structure

#### Basic Structure

A layer definition file has the following basic structure:

```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "unique_id",
      "title": "Layer Display Name",
      "url": "Tile URL",
      "minZoom": minimum zoom level,
      "maxZoom": maximum zoom level,
      "html": "Layer description",
      "iconUrl": "Icon URL (optional)"
    }
  ]
}
```

#### Layer Types

1. **Layer**: A single tile layer
2. **LayerGroup**: Groups multiple layers together

### How to Add Custom Layers

#### Method 1: Create a New Layer Definition File

1. Create a new file in the `layers_txt/` directory (e.g., `layers_custom.txt`)

2. Define your layers:

```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "my_custom_layer",
      "title": "My Custom Layer",
      "url": "https://example.com/tiles/{z}/{x}/{y}.png",
      "minZoom": 0,
      "maxZoom": 18,
      "html": "<div class='layer_text'>This is a custom layer.</div>"
    }
  ]
}
```

3. Add a reference to your new file in `layers_txt/layers.txt`:

```json
[
  {
    "url": "./layers_custom.txt"
  },
  {
    "url": "./layers1.txt"
  },
  ...
]
```

#### Method 2: Add to an Existing Layer Definition File

You can also edit an existing layer definition file (e.g., `layers1.txt`) to add new layers.

### Layer Definition Examples

#### Basic Tile Layer

```json
{
  "type": "Layer",
  "id": "my_tile_layer",
  "title": "Tile Layer Example",
  "url": "https://example.com/tiles/{z}/{x}/{y}.png",
  "cocotile": true,
  "minZoom": 5,
  "maxZoom": 18,
  "html": "<div class='layer_text'>Description text</div>",
  "legendUrl": "https://example.com/legend.html",
  "errorTileUrl": "./image/map/no-data.png"
}
```

#### Layer Group

```json
{
  "type": "LayerGroup",
  "title": "Custom Layer Group",
  "iconUrl": "https://example.com/icon.png",
  "toggleall": false,
  "html": "<div class='layer_text'>This group contains multiple layers.</div>",
  "entries": [
    {
      "type": "Layer",
      "id": "layer1",
      "title": "Layer 1",
      "url": "https://example.com/layer1/{z}/{x}/{y}.png",
      "minZoom": 0,
      "maxZoom": 18
    },
    {
      "type": "Layer",
      "id": "layer2",
      "title": "Layer 2",
      "url": "https://example.com/layer2/{z}/{x}/{y}.png",
      "minZoom": 0,
      "maxZoom": 18
    }
  ]
}
```

#### GeoJSON Layer

```json
{
  "type": "Layer",
  "id": "geojson_layer",
  "title": "GeoJSON Layer",
  "url": "https://example.com/data/{z}/{x}/{y}.geojson",
  "cocotile": true,
  "minZoom": 10,
  "maxZoom": 18,
  "maxNativeZoom": 15
}
```

### Important Properties

- **id**: Unique identifier for the layer (required)
- **title**: Display name of the layer (required)
- **url**: URL for tiles or data (required)
  - `{z}`: Zoom level
  - `{x}`: Tile X coordinate
  - `{y}`: Tile Y coordinate
- **type**: "Layer" or "LayerGroup" (required)
- **minZoom**: Minimum zoom level (optional, default: 0)
- **maxZoom**: Maximum zoom level (optional, default: 18)
- **maxNativeZoom**: Maximum zoom level of native tiles (optional)
- **cocotile**: Whether to use tile caching (optional, default: false)
- **html**: Description HTML for the layer (optional)
- **legendUrl**: URL to legend page (optional)
- **iconUrl**: URL for layer icon (optional)
- **errorTileUrl**: URL for error tile image (optional)
- **toggleall**: Show toggle all button for group (LayerGroup only, optional)
- **entries**: Array of child layers (LayerGroup only, required)

### Layer Definition Editing Tool

GSI Maps includes a web tool for editing layer definition files:

https://gsi-cyberjapan.github.io/gsimaps/config.html

This tool allows you to create and edit layer definitions using a GUI.

### Testing and Debugging

1. Start a local web server:
```bash
npm start
```

2. Open `http://localhost:8080` in your browser

3. Verify that your new layer appears on the map

4. Check the browser's developer console for any errors

### Important Notes

- Layer IDs must be unique
- URLs must point to valid tile servers
- When using external tile servers, pay attention to CORS settings
- Ensure that tile zoom level ranges are properly configured

### References

- Layer Definition Specifications: https://github.com/gsi-cyberjapan/layers-dot-txt-spec
- GSI Maps: https://maps.gsi.go.jp/
- GSI Maps Demo: https://gsi-cyberjapan.github.io/gsimaps/
