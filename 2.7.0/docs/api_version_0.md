# API v0

<section class="module">

## バージョン 0

API のバージョン 0（v0）は、PhoneGap Build のベータバージョンのプレビューリリースです。このリリースのオンライン提供は既存のクライアント向けに継続されますが、今後このリリースの更新は行われません。PhoneGap Build にアクセスする新しいアプリケーションを開発する場合は、[最新バージョンの API（現時点で v1）](/docs/api)を使用してください。

### 認証

v0 は現在、HTTPS 経由の基本認証を使用して認証を行います。他の認証オプション、特にユーザーが自分の PhoneGap Build 資格情報を使用してアプリケーションや開発ツールを認証できる方法について、現在検討中です（現在の作成者は OAuth 2 を推奨しています）。

未認証のリクエストが実行された場合は、常に `401`（未認証）のステータスコードが返されます。

</section>
<section class="module">

## JSON

リクエストが成功した場合は、JSON エンコードの文字列またはバイナリファイルが返されます。リクエストが失敗した場合は必ず、該当するステータスコードと共に、以下の形式で JSON エンコードの文字列が返されます。

    {"error":"some error message"}

この API を使用する場合は、返されるステータスコードを確認してください。ステータスコードが 200 でない場合は、以下のように、解析後のレスポンスの error フィールドを確認してください。

    if (res.status != 200)
        console.log(JSON.parse(res.body).error)

</section>

# API ドキュメント

<section class="module">

## 読み取り API

### GET https://build.phonegap.com/api/v0/me

認証済みユーザーの JSON エンコード表現を取得します。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v0/me</strong></pre>
    {"created_at":"2010-10-12T19:10:16Z","updated_at":"2010-11-29T19:58:00Z",
      "username":"alunny","email":"andrew.lunny@nitobi.com"}

### GET https://build.phonegap.com/api/v0/apps

認証済みユーザーのアプリケーションの JSON エンコード表現を取得します。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v0/apps</strong></pre>
    [{"created_at":"2010-11-09T20:36:58Z","title":"alunny's Amazing App",
      "updated_at":"2010-11-23T22:53:12Z","symbian_status":"symbian complete",
      "repo_url":"http://github.com/alunny/phonegap-start.git",
      "blackberry_status":"blackberry pending","android_status":"complete",
      "webos_status":"compiling webos project","id":50,"icon":"icon.png",
      "version":99.999,"package":"com.alunny.amazing","person_id":1,
      "desc":"An Amazing app by alunny"},
      {"created_at":"2010-11-23T00:16:04Z","title":"New Title",
      "updated_at":"2010-11-26T21:11:55Z","symbian_status":"symbian complete",
      "repo_url":null,"blackberry_status":"pending","android_status":"pending",
      "webos_status":"webos complete","id":52,"icon":null,"version":null,
      "package":null,"person_id":1,"desc":null},
      {"created_at":"2010-11-27T00:39:57Z","title":"Docco App",
      "updated_at":"2010-11-27T00:39:59Z","symbian_status":"symbian complete",
      "repo_url":null,"blackberry_status":"pending","android_status":"error",
      "webos_status":"webos complete","id":53,"icon":null,"version":null,
      "package":null,"person_id":1,"desc":null}]

### GET https://build.phonegap.com/api/v0/apps/:id

1 つのアプリケーション（認証済みユーザーに属しているアプリケーション）の JSON エンコード表現を取得します。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v0/apps/50</strong></pre>
    {"created_at":"2010-11-09T20:36:58Z","title":"alunny's Amazing App",
     "updated_at":"2010-11-23T22:53:12Z","symbian_status":"symbian complete",
     "repo_url":"http://github.com/alunny/phonegap-start.git",
     "blackberry_status":"blackberry pending","android_status":"error",
     "webos_status":"compiling webos project","id":50,"icon":"icon.png",
     "version":99.999,"package":"com.alunny.amazing","person_id":1,
     "desc":"An Amazing app by alunny"}

アプリケーションが存在しない場合または別のユーザーに属する場合は、エラーメッセージがステータスコード `404` と共に返されます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v0/apps/54</strong></pre>
    {"error":"app #54 not available"}

### GET https://build.phonegap.com/api/v0/apps/:id/:icon

アプリケーションのアイコンファイルを取得します。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v0/apps/50/icon &gt; icon.png</strong></pre>

取得できるアイコンがない場合は、エラーメッセージがステータスコード `404` と共に返されます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v0/apps/52/icon</strong></pre>
    {"error":"No icon available for app #52"}

### GET https://build.phonegap.com/api/v0/apps/:id/:platform

指定したプラットフォーム用のアプリケーションパッケージをダウンロードします。現時点で利用可能なプラットフォームは、`android`、`blackberry`、`symbian` および `webos` です。

実際にはこのリクエストによって、アプリケーションパッケージ自体へのリダイレクトが返されます。アプリケーションをダウンロードする際は、必ず API クライアントがこのリダイレクトを追跡するようにしてください。

<pre><strong>$ curl -Lu andrew.lunny@nitobi.com https://build.phonegap.com/api/v0/apps/50/android &gt; app_50.apk</strong></pre>

指定したプラットフォーム用のアプリケーションパッケージが利用できない場合は、エラーメッセージがステータスコード `404` と共に返されます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v0/apps/52/android</strong></pre>
    {"error":"App #52 for android error"}

### GET https://build.phonegap.com/api/v0/keys/

ビルド用にアップロードされている署名キーのリストを取得します。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v0/keys/</strong></pre>
    {"ios":[{"title":"Test Key","updated_at":"2011-07-07T15:51:23-07:00",
    "id":2,"mobile_provision":"test.mobileprovision",
    "cert_name":"Certificates.p12"}],"blackberry":[],"android":[]}

アップロードされているキーがない場合は、以下のレスポンスが返されます。

    {"ios":[],"blackberry":[],"android":[]}

特定のプラットフォームのキーを取得するには、以下のリクエストを使用します。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v0/keys/:platform</strong></pre>

アプリケーションが存在しない場合または別のユーザーに属する場合は、エラーメッセージがステータスコード `404` と共に返されます。

</section>
<section class="module">

## 書き込み API

### POST https://build.phonegap.com/api/v0/apps

新規アプリケーションを作成します。title パラメーターを渡す必要があります。また、git または svn 公開リポジトリの URL、`index.html` あるいはプロジェクトの zip ファイルを送信する必要があります。

repo_url を指定する場合：

<pre><strong>$ curl -u andrew.lunny@nitobi.com -d 'data={"title":"New App","repo":"http://github.com/alunny/phonegap-start.git"}' \
  https://build.phonegap.com/api/v0/apps</strong></pre>
    {"created_at":"2010-11-29T21:13:26Z","title":"alunny's Amazing App",
    "updated_at":"2010-11-29T21:13:26Z","symbian_status":"pending",
    "repo_url":"http://github.com/alunny/phonegap-start.git",
    "blackberry_status":"pending","android_status":"pending",
    "webos_status":"pending","id":55,"icon":"icon.png","version":"99.999",
    "package":"com.alunny.amazing","person_id":1,
    "desc":"An Amazing app by alunny"}

ファイルを指定する場合（curl を使用する場合は、`-d` ではなく `-F` オプションを使用します）：

<pre><strong>$ curl -F file=@index.html -F 'data={"title":"Another App"}' -u andrew.lunny@nitobi.com \
  https://build.phonegap.com/api/v0/apps</strong></pre>
    {"created_at":"2010-11-29T21:52:32Z","title":"Another App",
    "updated_at":"2010-11-29T21:52:32Z","symbian_status":"pending",
    "repo_url":null,"blackberry_status":"pending","android_status":"pending",
    "webos_status":"pending","id":56,"icon":null,"version":null,
    "package":null,"person_id":1,"desc":null}

ここでも、問題が発生した場合は以下の JSON エラーが返されます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -d 'data={"title":"New App"}' https://build.phonegap.com/api/v0/apps</strong></pre>
    {"error":"Need either a repo url or a file"}

リクエスト内に問題がある場合は、ステータスコード `400`（無効なリクエスト）が返されます。JSON 文字列に、必要な変更の詳細が示されます。ステータスコード `500` が返された場合は、内部エラーが発生しています。このリクエストについて、弊社までお問い合わせください。

### POST https://build.phonegap.com/api/v0/apps/:id/:icon

指定したアプリケーションのアイコンファイルを設定します。

<pre><strong>$ curl -F file=@icon.png -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v0/apps/56/icon</strong></pre>
    {"created_at":"2010-11-29T21:52:32Z","title":"Another App",
    "updated_at":"2010-11-29T22:24:26Z","symbian_status":"symbian complete",
    "repo_url":null,"blackberry_status":"pending","android_status":"pending",
    "webos_status":"webos complete","id":56,"icon":"icon.png",
    "version":null,"package":null,"person_id":1,"desc":null}

リクエスト内に問題がある場合は、JSON エラーがステータスコード `400` と共に返されます。

### POST https://build.phonegap.com/api/v0/apps/:id/push

現在のアプリケーションをソースリポジトリから更新します。この機能は特に、[Github の post-receive フック](http://help.github.com/post-receive-hooks/)機能と連携するように設計されています。現時点では、ポストデータは無視されます。以下の例では、curl で Content-Length ヘッダーの設定が有効になるように、ダミーのデータが含まれています。

<pre><strong>$ curl -X POST -d data=dummy -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v0/apps/55/push</strong></pre>
    {"created_at":"2010-11-29T21:13:26Z","title":"alunny's Amazing App",
    "updated_at":"2010-11-29T22:28:33Z","symbian_status":"pending",
    "repo_url":"http://github.com/alunny/phonegap-start.git",
    "blackberry_status":"pending","android_status":"pending",
    "webos_status":"pending","id":55,"icon":"icon.png","version":99.999,
    "package":"com.alunny.amazing","person_id":1,
    "desc":"An Amazing app by alunny"}

アプリケーションがリポジトリに関連付けられていない場合は、ステータスコード `400` が返されます。アプリケーションが見つからない場合は、ステータスコード `404` が返されます。内部エラーが発生した場合は、`500` が返されます。

<pre><strong>$ curl -X POST -d data=dummy -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v0/apps/56/push</strong></pre>
    {"error":"app #56 is not repo backed"}

### PUT https://build.phonegap.com/api/v0/apps/:id

アプリケーションに関連付けられたメタデータを更新します。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -X PUT -d 'data={"title":"New Title"}' \
  https://build.phonegap.com/api/v0/apps/56</strong></pre>
    {"created_at":"2010-11-29T21:52:32Z","title":"New Title",
    "updated_at":"2010-11-29T22:37:44Z","symbian_status":"pending",
    "repo_url":null,"blackberry_status":"pending","android_status":"pending",
    "webos_status":"pending","id":56,"icon":"icon.png","version":null,
    "package":null,"person_id":1,"desc":null}

ポストデータを解析できない場合は、ステータスコード `400` が返されます。

### POST https://build.phonegap.com/api/v0/keys/:platform

アプリケーションの署名用のキーをアップロードします。

#### IOS サンプル

password フィールドは、キーでパスワードが必要になる場合に使用するオプションのフィールドです。

以下のサンプルの場合：

<pre><strong>$ curl -F profile_file=@example.mobileprovision -F cert_file=@example.p12 -F 'data={"title":"Example Key", "password":"test"}' -u andrew.lunny@nitobi.com http://build.phonegap.com/api/v0/keys/ios/</pre></strong>

以下のようなレスポンスが生成されます。

    {"title":"Example Key","updated_at":"2011-07-08T10:27:01-07:00",
    "id":3,"cert_name":"example.p12","mobile_provision":"example.mobileprovision"}

#### Android サンプル

以下のサンプルの場合：

<pre><strong>$ curl -F key_file=@example.keystore -F 'data={"title":"Example Key","alias":"example alias", "key_pw":"test", "keystore_pw":"test"}' -u andrew.lunny@nitobi.com http://build.phonegap.com/api/v0/keys/android/</pre></strong>

以下のようなレスポンスが生成されます。

    {"title":"Example Key","updated_at":"2011-07-08T14:07:09-07:00","id":1}

#### Blackberry サンプル

以下のサンプルの場合：

<pre><strong>curl -F csk_file=@example.csk -F db_'data={"title":"example key", "password":"test"}' -u andrew.lunny@nitobi.com http://build.phonegap.com/api/v0/keys/blackberry/</pre></strong>

以下のようなレスポンスが生成されます。

    {"title":"example key","updated_at":"2011-07-08T10:48:18-07:00","id":1}

アプリケーションが存在しない場合または別のユーザーに属する場合は、エラーメッセージがステータスコード `404` と共に返されます。

### DELETE https://build.phonegap.com/api/v0/apps/:id

アプリケーションを削除します。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -X DELETE https://build.phonegap.com/api/v0/apps/56</strong></pre>
    {"success":"app #56 destroyed"}

ここでも、アプリケーションが見つからない場合は、`404` エラーが返されます。

</section>
