# 独自レイヤー追加ガイド - 目次 / Custom Layers Documentation Index

このドキュメント群は、地理院地図（gsimaps）に独自のレイヤーを追加する方法を説明しています。

---

## 🚀 初めての方へ / Getting Started

まずはこちらから：

1. **[クイックスタートガイド](QUICK_START_CUSTOM_LAYERS.md)** 📖
   - 5分で始められる手順
   - サーバーの起動方法
   - 最初のカスタムレイヤーを追加
   - すぐに試せるサンプルコード

2. **[まとめ（1ページ）](CUSTOM_LAYERS_SUMMARY.md)** 📄
   - 図解でわかりやすい
   - 最小構成の例
   - よく使うプロパティ一覧
   - チェックリスト

---

## 📚 詳細ドキュメント / Detailed Documentation

### 包括的なガイド

**[カスタムレイヤー追加ガイド](CUSTOM_LAYERS_GUIDE.md)** 📘
- レイヤー定義の仕組み（日本語・英語）
- ファイル構造の詳細説明
- プロパティの完全リファレンス
- テストとデバッグの方法
- ベストプラクティス

### 実践例集

**[実例とテンプレート集](layers_txt/EXAMPLES.md)** 💡
- 基本的なタイルレイヤー
- OpenStreetMapの利用
- GeoJSONベクトルデータ
- レイヤーグループの作成
- ズームレベル制限
- 著作権表示付きレイヤー
- 災害情報レイヤー（実践例）
- コピー＆ペーストできるテンプレート

---

## 📁 サンプルファイル / Sample Files

### すぐに使えるサンプル

| ファイル | 説明 | 用途 |
|---------|------|------|
| [layers_custom_example.txt](layers_txt/layers_custom_example.txt) | 動作するサンプルコード | 参考にする |
| [layers_test_custom.txt](layers_txt/layers_test_custom.txt) | テスト設定 | 動作確認 |

### ディレクトリガイド

**[layers_txt/README.md](layers_txt/README.md)**
- ディレクトリ構成の説明
- ファイルの役割
- クイックリファレンス

---

## 🎯 目的別ガイド / Guide by Purpose

### はじめて追加する場合

1. [クイックスタート](QUICK_START_CUSTOM_LAYERS.md) を読む
2. [サンプルファイル](layers_txt/layers_custom_example.txt) を見る
3. [基本例](layers_txt/EXAMPLES.md#1-基本的なタイルレイヤー) を使う
4. テストする

### 詳しく知りたい場合

1. [包括的ガイド](CUSTOM_LAYERS_GUIDE.md) を読む
2. [実践例集](layers_txt/EXAMPLES.md) を参照
3. プロパティリファレンスを確認

### トラブルシューティング

1. [まとめ](CUSTOM_LAYERS_SUMMARY.md#トラブルシューティング--troubleshooting) のトラブルシューティング
2. [クイックスタート](QUICK_START_CUSTOM_LAYERS.md#トラブルシューティング) の解決方法
3. [FAQ](CUSTOM_LAYERS_SUMMARY.md#faq)

---

## 📖 ドキュメント一覧 / Documentation List

### メインドキュメント

| 文書 | サイズ | 対象 | 内容 |
|-----|-------|------|------|
| [QUICK_START_CUSTOM_LAYERS.md](QUICK_START_CUSTOM_LAYERS.md) | 5.1KB | 初心者 | 5分で始められるチュートリアル |
| [CUSTOM_LAYERS_SUMMARY.md](CUSTOM_LAYERS_SUMMARY.md) | 7.7KB | 全員 | 1ページにまとめたリファレンス |
| [CUSTOM_LAYERS_GUIDE.md](CUSTOM_LAYERS_GUIDE.md) | 11KB | 中級者 | 包括的な詳細ガイド |
| [layers_txt/EXAMPLES.md](layers_txt/EXAMPLES.md) | 12KB | 実践者 | 実践的な例とテンプレート |
| [layers_txt/README.md](layers_txt/README.md) | 4.2KB | 全員 | ディレクトリの説明 |

### サンプルファイル

| ファイル | サイズ | 説明 |
|---------|-------|------|
| [layers_txt/layers_custom_example.txt](layers_txt/layers_custom_example.txt) | 3.3KB | 動作する完全なサンプル |
| [layers_txt/layers_test_custom.txt](layers_txt/layers_test_custom.txt) | 113B | テスト設定の例 |

---

## 🔗 関連リンク / Related Links

### 公式ドキュメント

- [地理院地図](https://maps.gsi.go.jp/) - 公式サイト
- [地理院地図デモ](https://gsi-cyberjapan.github.io/gsimaps/) - GitHub版デモ
- [レイヤー定義規約](https://github.com/gsi-cyberjapan/layers-dot-txt-spec) - 仕様書
- [レイヤー編集ツール](https://gsi-cyberjapan.github.io/gsimaps/config.html) - GUIツール

### このリポジトリ

- [README.md](README.md) - リポジトリのトップページ
- [CONTRIBUTING.md](CONTRIBUTING.md) - 貢献ガイド
- [LICENSE](LICENSE) - ライセンス情報

---

## ⚡ クイックリンク / Quick Links

### よく使うセクション

- [最小構成の例](CUSTOM_LAYERS_SUMMARY.md#最小構成--minimal-configuration)
- [プロパティ一覧](CUSTOM_LAYERS_SUMMARY.md#よく使うプロパティ--common-properties)
- [トラブルシューティング](CUSTOM_LAYERS_SUMMARY.md#トラブルシューティング--troubleshooting)
- [FAQ](CUSTOM_LAYERS_SUMMARY.md#faq)
- [コピー＆ペーストテンプレート](layers_txt/EXAMPLES.md#テンプレート)

### 実例

- [OpenStreetMap](layers_txt/EXAMPLES.md#2-openstreetmapの利用)
- [GeoJSON](layers_txt/EXAMPLES.md#3-geojsonベクトルデータ)
- [レイヤーグループ](layers_txt/EXAMPLES.md#4-レイヤーグループ)
- [災害情報](layers_txt/EXAMPLES.md#実践例災害情報レイヤー)

---

## 📊 学習の流れ / Learning Path

```
初心者 / Beginner
    ↓
1. クイックスタートで実際に試す
   → QUICK_START_CUSTOM_LAYERS.md
    ↓
2. サンプルファイルを見る
   → layers_txt/layers_custom_example.txt
    ↓
3. まとめで全体を把握
   → CUSTOM_LAYERS_SUMMARY.md

中級者 / Intermediate
    ↓
4. 詳細ガイドで理解を深める
   → CUSTOM_LAYERS_GUIDE.md
    ↓
5. 実践例から学ぶ
   → layers_txt/EXAMPLES.md
    ↓
6. 実際に作成してみる

上級者 / Advanced
    ↓
7. レイヤー定義規約を読む
   → https://github.com/gsi-cyberjapan/layers-dot-txt-spec
    ↓
8. レイヤー編集ツールを使う
   → https://gsi-cyberjapan.github.io/gsimaps/config.html
    ↓
9. 複雑なレイヤー構造を実装
```

---

## 🎓 レベル別おすすめドキュメント / Recommended by Level

### 🔰 初心者向け

1. **[クイックスタート](QUICK_START_CUSTOM_LAYERS.md)** ⭐⭐⭐⭐⭐
   - まずはここから！

2. **[まとめ](CUSTOM_LAYERS_SUMMARY.md)** ⭐⭐⭐⭐⭐
   - 図解でわかりやすい

3. **[基本例](layers_txt/EXAMPLES.md#1-基本的なタイルレイヤー)** ⭐⭐⭐⭐
   - シンプルな例から

### 🎯 中級者向け

1. **[包括的ガイド](CUSTOM_LAYERS_GUIDE.md)** ⭐⭐⭐⭐⭐
   - 詳細を理解する

2. **[実践例集](layers_txt/EXAMPLES.md)** ⭐⭐⭐⭐⭐
   - 実用的な例

3. **[プロパティリファレンス](CUSTOM_LAYERS_GUIDE.md#重要なプロパティ)** ⭐⭐⭐⭐
   - すべてのオプション

### 🚀 上級者向け

1. **[レイヤー定義規約](https://github.com/gsi-cyberjapan/layers-dot-txt-spec)** ⭐⭐⭐⭐⭐
   - 公式仕様

2. **[レイヤー編集ツール](https://gsi-cyberjapan.github.io/gsimaps/config.html)** ⭐⭐⭐⭐
   - GUIで効率化

3. **[災害情報レイヤー例](layers_txt/EXAMPLES.md#実践例災害情報レイヤー)** ⭐⭐⭐⭐⭐
   - 実践的な実装

---

## 💬 サポート / Support

質問や問題がある場合：

1. このドキュメント群を検索
2. [FAQ](CUSTOM_LAYERS_SUMMARY.md#faq) を確認
3. [トラブルシューティング](CUSTOM_LAYERS_SUMMARY.md#トラブルシューティング--troubleshooting) を参照
4. GitHubでイシューを作成

---

## 📝 更新履歴 / Change Log

- 2024-10-24: 初版リリース
  - 包括的なドキュメント作成
  - サンプルファイル追加
  - 実践例集作成

---

**ハッシュタグ:** #gsimaps

**リポジトリ:** https://github.com/gsi-cyberjapan/gsimaps
