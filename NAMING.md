# チュートリアルで作成する成果物名

本チュートリアルでは、以下の名前で成果物を作成します。

## chapter3

| 種類 | 名前 |
| --- | --- |
| プロジェクト | `Sales CSV Export` |

## chapter4

| 種類 | 名前 |
| --- | --- |
| 統合 | `Export Sales CSV` |
| REST アダプタ接続 | `REST Trigger Connection` |
| REST トリガー・アクション | `receiveProductRequest` |
| Scope | `mainScope` |

## chapter5

| 種類 | 名前 |
| --- | --- |
| ATP アダプタ接続 | `ATP Connection` |
| ATP 呼出しアクション | `getSalesByProductId` |
| バインド変数 | `#VAR_PRODUCT_ID` |
| Switch アクション | `hasSalesRecord` |
| Logger アクション | `logNoSalesRecord` |

## chapter6

| 種類 | 名前 | 備考 |
| --- | --- | --- |
| Stage File アクション | `writeSalesCsv` | |
| Stage File - File | `sales.csv` | |
| Stage File - Output Directory | `/tmp` | |
| Stage File - レコード | `salesRecord` | Mapper では、**「Sales Record」** と表示される |
| Stage File - レコードセット | `salesRecordSet` | Mapper では、 **「Sales Record Set」** と表示される |
| FTP アダプタ接続 | FTP Connection | |
| FTP Invoke アクション | uploadSalesCsv | |
| FTP Invoke - File | 'sales-%SEQ%.csv` | `%SEQ%` は実行時 Oracle Integration によって連番へ置き換えられる |
| FTP Invoke - Directory | `/home/users/<username>` | `<username>` は Oracle Integration にログインしたユーザー名と置き換える |
