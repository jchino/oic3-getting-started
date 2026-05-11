# 8. 統合のアクティブ化と外部実行

この章では、作成した統合をアクティブ化し、外部から実行します。
これにより、Oracle Integration の統合が実際の API として動作することを確認できます。

## 8.1 統合のアクティブ化

統合は作成しただけでは実行できません。
実行するには ***アクティブ化*** が必要です。

『[7. 統合のテスト実行](chapter7.md)』では、統合キャンバスの **「テスト」** をクリックすることで、自動的に統合がアクティブ化されていました。
Oracle Integration の外部から統合の実行したり、本番運用を開始する場合には、明示的に統合をアクティブ化する必要があります。

1.  本チュートリアルのために作成したプロジェクトを開きます。

2.  作成した統合のメニュー・をクリックし、 **「アクティブ化」** を選択します。

3.  **「統合のアクティブ化」** パネルが表示されたら、 **「トレース・レベルの選択」** と **「ランタイム・オプションの構成」** はそれぞれ初期値を受け入れることにして、 **「アクティブ化」** をクリックします。

    ![スクリーンショット: 統合のアクティブ化](./images/activate_button.png)

4.  アクティブ化が成功したことを伝えるメッセージが表示されたら、サービス・コンソール右上にある **「リフレッシュ」** をクリックします。
    統合のステータスが **「構成済」** から **「アクティブ」** に変わったことを確認します。

    ![スクリーンショット: 統合のステータスが「アクティブ」になった状態](./images/activate_status.png)

## 8.2 統合の実行

まずは、Oracle Integration が用意している統合の実行画面を使用して実行してみましょう。

1.  統合のメニューから **「実行」** を選択します。

2.  統合の実行画面が表示されます。
    **「本文」** タブを開き、リクエスト・ペイロードの JSON で `product_id` の値を指定します。

3.  画面右上にある **「実行」** をクリックします。

    ![スクリーンショット: 統合の実行](./images/run_screen.png)

4.  画面の右側にアクティビティ・ストリームが表示されます。
    統合が期待通りに実行されたことを確認します。

## 8.3 エンドポイント URL の確認

外部から実行するためには、エンドポイント URL が必要です。
エンドポイント URL は、次の手順で確認できます。

1.  統合の実行画面が表示されていない場合は、統合の実行画面を開きます。

2.  統合の実行画面が表示されたら、 **「エンドポイント・メタデータ」** をクリックします。

3.  画面の右側に **「エンドポイント・メタデータ」** パネルが表示されます。
    **「Endpoint URL」** をコピーしておきます。

    ![スクリーンショット: Endpoint URL の確認](./images/endpoint.png)

エンドポイントは以下のような形式になります:

```sh
https://<your-instance>/ic/api/integration/v2/flows/rest/project/<project-id>/<integration-id>/<version>/export
```

- <project-id>: プロジェクトの識別子
- <integration-id>: 統合の識別子
- <version>: バージョン

## 8.4 curl による統合の実行

本チュートリアルで作成した統合は、POST メソッドでレスポンス・ペイロードとして JSON を受け取ります。
curl の基本的なコマンドは次のとおりです。

```sh
curl -X POST -i \
  https://<your-instance>/ic/api/integration/v2/flows/rest/project/<project-id>/<integration-id>/<version>/export \
  -H 'Content-Type: application/json' \
  -d '{ "product_id": 30 }' \
  -u '<username>:<password>'
```

| パラメータ | 説明 |
| --- | --- |
| -X | HTTP メソッド。今回は `POST` を指定 |
| -i | レスポンス・ヘッダーを出力 |
| -H | リクエスト・ヘッダーとその値。今回は `Content-Type: application/json` を指定 |
| -d | リクエスト・ペイロード |
| -u | Basic 認証のためのユーザー名/パスワード |

### 8.4.1 curl コマンドの実行

Cloud Shell を起動し、次の例のように curl コマンドを実行します。

```sh
curl -X POST -i \
  https://<your-instance>/ic/api/integration/v2/flows/rest/project/<project-id>/<integration-id>/<version>/export \
  -H 'Content-Type: application/json' \
  -d '{ "product_id": 30 }' \
  -u 'user@example.com:password'
```

> **Note:**
>
> - `https://<your-instance>/.../export` は、8.3 で取得した Endpoint URL と置き換えてください
> - `user@example.com` と `password` は、Oracle Integration にログインしたユーザー名とパスワードに置き換えてください

### 8.4.2 出力例

Oracle Integration によってリクエストが受信されると、HTTP ステータスとして `202 Accepete` （次のコード・ブロック1行目）が返ってきます。

```sh
HTTP/1.1 202 Accepted
Date: Fri, 01 May 2026 04:24:01 GMT
Transfer-Encoding: chunked
Connection: keep-alive
x-oracle-ics-instance-id: lJrSjUUVEfGXW0tyvl-GZA
oic-virtualservice: true
Strict-Transport-Security: max-age=15768000; includeSubDomains
opc-request-id: IFESXKPBBYJJH6OFZJISWZT9CWR7D8H1/YP9XBQ8DI5OL3QIPAPHQHFDN3VC25CAP/EHLDGU1TQQZ2OPTUGVMM95J69MPVY9YW
```

他のステータスが返ってきた場合は、8.6 トラブル・シューティングを確認してください。

## 8.5 統合の実行結果の確認

curl コマンドの実行に成功したら、統合の実行画面の **「インスタンスのトラッキング」** をクリックします。
これにより、プロジェクトの **「監視」** ページが表示され、直近1時間に実行された統合の結果がリスト形式で表示されます。

![スクリーンショット: インスタンスのトラッキング](./images/run_success.png)

ステータスが **「成功」** と表示されていれば、統合の実行が成功したことを表しています。

## 8.6 トラブル・シューティング

curl コマンドの実行がエラーになった場合は、以下を参考にエラーを解消してください。

### ケース1: 401 Unauthorized

- 原因: 認証情報が不足しているか無効
- 対処方法: Basic 認証の場合はユーザー名・パスワードが正しく指定されていることを確認

### ケース3: 403 Forbidden

- 原因: 指定したユーザーに適切な Oracle Integration のアプリケーション・ロールが付与されていない
- 対処方法: 指定したユーザーに Oracle Integration サービス・インスタンスのアプリケーション・ロールとして次のいずれかが付与されていることを確認
  + Service Invoker
  + Service User
  + Service Developer
  + Service Administrator

### ケース2: 404 Not Found

- 原因: 指定された URL が無効
- 対処方法:
  + URL にスペル・ミスがないか確認
  + 統合のバージョン番号を確認

### ケース3: 415 Unsupported Media Type

- 原因: リクエスト・ヘッダー `Content-Type` が無効
- 対処方法: 本チュートリアルでは、リクエスト・ヘッダーで `Content-Type: application/json` が指定されていることを確認

## 8.7 統合の REST エンドポイントの認証

Oracle Integration の REST エンドポイントは認証が必要です。
本チュートリアルでは、REST アダプタ・トリガー接続 (REST Trigger Conn) を作成した際に、セキュリティ・ポリシーとして「OAuth 2.0 Or Basic Authentication」を選択しました。
そのため、次の2つの認証方式が使用できます。

- Basic 認証
- OAuth 2.0

本チュートリアルでは Basic 認証を使用していますが、本番運用時は OAuth 2.0 の使用が推奨されます。
OAuth 2.0 を使用するためには、IAM Identity Domain で機密クライアント・アプリケーションを作成する必要があります。

詳細は次のドキュメントを確認してください:

- [OAuthを使用した統合のRESTエンドポイントの保護](https://docs.oracle.com/cd/G41715_01/paas/application-integration/integrations-user/protect-integrations-rest-endpoint-oauth.html) (日本語機械翻訳版)
- [Protect an Integration's REST Endpoint with OAuth](https://docs.oracle.com/en/cloud/paas/application-integration/integrations-user/protect-integrations-rest-endpoint-oauth.html) (英語オリジナル版)

## 8.8 この章のまとめ

統合フローは、設計・作成しただけでは動作せず、アクティブ化することで初めて実行可能になります。
この章では、作成した統合フローをアクティブ化し、外部から実行する方法を学びました。

また、REST アダプタ・トリガーを使用することで、統合を外部から呼び出せる API として公開できることを確認しました。
さらに、curl コマンドを使って HTTP POST リクエストを送信し、JSON データを統合に渡すことで、実際の動作を検証しました。

この一連の流れにより、以下を理解できたはずです：

- 統合をアクティブ化して実行可能にする方法
- REST エンドポイントの確認方法
- 外部クライアント（curl）から統合を呼び出す方法

この時点で、Oracle Integration を使った「外部システムとの連携」の基本が一通り体験できています。

次の章では、統合の実行結果を監視し、問題発生時の確認方法について学びます。
