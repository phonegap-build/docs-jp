# 書き込み API V1

このドキュメントは、Adobe® PhoneGap™ Build API V1 ドキュメントの一部です。以下のドキュメントも参照してください。

* [API 概要](/docs/api)
* [読み取り API](/docs/read_api)

すべての書き込み API では、JSON エンコード形式の内容が必要です。また、多くの書き込み API でファイルのアップロードも可能です。これにより、API リクエストがコンテンツタイプ `multipart/form-data`であり、リクエストの JSON  本体の名前が `data` であることが必要になります。今後のリリースでは、より優れた対処方法を検討します。

### POST https://build.phonegap.com/api/v1/apps

新規アプリケーションを作成します。

#### 必須のパラメーター

* __title__ ：アプリケーションのタイトルを指定する必要があります。タイトルがパッケージの `config.xml` にも指定されている場合、`config.xml` ファイル内のタイトルが優先されます。
* __create_method__ ：アプリケーションの作成方法（以下で説明します）。有効な値は次の 3 つです。
  * __file__ ：アプリケーションの内容を含んだファイルがアップロードされます。
  * __remote_repo__ ：アプリケーションの内容を含むリモートリポジトリを使用します。
  * __hosted_repo__ ：アプリケーションの内容を、`git.phonegap.com` でホストされる git リポジトリにアップロードします。

#### オプションのパラメーター

* __package__ ：アプリケーションのパッケージ識別子を設定します。この設定は、アプリケーションの作成後にも実行できます。また、`config.xml` ファイル内でも実行できます。デフォルトは `com.phonegap.www` です。
* __version__ ：アプリケーションのバージョンを設定します。この設定は、アプリケーションの作成後にも実行できます。また、`config.xml` ファイル内でも実行できます。デフォルトは `0.0.1` です。
* __description__ ：アプリケーションの説明を設定します。この設定は、アプリケーションの作成後にも実行できます。また、`config.xml` ファイル内でも実行できます。デフォルトは空白です。
* __debug__ ：アプリケーションを[デバッグモード](/docs/phonegap-debug)でビルドします。デフォルトは false です。
* __keys__ ：署名する各プラットフォームで使用するための署名キーを設定します。詳しくは、後述の説明を参照してください。
* __private__ ：アプリケーションを公開してダウンロードできるようにするかを指定します。ベータ期間のデフォルトは `true` です。ベータ期間が終了した後のデフォルトは `false` です。
* __phonegap_version__ ：アプリケーションで使用する PhoneGap のバージョン。サポートされるバージョンと現在デフォルトになっているバージョンについて詳しくは、[config.xml](/docs/config-xml) を参照してください。

#### create_method

新しいアプリケーションはアーカイブファイルまたはリモートの git リポジトリから作成できます。または、PhoneGap Build でホストされた git リポジトリをアプリケーションと共に作成することもできます。どちらの方法を使用するかを選択するには、JSON データ内の `create_method` パラメーターを設定してください。

アプリケーションの作成方法は変更できません。リポジトリから作成されたアプリケーションを、ファイルベースのアプリケーションに変更することはできません。また、その逆の変更もできません。後で変更する場合は、古いアプリケーションを削除して、新しいアプリケーションを作成します。

#### ファイルベースのアプリケーション

ファイルベースのアプリケーションを作成するには、`create_method` パラメーターの値を `file` に設定し、パラメーター `file` を使用して、ポストのマルチパートの本体部分で zip ファイル、tar.gz ファイルまたは  index.html ファイルを指定します。

<pre><strong>$ curl -F file=@/Users/alunny/index.html -u andrew.lunny@nitobi.com -F 'data={"title":"API V1 App","package":"com.alunny.apiv1","version":"0.1.0","create_method":"file"}' https://build.phonegap.com/api/v1/apps</strong></pre>
    {
        "keys":{
            "ios":{
                "title":"ios-key",
                "default":true,
                "id":2,
                "link":"/api/v1/keys/ios/2"
             },
             "blackberry":null,
             "android":{
                "title":"release-key",
                "default":true,
                "id":2,
                "link":"/api/v1/keys/android/2"
             }
        },
        "download":{},
        "title":"API V1 App",
        "repo":null,
        "collaborators":[
            {
                "person":"andrew.lunny@nitobi.com",
                "role":"admin"
            }
        ],
        "role":"admin",
        "id":26486,
        "icon":{
            "filename":null,
            "link":"/api/v1/apps/26486/icon"
        },
        "package":"com.alunny.apiv1",
        "version":"0.1.0",
        "description":null,
        "debug":false,
        "private":true,
        "link":"/api/v1/apps/26486",
        "status":{
            "webos":"pending",
            "ios":"pending",
            "blackberry":"pending",
            "android":"pending",
            "symbian":"pending",
            "winphone":"pending"
        },
        "error":{},
        "phonegap_version":"3.0.0",
        "build_count":null
    }

#### リモートリポジトリベースのアプリケーション

リモートリポジトリベースのアプリケーションを作成するには、`create_method` パラメーターの値を `remote_repo` に設定し、`repo` パラメーターにリポジトリの URL を指定します。

この際、公開アクセス可能な URL を指定する必要があります。PhoneGap Build ではリポジトリに対する認証は実行されません。コードをプライベートに維持する場合は、他の `create_method` オプションを使用してください。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -d 'data={"title":"API V1 App","repo":"https://github.com/alunny/phonegap-start.git","create_method":"remote_repo"}' https://build.phonegap.com/api/v1/apps</strong></pre>
    {
        "keys":{
            "ios":{
                "title":"ios-key",
                "default":true,
                "id":2,
                "link":"/api/v1/keys/ios/2"
             },
             "blackberry":null,
             "android":{
                "title":"release-key",
                "default":true,
                "id":2,
                "link":"/api/v1/keys/android/2"
             }
        },
        "download":{},
        "title":"alunnys Amazing App",
        "repo":"https://github.com/alunny/phonegap-start.git",
        "collaborators":[
            {
                "person":"andrew.lunny@nitobi.com",
                "role":"admin"
            }
        ],
        "role":"admin",
        "id":26488,
        "icon":{
            "filename":"blurry",
            "link":"/api/v1/apps/26488/icon"
        },
        "package":null,
        "version":null,
        "description":null,
        "debug":false,
        "private":true,
        "link":"/api/v1/apps/26488,
        "status":{
            "webos":"pending",
            "ios":"pending",
            "blackberry":"pending",
            "android":"pending",
            "symbian":"pending"
        },
        "error":{},
        "phonegap_version":"3.0.0",
        "build_count":null
    }

認証の必要なリポジトリ URL を指定した場合、レスポンスには `400` の HTTP ステータスコードが含まれ、レスポンス本文内にはエラーメッセージが含まれます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -d 'data={"title":"API V1 App","repo":"https://alunny@github.com/alunny/phonegap-start.git","create_method":"remote_repo"}' https://build.phonegap.com/api/v1/apps</strong></pre>
    {
        "error":"Private repository URLs not supported - try removing &quot;alunny@&quot;"
    }

#### PhoneGap Build でホストされたリポジトリ

PhoneGap Build でホストされたリポジトリをアプリケーションに対してリクエストするには、`create_method` パラメーターを `hosted_repo` に設定します。

JSON レスポンスを受信したら、アプリケーションの `repo` 属性を確認し、その git リモートにプッシュしてアプリケーションのビルドを取得できます。PhoneGap Build の認証済みの git リポジトリを使用する方法について詳しくは、[Git ホスティングに関する記事](/docs/git-hosting)を参照してください。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -d 'data={"title":"Hosted Application","create_method":"hosted_repo"}' https://build.phonegap.com/api/v1/apps</strong></pre>
    {
        "keys":{
            "ios":{
                "title":"ios-key",
                "default":true,
                "id":2,
                "link":"/api/v1/keys/ios/2"
             },
             "blackberry":null,
             "android":{
                "title":"release-key",
                "default":true,
                "id":2,
                "link":"/api/v1/keys/android/2"
             }
        },
        "download":{},
        "title":"Hosted Application",
        "repo":"git@git.phonegap.com:alunny/26500_HostedApplication.git",
        "collaborators":[
            {
                "person":"andrew.lunny@nitobi.com",
                "role":"admin"
            }
        ],
        "role":"admin",
        "id":26500,
        "icon":{
            "filename":"null",
            "link":"/api/v1/apps/26500/icon"
        },
        "package":null,
        "version":null,
        "description":null,
        "debug":false,
        "private":true,
        "link":"/api/v1/apps/26500,
        "status":{
            "webos":"pending",
            "ios":"pending",
            "blackberry":"pending",
            "android":"pending",
            "symbian":"pending"
        },
        "error":{},
        "phonegap_version":"3.0.0",
        "build_count":null
    }

#### 署名キー

PhoneGap Build でビルドに署名するには、まず 1 つ以上のキーをアップロードする必要があります。そのためには、`POST https://build.phonegap.com/api/v1/keys` メソッドまたは Web インターフェイスを使用します。同じ URL に GET リクエストを送信することで、アカウントに関連付けられたすべてのキーのリストを取得できます。

ビルドサーバーに送信する `data` JSON ハッシュ内で、このビルドで使用するプラットフォームごとのキーを ID で指定できます。

各プラットフォームの値は、以下のような整数値の ID になります。

    "keys":{"ios":123}

または、`password` フィールド（Android の場合は `key_pw` フィールドと `keystore_pw` フィールド）を含むオブジェクトとなります。

    "keys":{"ios":{"id":123,"password":"password1"}

2 つ目の形式を使用すると、個別の PUT リクエストを `https://build.phonegap.com/v1/keys/ios/123` に送信せずに、特定のキーのロックを解除できます。

サンプルのポストは以下のとおりです（1 つ目の形式を使用）。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -d 'data={"title":"Signing Keys","create_method":"hosted_repo","keys":{"ios":123,"android":567}}' https://build.phonegap.com/api/v1/apps</strong></pre>
    {
        "keys":{
            "ios":{
                "title":"new iOS key",
                "default":false,
                "id":123,
                "link":"/api/v1/keys/ios/123"
             },
             "blackberry":null,
             "android":{
                "title":"some android key",
                "default":false,
                "id":567,
                "link":"/api/v1/keys/android/567"
             }
        },
        "download":{},
        "title":"Hosted Application",
        "repo":"git@git.phonegap.com:alunny/36500_HostedApplication.git",
        "collaborators":[
            {
                "person":"andrew.lunny@nitobi.com",
                "role":"admin"
            }
        ],
        "role":"admin",
        "id":36500,
        "icon":{
            "filename":"null",
            "link":"/api/v1/apps/36500/icon"
        },
        "package":null,
        "version":null,
        "description":null,
        "debug":false,
        "private":true,
        "link":"/api/v1/apps/36500,
        "status":{
            "webos":"pending",
            "ios":"pending",
            "blackberry":"pending",
            "android":"pending",
            "symbian":"pending",
            "winphone":"pending"
        },
        "error":{},
        "phonegap_version":"3.0.0",
        "build_count":null
    }

### PUT https://build.phonegap.com/api/v1/apps/:id

既存のアプリケーション（アプリケーションの内容、アプリケーションのメタデータ、またはその両方）を更新します。レスポンスは、`GET /api/v1/apps/:id` リクエストと同様に、アプリケーションの JSON 表現となります。

メタデータを更新するには、JSON オブジェクトをパラメーター `data` として送信します。この JSON オブジェクトで使用できるオプションは以下のとおりです。

* __title__ ：アプリケーションのタイトル
* __package__ ：アプリケーションのパッケージ識別子（例：`com.phonegap.www`）
* __version__ ：アプリケーションのバージョン（例：`0.0.1`）
* __description__ ：アプリケーションの説明
* __debug__ ：アプリケーションを[デバッグモード](/docs/phonegap-debug)でビルドするかどうか
* __private__ ：アプリケーションの表示を制限するかどうか
* __phonegap_version__ ：アプリケーションで使用する PhoneGap のリリース

アプリケーションのバージョンを更新する簡単なサンプルを以下に示します。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -X PUT -d 'data={"version":"0.2.0"}' https://build.phonegap.com/api/v1/apps/8</strong></pre>
    {
        "id":8,
        "version":"0.2.0",
        "keys":{
            "ios":null,
            "blackberry":null,
            "android":null
        },
        "repo":null,
        "download":{},
        "collaborators":[
            {
                "person":"andrew.lunny@nitobi.com",
                "role":"admin"
            }
        ],
        "title":"App From API",
        "role":"admin",
        "icon":{
            "filename":null,
            "link":"/api/v1/apps/8/icon"
        },
        "package":null,
        "link":"/api/v1/apps/8",
        "debug":false,
        "private":true,
        "description":null,
        "status":{
            "webos":"pending",
            "ios":null,
            "blackberry":"pending",
            "android":"pending",
            "symbian":"pending"
        },
        "error":{},
        "phonegap_version":"3.0.0",
        "build_count":12
    }

デフォルトでは、アプリケーションはメタデータが変更された後、サポートされるすべてのプラットフォームに対してビルドされます。

#### 署名キー

新しいアプリケーションの作成と同様に、ビルドの対象となる各プラットフォームで使用する署名キーを指定できます。また、キーの資格情報を入力することもできます。この情報によってキーのロックが解除され、使用できるようになります。

アプリケーション用の新しい Android キーを選択してロックを解除するサンプルのポストを以下に示します。

<pre><strong>
$ curl -u andrew.lunny@nitobi.com -X PUT
-d 'data={"keys":{"android":
{"id":457,"key_pw":"password1","keystore_pw":"password2"}}'
https://build.phonegap.com/api/v1/apps/36500</strong></pre>
    {
        "keys":{
            "ios":{
                "title":"new iOS key",
                "default":false,
                "id":123,
                "link":"/api/v1/keys/ios/123"
             },
             "blackberry":null,
             "android":{
                "title":"changed android key",
                "default":false,
                "id":457,
                "link":"/api/v1/keys/android/457"
             }
        },
        "download":{},
        "title":"Hosted Application",
        "repo":"git@git.phonegap.com:alunny/36500_HostedApplication.git",
        "collaborators":[
            {
                "person":"andrew.lunny@nitobi.com",
                "role":"admin"
            }
        ],
        "role":"admin",
        "id":36500,
        "icon":{
            "filename":"null",
            "link":"/api/v1/apps/36500/icon"
        },
        "package":null,
        "version":null,
        "description":null,
        "debug":false,
        "private":true,
        "link":"/api/v1/apps/36500,
        "status":{
            "webos":"pending",
            "ios":"pending",
            "blackberry":"pending",
            "android":"pending",
            "symbian":"pending",
            "winphone":"pending"
        },
        "error":{},
        "phonegap_version":"3.0.0",
        "build_count":null
    }


#### ファイルベースのアプリケーションの更新

アプリケーションがファイルのアップロードにより作成された場合は、リクエスト内の `file` パラメーターに新しい `index.html`、zip ファイルまたは tar.gz ファイルを指定して、アプリケーションの内容を更新できます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -X PUT -F file=@/Users/alunny/new/index.html https://build.phonegap.com/api/v1/apps/8</strong></pre>

#### リポジトリベースのアプリケーションの更新

リモートリポジトリからアプリケーションを更新するには、`data` ハッシュに `pull` フィールドを追加し、そのフィールドを `true` に設定するだけです。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -X PUT -d 'data={"pull":"true"}' https://build.phonegap.com/api/v1/apps/8</strong></pre>

PhoneGap Build によってリモートリポジトリから新しいコードがダウンロードされ、サポートされるすべてのプラットフォーム向けにアプリケーションが再ビルドされます。

### POST https://build.phonegap.com/api/v1/apps/:id/icon

指定したアプリケーションのアイコンファイルを設定します。ポスト内で、`png` ファイルを `icon` パラメーターとして送信します。

解像度の異なる複数のアイコンが必要な場合は、この API メソッドは使用しないでください。代わりに、アプリケーションパッケージ内に複数のアイコンファイルを含めて、[config.xml ファイル](/docs/config-xml) でその使用法を指定します。

レスポンスには `201` 作成済みステータスが含まれ、アプリケーションはビルド用のキューに格納されます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -f icon=@icon.png https://build.phonegap.com/api/v1/apps/8/icon</strong></pre>

### POST https://build.phonegap.com/api/v1/apps/:id/build

指定したアプリケーションの新しいビルドをキューに格納します。古いビルドは破棄され、新しいビルドがキューに格納されます。

ビルドでは最新のアプリケーションの内容と、選択した署名キーが使用されます。レスポンスには `202`（受諾済み）ステータスが含まれます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -X POST -d '' https://build.phonegap.com/api/v1/apps/12/build</strong></pre>

ビルドするプラットフォームを選択するには、ポスト内の JSON エンコード形式のパラメーターにそれらのプラットフォームを指定します。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -X POST -d 'data={"platforms":["android","webos"]}' https://build.phonegap.com/api/v1/apps/12/build</strong></pre>

ビルドがキューに格納されたら、`GET /api/v1/apps/:id` の結果を監視することで、各プラットフォームのステータスが `pending` から（`complete` または `error` に）変更されるタイミングを確認できます。

### POST https://build.phonegap.com/api/v1/apps/:id/build/:platform

1 つのプラットフォームをビルドする場合は、以下のような簡単な URL を使用できます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -X POST -d '' https://build.phonegap.com/api/v1/apps/12/build/android</strong></pre>

### POST https://build.phonegap.com/api/v1/apps/:id/collaborators

指定したアプリケーションに対して一緒に作業する共同制作者を追加します。この操作を実行するには、アプリケーションの所有者または管理者である必要があります。

#### 必須のパラメーター

* __email__ ：新しい共同制作者の電子メールアドレス。
* __role__ ：新しい共同制作者のアクセスレベル。`tester`（読み取り専用アクセス）または `dev`（読み取りおよび書き込みアクセス）です。

ユーザーがシステム上にいる場合は、`201`（作成済み）HTTP ステータスコードが返されます。これで、ユーザーが現時点でアプリケーションにアクセスできることを確認できます。ユーザーがシステム上に登録されていない場合は、`202`（受諾済み）ステータスが返され、その共同制作者は保留中として示されます。

共同制作者が追加された後に、影響を受けるアプリケーションの JSON 表現が返されます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -d 'data={"email":"newguy@nitobi.com","role":"dev"}' https://build.phonegap.com/api/v1/apps/12/collaborators</strong></pre>
    {
        "id":12,
        "title":"App With Collaborators",
        "collaborators":{
            "link":"/api/v1/apps/9/collaborators",
            "pending":[
                {
                    "person":"newguy@nitobi.com",
                    "role":"developer"
                },
                {
                    "person":"nobody@nitobi.com",
                    "role":"tester"
                }
            ],
            "active":[
                {
                    "person":"admin@nitobi.com",
                    "role":"admin",
                    "id":9,
                    "link":"/api/v1/apps/9/collaborators/9"
                },
                {
                    "person":"foo@bar.com",
                    "role":"developer",
                    "id":13,
                    "link":"/api/v1/apps/9/collaborators/13"
                }
            ]
        },
        "package":"app.with.collaborators",
        ...
    }

### PUT https://build.phonegap.com/api/v1/apps/:id/collaborators/:id

PhoneGap Build での特定の共同制作者の役割を、`dev` または `tester` に変更できます。

アプリケーションの所有者でない場合は、`401` 未認証レスポンスが返されます。現時点では共同制作者の電子メールを変更できません。変更しようとすると、`400` ステータスが返されます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -d 'data={"role":"tester"}' -X PUT https://build.phonegap.com/api/v1/apps/12/collaborators/13</strong></pre>
    {
        "id":13,
        "person":"foo@bar.com",
        "role":"tester",
        "app":{
            "id":12,
            "download":{},
            "title":"Hosted thru API",
            "role":"admin",
            "icon":{
                "filename":null,
                "link":"/api/v1/apps/12/icon"
            },
            "version":null,
            "package":null,
            "description":null,
            "debug":null,
            "link":"/api/v1/apps/12",
            "status":{
              "ios":"pending",
              "webos":"pending",
              "blackberry":"pending",
              "android":"pending",
              "symbian":"pending",
              "winphone":"pending"
            },
            "phonegap_version":"3.0.0",
            "build_count":null,
            "error":{}
        },
        "link":"/api/v1/apps/12/collaborators/13"
    }

### POST https://build.phonegap.com/api/v1/keys/:platform

PhoneGap Build アカウントに署名キーを追加します。URL 内に `platform` パラメーターを指定する必要があります。また、ターゲットとするプラットフォームに応じて異なるファイルを用意する必要があります。

#### iOS 署名キー

iOS 向けにビルドするには、以下の情報が必要です。

* `p12` 証明書ファイル
* `mobileprovision` ファイル
* 証明書にアクセスするためのパスワード（オプション）
* 証明書とプロファイルのペアに付けたタイトル

これらのファイルの取得方法について詳しくは、[iOS 署名](/docs/ios-builds)のドキュメントを参照してください。

サンプルのポストは以下のようになります。

<pre><strong>
$ curl -u andrew.lunny@nitobi.com
-F cert=@My_Certificate.p12 -F profile=@MyDevices.mobileprovision
-F 'data={"title":"Developer Cert","password":"12345678"}'
https://build.phonegap.com/api/v1/keys/ios</strong></pre>
     {
        "title":"Developer Cert",
        "default":false,
        "id":11,
        "link":"/api/v1/keys/ios/11",
        "provision":"meandmyteam.mobileprovision",
        "cert_name":"My_Certificate.p12",
        "role":"developer",
        "locked":false
     }

`password` パラメーターを省略した場合、アップロードが完了した後にキーがロックされます。キーのロックを解除するまでは、そのキーを使用してビルドできません。

#### Android キー

Android ビルドに署名するには、以下の情報が必要です。

* `keystore` ファイル
* そのキーストアに使用しているエイリアス
* キーストアのパスワード（`keystore_pw`）（オプション）
* プライベートキーのパスワード（`key_pw`）（オプション）
* キーのタイトル

キーストアファイルおよび関連するデータの取得方法について詳しくは、[Android コード署名](/docs/android-signing)のドキュメントを参照してください。

サンプルのポストは以下のようになります。

<pre><strong>
$ curl -u andrew.lunny@nitobi.com
-F keystore=@android.keystore
-F 'data={"title":"Android Key","alias":"release",
"key_pw":"90123456","keystore_pw":"78901234"}'
https://build.phonegap.com/api/v1/keys/android</strong></pre>
    {
        "title":"Android Key",
        "default":false,
        "id":2,
        "alias":"release",
        "link":"/api/v1/keys/android/2",
        "locked":false
    }

`key_pw` パラメーターと `keystore_pw` パラメーターのどちらか一方または両方を省略した場合、アップロード後にキーがロックされます。キーのロックを解除するまでは、そのキーを使用してビルドできません。

#### BlackBerry キー

Blackberry ビルドに署名するには、以下の情報が必要です。

* `sigtool.csk` ファイル
* `sigtool.db` ファイル
* キーのパスワード（オプション）
* キーのタイトル

`sigtool` ファイルの取得方法については、[BlackBerry キー](/docs/blackberry-keys)のドキュメントを参照してください。

サンプルのポストは以下のようになります。

<pre><strong>
$ curl -u andrew.lunny@nitobi.com
-F db=@sigtool.db -F csk=@sigtool.csk
-F 'data={"title":"My BB Key","password":"78901234"}'
https://build.phonegap.com/api/v1/keys/blackberry</strong></pre>
    {
        "title":"My BB Key",
        "default":false,
        "id":2,
        "link":"/api/v1/keys/blackberry/2",
        "locked":false
    }

`password` パラメーターを省略した場合、アップロードが完了した後にキーがロックされます。キーのロックを解除するまでは、そのキーを使用してビルドできません。

### PUT https://build.phonegap.com/api/v1/keys/:platform/:id

PhoneGap Build で既存の署名キーを更新します。署名キーを今後のビルドでも使用できるように、ロックを解除するために使用します。キーのロックを解除するには、適切な資格情報を指定する必要があります。iOS または BlackBerry では 1 つのパスワード、Android では 2 つのパスワード（キーのパスワードとキーストアのパスワード）です。

PhoneGap Build では、キーのパスワードは検証されません。パスワードが正しくない場合、そのキーを使用してビルドを実行しようとするとエラーが発生します。

#### IOS サンプル

<pre><strong>
$ curl -u andrew.lunny@nitobi.com 
-d 'data={"password":"password1"}'
-X PUT
https://build.phonegap.com/api/v1/keys/ios/11</strong></pre>
     {
        "title":"Developer Cert",
        "default":false,
        "id":11,
        "link":"/api/v1/keys/ios/11",
        "provision":"meandmyteam.mobileprovision",
        "cert_name":"My_Certificate.p12",
        "role":"developer",
        "locked":false
     }

#### Android サンプル

<pre><strong>
$ curl -u andrew.lunny@nitobi.com 
-d 'data={"key_pw":"password1","keystore_pw":"password2"}'
-X PUT
https://build.phonegap.com/api/v1/keys/android/2</strong></pre>
    {
        "title":"Android Key",
        "default":false,
        "id":2,
        "alias":"release",
        "link":"/api/v1/keys/android/2",
        "locked":false
    }

#### Blackberry サンプル

<pre><strong>
$ curl -u andrew.lunny@nitobi.com 
-d 'data={"password":"password1"}'
-X PUT
https://build.phonegap.com/api/v1/keys/blackberry/2</strong></pre>
    {
        "title":"My BB Key",
        "default":false,
        "id":2,
        "link":"/api/v1/keys/blackberry/2",
        "locked":false
    }

### DELETE https://build.phonegap.com/api/v1/apps/:id

PhoneGap Build からアプリケーションを削除します。`202`（受諾済み）ステータスまたは `404` ステータス（アプリケーションが見つからない場合）が返されます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -X DELETE https://build.phonegap.com/api/v1/apps/8</strong></pre>
    {
        "success":"app 8 deleted"
    }

### DELETE https://build.phonegap.com/api/v1/apps/:id/collaborators/:id

所有するプロジェクトから共同制作者を削除します。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -X DELETE https://build.phonegap.com/api/v1/apps/12/collaborators/13</strong></pre>
    {
        "success":"foo@bar.com removed from app 9"
    }

### DELETE https://build.phonegap.com/api/v1/keys/:platform/:id

PhoneGap Build から署名キーを削除します。`202`（受諾済み）ステータスまたは `404` ステータス（キーが見つからない場合）が返されます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com -X DELETE https://build.phonegap.com/api/v1/keys/android/8</strong></pre>
    {
        "success":"android key 8 deleted"
    }
