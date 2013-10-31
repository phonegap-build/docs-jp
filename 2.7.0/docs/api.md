# API

Adobe® PhoneGap™ Build API では、PhoneGap Build Web サービスを使用して、PhoneGap アプリケーションの作成、ビルド、更新、ダウンロードをプログラムによって実行できます。この API は、IDE、シェルスクリプト、アプリケーションビルダー、その他のあらゆる場所に簡単に統合できるように設計されています。

このドキュメントでは、この API のバージョン 1 を対象として説明します。

## API ドキュメント

* [読み取り API](docs_read_api.md.html)
* [書き込み API](docs_write_api.md.html)

## 認証

バージョン 1 では、HTTPS 経由の基本認証およびトークン認証という、2 種類の認証形式をサポートしています。

基本認証を使用する場合は、PhoneGap Build の資格情報（ユーザー名とパスワード）を使用して、以下のように各リクエストを認証します。
<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/me</strong></pre>
    {
        "created_at":"2010-10-12T19:10:16Z",
        "updated_at":"2010-11-29T19:58:00Z",
        "username":"alunny",
        "email":"andrew.lunny@nitobi.com"
    }

トークン認証を使用する場合は、基本認証を使用し、トークンのリクエストを付加して `/token` にポストします。その結果、レスポンスとしてトークンが返されます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -X POST -d "" https://build.phonegap.com/token</pre></strong>
    {
        "token":"ASTRINGTOKEN"
    }

その後で、以下のように、実行するすべての呼び出しで、このトークンをパラメーターとして渡すことができます。

<pre><strong>$ curl https://build.phonegap.com/api/v1/me?auth_token=ASTRINGTOKEN</strong></pre>
    {
        "username":"alunny",
        "email":"andrew.lunny@nitobi.com"
    }

両方の認証形式がサポートされています。未認証のリクエストが実行された場合は、常に `401`（未認証）のステータスコードが返されます。

わかりやすく説明するために、以下のすべての例でトークン認証を使用します。

<strong>Github ユーザー</strong>

Github 認証を使用して登録したユーザーの場合、PhoneGap Build の資格情報を持っていない可能性があり、その場合は基本認証を使用できません。Github にリンクされたアカウント用の認証トークンを受信するには、「アカウントを編集」（サイトのナビゲーションバーの右上）に移動します。認証トークンのセクションで、トークンを取得できます。このセクションでは、トークンの作成、リセットおよび削除もできます。トークンをリセットまたは削除した場合、今後のリクエストで以前のトークンを使用すると、それらのリクエストは無効になります。

## JSON

リクエストが成功した場合は、JSON エンコードの文字列またはバイナリファイルが返されます。リクエストが失敗した場合は必ず、該当するステータスコードと共に、以下の形式で JSON エンコードの文字列が返されます。

    {
        "error":"some error message"
    }

この API を使用する場合は、返されるステータスコードを確認してください。ステータスコードが 200 でない場合は、以下のように、解析後のレスポンスの error フィールドを確認してください。

    if (res.status != 200)
        console.log(JSON.parse(res.body).error)

HTTP の標準に従い、4xx ステータスはリクエスト内に問題があることを示します。また、5xx ステータスは、サーバー側でエラーが発生したことを示します。500 エラーが発生した場合または予期しない 400 エラーを受信した場合は、[サポートフォーラム](http://community.phonegap.com)を確認してください。

## JSONP

PhoneGap Build の開発者は JSONP アクセスを利用できます。リクエストに `callback` パラメーターを追加するだけで、JSONP レスポンスの本文が指定した関数でラップされます。

<pre><strong>$ curl https://build.phonegap.com/api/v1/me?auth_token=ASTRINGTOKEN&callback=exec</strong></pre>
    exec({
        "username":"alunny",
        "email":"andrew.lunny@nitobi.com"
    })

この機能によって、通常の `<script>` タグを使用して PhoneGap Build API にアクセスできます。[JSONP について詳しくは、こちらを参照してください](http://en.wikipedia.org/wiki/JSONP)。

## HATEOAS

PhoneGap Build API v1 では、 __Hypermedia as the Engine of Application State（[HATEOAS](http://en.wikipedia.org/wiki/HATEOAS)）__ を可能な限り使用します。このため、アプリケーション開発者は、アプリケーション内部の他のルートを知らなくても、api ソース（`/api/v1`）を検出し、ネストされたリソースの `link` 属性を追跡することでアプリケーションをナビゲートできます。

API v1 のホームリソースは、`/me` リソース（現在のユーザーの表現）と同じです。
