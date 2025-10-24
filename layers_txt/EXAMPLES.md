# レイヤー定義の実例集 / Layer Definition Examples

このファイルには、実際に使えるレイヤー定義の例を掲載しています。

## 目次 / Contents

1. [基本的なタイルレイヤー](#1-基本的なタイルレイヤー)
2. [OpenStreetMapの利用](#2-openstreetmapの利用)
3. [GeoJSONベクトルデータ](#3-geojsonベクトルデータ)
4. [レイヤーグループ](#4-レイヤーグループ)
5. [ズームレベル制限](#5-ズームレベル制限)
6. [著作権表示付きレイヤー](#6-著作権表示付きレイヤー)
7. [複数レイヤーの定義](#7-複数レイヤーの定義)

---

## 1. 基本的なタイルレイヤー

最もシンプルなタイルレイヤーの定義です。

```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "simple_tile_layer",
      "title": "シンプルなタイルレイヤー",
      "url": "https://your-tile-server.com/tiles/{z}/{x}/{y}.png"
    }
  ]
}
```

**用途:**
- 自社で運用しているタイルサーバー
- シンプルな地図タイル
- 基本的な実装

---

## 2. OpenStreetMapの利用

OpenStreetMapのタイルを表示する例です。

```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "openstreetmap",
      "title": "OpenStreetMap",
      "url": "https://tile.openstreetmap.org/{z}/{x}/{y}.png",
      "minZoom": 0,
      "maxZoom": 19,
      "html": "<div class='layer_text'>OpenStreetMapは、誰でも自由に地図を使えるよう、オープンデータの地図を作るプロジェクトです。</div><div class='gsi_layerinfo_copy'>© OpenStreetMap contributors</div>"
    }
  ]
}
```

**注意点:**
- OpenStreetMapの利用規約を必ず確認してください
- 著作権表示は必須です
- 大量アクセスの場合は独自のタイルサーバーを検討してください

---

## 3. GeoJSONベクトルデータ

ポイント、ライン、ポリゴンなどのベクトルデータを表示します。

```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "vector_data",
      "title": "ベクトルデータレイヤー",
      "url": "https://your-server.com/data/{z}/{x}/{y}.geojson",
      "minZoom": 10,
      "maxZoom": 18,
      "maxNativeZoom": 15,
      "html": "<div class='layer_text'>このレイヤーはGeoJSON形式のベクトルデータを表示します。<br>ズームレベル10以上で表示されます。</div>"
    }
  ]
}
```

**用途:**
- 施設のポイントデータ
- 道路や河川のライン
- 行政区域などのポリゴン
- リアルタイムデータの表示

---

## 4. レイヤーグループ

関連するレイヤーをグループ化します。

```json
{
  "layers": [
    {
      "type": "LayerGroup",
      "title": "交通情報",
      "iconUrl": "https://example.com/icons/traffic.png",
      "toggleall": true,
      "html": "<div class='layer_text'>交通に関する情報をまとめて表示します。</div>",
      "entries": [
        {
          "type": "Layer",
          "id": "roads",
          "title": "道路",
          "url": "https://example.com/roads/{z}/{x}/{y}.png",
          "minZoom": 10,
          "maxZoom": 18
        },
        {
          "type": "Layer",
          "id": "railways",
          "title": "鉄道",
          "url": "https://example.com/railways/{z}/{x}/{y}.png",
          "minZoom": 10,
          "maxZoom": 18
        },
        {
          "type": "Layer",
          "id": "stations",
          "title": "駅",
          "url": "https://example.com/stations/{z}/{x}/{y}.geojson",
          "minZoom": 12,
          "maxZoom": 18
        }
      ]
    }
  ]
}
```

**機能:**
- `toggleall: true` で全レイヤーの一括切り替え
- 階層的な整理が可能
- グループごとの説明を付与

---

## 5. ズームレベル制限

特定のズームレベルでのみ表示されるレイヤーです。

```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "detailed_layer",
      "title": "詳細レイヤー（拡大時のみ表示）",
      "url": "https://example.com/detailed/{z}/{x}/{y}.png",
      "minZoom": 14,
      "maxZoom": 18,
      "html": "<div class='layer_text'>このレイヤーはズームレベル14以上で表示されます。<br>詳細な情報を含むため、広域表示では非表示となります。</div>"
    }
  ]
}
```

**用途:**
- 詳細な建物データ（高ズーム時のみ）
- 広域の概要データ（低ズーム時のみ）
- データ量の最適化

---

## 6. 著作権表示付きレイヤー

データソースの著作権を明記したレイヤーです。

```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "satellite_imagery",
      "title": "衛星画像",
      "url": "https://example.com/satellite/{z}/{x}/{y}.jpg",
      "cocotile": true,
      "minZoom": 5,
      "maxZoom": 18,
      "html": "<div class='layer_text'><p>高解像度の衛星画像です。</p><p>撮影日：2024年10月</p></div><div class='gsi_layerinfo_copy'>© Your Organization Name<br>データ提供：Satellite Provider Inc.</div>",
      "legendUrl": "https://example.com/satellite/legend.html"
    }
  ]
}
```

**重要:**
- 著作権情報は必ず記載してください
- データ提供元の利用規約を確認してください
- 凡例ページがある場合は `legendUrl` を設定

---

## 7. 複数レイヤーの定義

一つのファイルに複数のレイヤーを定義する例です。

```json
{
  "layers": [
    {
      "type": "LayerGroup",
      "title": "自治体データ",
      "toggleall": false,
      "html": "<div class='layer_text'>地方自治体が提供するオープンデータです。</div>",
      "entries": [
        {
          "type": "Layer",
          "id": "city_facilities",
          "title": "公共施設",
          "url": "https://city.example.com/facilities/{z}/{x}/{y}.geojson",
          "minZoom": 12,
          "maxZoom": 18,
          "html": "市内の公共施設の位置を表示します。"
        },
        {
          "type": "Layer",
          "id": "city_parks",
          "title": "公園",
          "url": "https://city.example.com/parks/{z}/{x}/{y}.geojson",
          "minZoom": 13,
          "maxZoom": 18,
          "html": "市内の公園の位置と範囲を表示します。"
        },
        {
          "type": "Layer",
          "id": "city_hazard",
          "title": "ハザードマップ",
          "url": "https://city.example.com/hazard/{z}/{x}/{y}.png",
          "minZoom": 10,
          "maxZoom": 18,
          "html": "<div class='layer_text'>洪水・土砂災害のハザードマップです。<br>避難計画の参考にしてください。</div>"
        }
      ]
    }
  ]
}
```

---

## 実践例：災害情報レイヤー

実際の運用を想定した、災害情報レイヤーの完全な例です。

```json
{
  "layers": [
    {
      "type": "LayerGroup",
      "title": "災害情報（2024年10月）",
      "iconUrl": "https://maps.gsi.go.jp/portal/sys/v4/symbols/600.png",
      "toggleall": true,
      "html": "<div class='layer_text'><p>2024年10月の災害に関する情報です。</p><p>最終更新：2024年10月23日</p></div>",
      "entries": [
        {
          "type": "Layer",
          "id": "disaster_2024_10_affected_areas",
          "title": "被災地域",
          "url": "https://disaster-info.example.com/affected/{z}/{x}/{y}.geojson",
          "minZoom": 8,
          "maxZoom": 18,
          "html": "<div class='layer_text'>被災した地域を表示します。<br>クリックで詳細情報を確認できます。</div>"
        },
        {
          "type": "Layer",
          "id": "disaster_2024_10_shelters",
          "title": "避難所",
          "iconUrl": "https://maps.gsi.go.jp/portal/sys/v4/symbols/601.png",
          "url": "https://disaster-info.example.com/shelters/{z}/{x}/{y}.geojson",
          "minZoom": 10,
          "maxZoom": 18,
          "html": "<div class='layer_text'>開設中の避難所を表示します。<br>⚠️ 最新情報は自治体HPを確認してください。</div>"
        },
        {
          "type": "Layer",
          "id": "disaster_2024_10_aerial_photo",
          "title": "災害後の航空写真",
          "url": "https://disaster-info.example.com/photos/{z}/{x}/{y}.jpg",
          "cocotile": true,
          "minZoom": 14,
          "maxZoom": 18,
          "html": "<div class='layer_text'><p>災害発生後に撮影された航空写真です。</p><p>撮影日：2024年10月15日</p></div><div class='gsi_layerinfo_copy'>©災害対策本部</div>",
          "legendUrl": "https://disaster-info.example.com/legend.html"
        }
      ]
    }
  ]
}
```

---

## プロパティの詳細説明

### 必須プロパティ

| プロパティ | 説明 | 例 |
|----------|------|-----|
| type | レイヤーの種類 | "Layer" または "LayerGroup" |
| id | 一意の識別子（Layerのみ） | "my_layer_001" |
| title | 表示名 | "私のレイヤー" |
| url | データのURL（Layerのみ） | "https://example.com/{z}/{x}/{y}.png" |

### オプションプロパティ

| プロパティ | 説明 | デフォルト | 例 |
|----------|------|----------|-----|
| minZoom | 最小ズームレベル | 0 | 5 |
| maxZoom | 最大ズームレベル | 18 | 18 |
| maxNativeZoom | ネイティブタイルの最大ズーム | maxZoom | 15 |
| cocotile | タイルキャッシュを使用 | false | true |
| html | 説明HTML | - | "\<div\>説明\</div\>" |
| iconUrl | アイコンURL | - | "https://example.com/icon.png" |
| legendUrl | 凡例ページURL | - | "https://example.com/legend.html" |
| errorTileUrl | エラー時の画像URL | - | "./image/no-data.png" |
| toggleall | 一括切り替え（GroupOnly） | false | true |
| entries | 子レイヤー配列（GroupOnly） | - | [...] |

---

## ベストプラクティス

### ✅ 推奨事項

1. **IDは分かりやすく一意に**
   ```json
   "id": "myorg_2024_roads"  // ✅ 良い例
   "id": "layer1"             // ❌ 避けるべき
   ```

2. **説明を詳しく記載**
   ```json
   "html": "<div class='layer_text'><p>詳細な説明</p><p>更新日：2024/10/23</p></div>"
   ```

3. **著作権情報は必須**
   ```json
   "html": "...<div class='gsi_layerinfo_copy'>© データ提供元</div>"
   ```

4. **適切なズーム範囲を設定**
   ```json
   "minZoom": 10,  // 詳細データは高ズームのみ
   "maxZoom": 18
   ```

### ⚠️ 注意事項

1. JSONの構文エラーに注意
2. URLのエスケープ処理
3. CORSの設定確認
4. データ量とパフォーマンス
5. ライセンスと利用規約の確認

---

## テンプレート

コピー＆ペーストして使えるテンプレートです。

### シンプルなタイルレイヤー

```json
{
  "layers": [
    {
      "type": "Layer",
      "id": "YOUR_LAYER_ID",
      "title": "YOUR_LAYER_TITLE",
      "url": "YOUR_TILE_URL/{z}/{x}/{y}.png",
      "minZoom": 0,
      "maxZoom": 18,
      "html": "<div class='layer_text'>YOUR_DESCRIPTION</div>"
    }
  ]
}
```

### レイヤーグループ

```json
{
  "layers": [
    {
      "type": "LayerGroup",
      "title": "YOUR_GROUP_TITLE",
      "toggleall": true,
      "html": "<div class='layer_text'>YOUR_GROUP_DESCRIPTION</div>",
      "entries": [
        {
          "type": "Layer",
          "id": "YOUR_LAYER_1_ID",
          "title": "YOUR_LAYER_1_TITLE",
          "url": "YOUR_LAYER_1_URL/{z}/{x}/{y}.png"
        }
      ]
    }
  ]
}
```

---

## さらに詳しく

- 📖 [CUSTOM_LAYERS_GUIDE.md](../CUSTOM_LAYERS_GUIDE.md) - 包括的なガイド
- 🚀 [QUICK_START_CUSTOM_LAYERS.md](../QUICK_START_CUSTOM_LAYERS.md) - クイックスタート
- 📊 [CUSTOM_LAYERS_SUMMARY.md](../CUSTOM_LAYERS_SUMMARY.md) - まとめ
- 💡 [layers_custom_example.txt](./layers_custom_example.txt) - 実際に動作する例
