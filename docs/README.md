# Oracle Integration チュートリアル

## このチュートリアルについて

このチュートリアルでは、Oracle Integration を使用した REST API、データベース、ファイル連携を使用した自動化処理の基本を学習します。

## このチュートリアルで作成するもの

このチュートリアルでは、REST API リクエストで受信した商品 ID をもとにデータベースから販売データを検索し、その結果を CSV ファイルとしてファイル・サーバーへ出力する自動化処理を作成します。

![処理フロー図](./images/chapter1_processing_flow.png)

## 対象読者

- Oracle Integration を初めて利用する方
- クラウド統合製品の利用経験がない方

## 前提知識

- if / loop 程度の基本的なプログラミング知識
- JSON の基本的な読み書き

## 必要な環境

このチュートリアルは Oracle Cloud Infrastructure (OCI) の環境とユーザー・アカウントが必要です。
トライアル環境でも実施できる内容になっています。

また、Oracle Integration の他に、OCI の次のサービスを使用します。

- Oracle Autonomous AI Database (Always Free でも可能です)
- OCI Cloud Shell

このチュートリアルでは、これらのサービスの環境設定などの詳細は触れていません。
必要に応じて
[OCI のドキュメント](https://docs.oracle.com/ja-jp/iaas/Content/home.htm)
や
[OCI チュートリアル](https://oracle-japan.github.io/ocitutorials/)
などを参照してください。

## このチュートリアルの進め方

このチュートリアルは、まず動かすことを重視しています。

詳細な機能説明よりも、実際に操作しながら Oracle Integration に慣れることを目的としています。

## このチュートリアルの構成

このチュートリアルは、次の内容で構成されています。

- 概要編
  + Oracle Integration の概要
  + サービス・コンソール
  + プロジェクト
- チュートリアル編
  + REST API の受信
  + Oracle Autonomous AI Database からのデータ取得
  + CSV ファイルの生成
  + ファイル・サーバーとの連携
  + 統合の実行と監視

## 注意事項

- このチュートリアルは Oracle Integration 3 を対象としています。
- Oracle Integration の UI はバージョンにより異なる場合があります。
