# レイヤー定義ファイルディレクトリ / Layer Definition Files Directory

## 日本語

### 概要

このディレクトリには、地理院地図で使用されるレイヤー定義ファイルが含まれています。

### ファイル構成

- **layers.txt**: メインのレイヤー定義ファイル。他のレイヤー定義ファイルへの参照を含みます。
- **layers0.txt**: ベースマップ（標準地図、淡色地図など）の定義
- **layers1.txt - layers7.txt**: 各種レイヤーカテゴリの定義
- **layers_topic_*.txt**: トピック別のレイヤー定義（災害情報など）
- **layers_custom_example.txt**: カスタムレイヤーの例（参考用）

### カスタムレイヤーの追加方法

#### ステップ1: レイヤー定義ファイルを作成

このディレクトリに新しいファイルを作成します（例：`layers_custom.txt`）。

```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "my_custom_layer",
      "title": "私のカスタムレイヤー",
      "url": "https://example.com/tiles/{z}/{x}/{y}.png",
      "minZoom": 0,
      "maxZoom": 18
    }
  ]
}
```

#### ステップ2: layers.txt に参照を追加

`layers.txt` を編集して、新しいファイルへの参照を追加します：

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

### ファイル形式

すべてのレイヤー定義ファイルはJSON形式です。以下の要素を含むことができます：

- **Layer**: 単一のタイルレイヤー
- **LayerGroup**: 複数のレイヤーをグループ化

### 参考例

- **`layers_custom_example.txt`** - 実際に動作するサンプルコード
- **`EXAMPLES.md`** - 実践的な例とテンプレート集

これらの例には以下が含まれています：

- 基本的なタイルレイヤー
- GeoJSONレイヤー
- 外部タイルサーバー（OpenStreetMapなど）
- ネストされたレイヤーグループ
- 災害情報レイヤーなどの実践例

### より詳しい情報

カスタムレイヤーの追加に関する詳細なガイドは、リポジトリルートの `CUSTOM_LAYERS_GUIDE.md` をご覧ください。

### レイヤー定義の編集ツール

Webベースの編集ツールが利用可能です：
https://gsi-cyberjapan.github.io/gsimaps/config.html

---

## English

### Overview

This directory contains layer definition files used by GSI Maps.

### File Structure

- **layers.txt**: Main layer definition file. Contains references to other layer definition files.
- **layers0.txt**: Base map definitions (standard map, pale map, etc.)
- **layers1.txt - layers7.txt**: Definitions for various layer categories
- **layers_topic_*.txt**: Topic-specific layer definitions (disaster information, etc.)
- **layers_custom_example.txt**: Example custom layers (for reference)

### How to Add Custom Layers

#### Step 1: Create a Layer Definition File

Create a new file in this directory (e.g., `layers_custom.txt`).

```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "my_custom_layer",
      "title": "My Custom Layer",
      "url": "https://example.com/tiles/{z}/{x}/{y}.png",
      "minZoom": 0,
      "maxZoom": 18
    }
  ]
}
```

#### Step 2: Add Reference in layers.txt

Edit `layers.txt` to add a reference to your new file:

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

### File Format

All layer definition files are in JSON format. They can contain:

- **Layer**: A single tile layer
- **LayerGroup**: Groups multiple layers together

### Reference Examples

- **`layers_custom_example.txt`** - Working sample code
- **`EXAMPLES.md`** - Practical examples and templates

These examples include:

- Basic tile layers
- GeoJSON layers
- External tile servers (OpenStreetMap, etc.)
- Nested layer groups
- Real-world examples like disaster information layers

### More Information

For a detailed guide on adding custom layers, see `CUSTOM_LAYERS_GUIDE.md` in the repository root.

### Layer Definition Editing Tool

A web-based editing tool is available at:
https://gsi-cyberjapan.github.io/gsimaps/config.html
