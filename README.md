# Oracle Integration 3 入門チュートリアル

このリポジトリでは、Oracle Integration を使用したアプリケーション統合の基本を学ぶためのチュートリアルを提供します。

## 🎯 チュートリアルの目的

このチュートリアルでは、Oracle Integration を使用して以下の処理を実装しながら、基本的な使い方を学びます。

- REST API によるリクエスト受信
- データベース（ADB）への問い合わせ
- CSVファイルの生成
- SFTP サーバーへのファイル転送

初心者向けに、最小構成で動作することを重視しています。

実務的な内容（例外処理、スケジュール）は、今後付録で扱う予定です。

## 👤 対象読者

- Oracle Integration をこれから利用する方
- 基本的なプログラミング知識（条件分岐・ループなど）を持つ方

## 🧱 チュートリアルの概要

以下のような統合フローを作成します:

1. REST Adapter でリクエストを受信
2. ATP Adapter で SQL を実行
3. 結果を CSV ファイルとして生成
4. FTP Adapter でファイルを Oracle Integration のサーバーへアップロード

<!--
## 🗺 全体アーキテクチャ

<p align="center">
  <img src="./docs/images/architecture.png" width="700" alt="全体アーキテクチャ">
</p>

<p align="center">
図. 全体アーキテクチャ
</p>
-->

## 📚 コンテンツ構成

- [はじめに](./docs/README.md)
- [Oracle Integration の基本](./docs/chapter1.md)
- [サービス・コンソール](./docs/chapter2.md)
- [プロジェクト](./docs/chapter3.md)
- [統合の作成（基礎）](./docs/chapter4.md)
- [データの取得と変換](./docs/chapter5.md)
- [ファイル連携](./docs/chapter6.md)
- [統合のテスト実行](./docs/chapter7.md)
- [アクティベーションと外部からの実行](./docs/chapter8.md)
- [モニタリング](./docs/chapter9.md)

チュートリアルで作成する成果物の名前は [NAMING.md](NAMING.md) にまとめています。

## 🛠 前提条件

- Oracle Integration インスタンスが利用可能であること
- 必要な接続先（ADB/SFTP など）が作成済みであること

詳細な環境構築手順は本チュートリアルでは扱いません

## 📝 補足

このチュートリアルは
[Honkit](https://github.com/honkit/honkit)
を使用して Markdown から静的な Web ページを生成します。

## 🙌 貢献

改善提案やフィードバックは Issues にお願いします。
