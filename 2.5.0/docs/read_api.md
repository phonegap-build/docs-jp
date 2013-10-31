# 読み取り API V1

このドキュメントは、Adobe® PhoneGap™ Build API V1 ドキュメントの一部です。以下のドキュメントも参照してください。

* [API 概要](/docs/api)
* [書き込み API](/docs/write_api)

このドキュメントで使用するサンプルのレスポンスは、読みやすくするために整形しています。実際の JSON のレスポンスには空白はそれほど多く含まれません。

### GET https://build.phonegap.com/api/v1/me

認証済みユーザーに関する JSON エンコード表現および関連するリソースのリストを取得します。

これは、PhoneGap Build API を走査するアプリケーションの開始点となります。この URL には、`https://build.phonegap.com/api/v1` というエイリアスが設定されています。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/me</strong></pre>
    {   
        "id": 1,
        "username":"alunny",
        "email":"andrew.lunny@nitobi.com",
        "apps": {
            "id": 2,
            "link": "/api/v1/apps",
            "all": [
                {
                    "title": "A Single App",
                    "role": "owner",
                    "link": "/api/v1/apps/1234"
                }
            ]
        },
        "keys": {
            "ios": {
                "all":[
                    {
                        "id": 34,
                        "default":true,
                        "title": "iOS Development Key",
                        "link": "/api/v1/keys/ios/34"
                    },
                    {
                        "id": 82,
                        "default":false,
                        "title": "iOS Distribution Key",
                        "link": "/api/v1/keys/ios/82"
                    }
                ],
                "link":"/api/v1/keys/ios"
            },
            "blackberry": {
                "all":[
                    {
                        "id": 12,
                        "default":false,
                        "title": "My BlackBerry Key",
                        "link": "/api/v1/keys/blackberry/12"
                    }
                ],
                "link":"/api/v1/keys/blackberry"
            },
            "android": {
                "all":[
                    {
                        "id": 56,
                        "default":false,
                        "title": "Android Release Certificate",
                        "link": "/api/v1/keys/android/56"
                    }
                ],
                "link":"/api/v1/keys/android"
            },
            "link": "/api/v1/keys"
        },
        "link": "/api/v1/me"
    }

### GET https://build.phonegap.com/api/v1/apps

認証済みユーザーのアプリケーションの JSON エンコード表現を取得します。

API クライアントは各アプリケーションの `link` 属性を追跡することで、関連する署名キーや共同制作者などの詳細情報を取得できます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/apps</strong></pre>
    {
        "apps":[
            {
                "title":"My Index",
                "id":1,
                "package":"com.my.index",
                "version":"0.0.1",
                "repo":null,
                "description":"An Index of My Applications",
                "debug":false,
                "private":true,
                "link":"/api/v1/apps/1",
                "build_count":4,
                "phonegap_version":"3.0.0",
                "status":{
                    "android":"complete",
                    "blackberry":"error",
                    "ios":null,
                    "symbian":"complete",
                    "webos":"pending",
                    "winphone":"pending"
                },
                "download":{
                    "android":"/api/v1/apps/1/android",
                    "symbian":"/api/v1/apps/1/symbian"
                },
                "error":{
                    "blackberry":"invalid widget archive"
                },
                "icon":{
                    "filename":"icon.png",
                    "link":"/api/v1/apps/1/icon"
                },
                "role":"admin"
            },
            {
                "title":"PhoneGap: Getting Started",
                "id":2,
                "package":"com.phonegap.getting.started",
                "version":"1.0.0",
                "repo":"https://github.com/phonegap/phonegap-start.git",
                "description":"A template for getting started with
                        PhoneGap development and build.phonegap.com",
                "debug":false,
                "private":true,
                "link":"/api/v1/apps/2",
                "build_count":12,
                "status": {
                    "android":"complete",
                    "blackberry":"complete",
                    "ios":"complete",
                    "symbian":"complete",
                    "webos":"complete",
                    "winphone":"complete"
                },
                "download":{
                    "android":"/api/v1/apps/1/android",
                    "blackberry":"/api/v1/apps/1/blackberry",
                    "ios":"/api/v1/apps/1/ios",
                    "symbian":"/api/v1/apps/1/symbian",
                    "webos":"/api/v1/apps/1/webos",
                    "winphone":"/api/v1/apps/1/winphone"
                },
                "error":{},
                "icon":{
                    "filename":"big-icon.png",
                    "link":"/api/v1/apps/2/icon"
                },
                "role":"admin"
            }
        ],
        "link":"/api/v1/apps"
    }

### GET https://build.phonegap.com/api/v1/apps/:id

特定のアプリケーションの JSON エンコード表現を取得します（認証済みユーザーにそのアプリケーションへのアクセス権がある場合）。

すべてのアプリケーションのリストで表示されるフィールドに加えて、この詳細表示には以下の情報が含まれます。

  * `keys`：アプリケーションの現在のビルドに使用されているすべてのキー。プラットフォームを選択した場合は、そのプラットフォームの所有者のデフォルトキーも含まれます。
  * `collaborators`：認証済みのユーザーがアプリケーションの所有者の場合、このアプリケーションにアクセスできる個人とその人の役割。PhoneGap Build に登録されている共同制作者は `active` の下に示されます。招待したがまだアカウントを作成していない共同制作者は `pending` として示されます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/apps/2</strong></pre>
    {
        "title":"PhoneGap: Getting Started",
        "id":2,
        "package":"com.phonegap.getting.started",
        "version":"1.0.0",
        "repo":"https://github.com/phonegap/phonegap-start.git",
        "description":"A template for getting started with
                PhoneGap development and build.phonegap.com",
        "debug":false,
        "private":true,
        "link":"/api/v1/apps/2",
        "build_count":12,
        "status": {
            "android":"complete",
            "blackberry":"complete",
            "ios":"complete",
            "symbian":"complete",
            "webos":"complete",
            "winphone":"complete"
        },
        "download":{
            "android":"/api/v1/apps/1/android",
            "blackberry":"/api/v1/apps/1/blackberry",
            "ios":"/api/v1/apps/1/ios",
            "symbian":"/api/v1/apps/1/symbian",
            "webos":"/api/v1/apps/1/webos",
            "winphone":"/api/v1/apps/1/winphone"
        },
        "error":{},
        "icon":{
            "filename":"big-icon.png",
            "link":"/api/v1/apps/2/icon"
        },
        "role":"admin",
        "keys":{},
        "collaborators":{
            "link":"/api/v1/apps/9/collaborators",
            "active":[
                {
                    "id":9,
                    "person":"andrew.lunny@nitobi.com",
                    "role":"admin",
                    "link":"/api/v1/apps/9/collaborators/9"
                },
                {
                    "id":13,
                    "person":"foo@bar.com",
                    "role":"developer",
                    "link":"/api/v1/apps/9/collaborators/13"
                }
            ],
            "pending":[
                {
                    "person":"nobody@nitobi.com",
                    "role":"tester"
                }
            ]
        }
    }

アプリケーションが存在しない場合またはアプリケーションにアクセスできない場合は、エラーメッセージがステータスコード `404` と共に返されます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/apps/520394</strong></pre>
    {
        "error":"app #54 not available"
    }

### GET https://build.phonegap.com/api/v1/apps/:id/icon

アプリケーションに関連付けられているメインアイコンを取得します。このアイコンは、`config.xml` ファイル内で指定されている最大のアイコンか、API または PhoneGap Build Web インターフェイスを使用してアップロードしたアイコンのいずれかです。

成功した場合、この API メソッドにより、アイコンファイルへの 302 リダイレクトが返されます。レスポンスの実際の本文は対象のリソースを示しています。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/apps/2/icon</strong></pre>
    {
        "location":""http://s3.amazonaws.com/build.phonegap.com/some-long-guid/icon.png"
    }

api クライアントでリダイレクトを追跡できる場合は、レスポンスを `png` ファイルとして保存できます（curl では、`-L` オプションを指定して実行します）。

<pre><strong>$ curl -Lu andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/apps/2/icon > ~/my-icon.png</strong></pre>

取得できるアイコンがない場合は、エラーメッセージがステータスコード 404 と共に返されます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v0/apps/52/icon</strong></pre>

    {
        "error":"No icon available for app #52"
    }

### GET https://build.phonegap.com/api/v1/apps/:id/:platform

指定したプラットフォーム用のアプリケーションパッケージをダウンロードします。利用可能なプラットフォームは、`android`、`blackberry`、`ios`、`symbian`、`webos` および `winphone` です。

成功した場合、この API メソッドにより、アプリケーションバイナリへの 302 リダイレクトが返されます。レスポンスの実際の本文はリソースの正確な場所を示しています。

<pre><strong>$ curl -Lu andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/apps/50/android</strong></pre>
    {
        "location":""http://s3.amazonaws.com/build.phonegap.com/some-long-guid/app.apk"
    }

api クライアントでリダイレクトを追跡できる場合、レスポンスを直接保存できます。

<pre><strong>$ curl -Lu andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/apps/50/android > app_50.apk</strong></pre>

直接ダウンロードする場合は、ダウンロードするファイルの拡張子が正しいことを確認してください。

* `apk`（Android）
* `ipa`（iOS）
* `ipk`（webOS）
* `jad`（未署名の BlackBerry ビルド）、`zip`（BlackBerry 署名キーがアップロードされている場合）
* `wgz`（Symbian）
* `xap`（Windows Phone）

指定したプラットフォーム用のアプリケーションパッケージが利用できない場合は、エラーメッセージがステータスコード `404` と共に返されます。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/apps/52/android</strong></pre>
    {
        "error":"app #52 download unavailable for android"
    }

### GET https://build.phonegap.com/api/v1/keys

アカウントに関連付けられているすべての署名キーの JSON エンコードリストを取得します。

これによって、関連付けられたすべてのキーの短いリストが返されます。このリストは、`/api/v1/me` をリクエストした場合に表示されるリストに似ています。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/keys</strong></pre>
    {
        "keys":{
            "ios":{
                "all":[
                    {
                        "id":8,
                        "title":"My Dev Certificate",
                        "default":false,
                        "cert_name":"My_Dev_Cert.p12",
                        "provision":"My_Devices.mobileprovision",
                        "link":"/api/v1/keys/ios/8",
                        "role":"developer",
                        "locked":true
                    }
                ],
                "link":"/api/v1/keys/ios"
            },
            "blackberry":{
                "all":[
                    {
                        "id":6,
                        "title":"I make bb apps too",
                        "default":false,
                        "link":"/api/v1/keys/blackberry/1",
                        "locked":true
                    }
                ],
                "link":"/api/v1/keys/blackberry"
            },
            "android":{
                "all":[
                    {
                        "id":1,
                        "title":"Android Release Key",
                        "default":false,
                        "alias":"release",
                        "link":"/api/v1/keys/android/1",
                        "locked":true
                    }
                ],
                "link":"/api/v1/keys/android"
            }
        },
        "link":"/api/v1/keys"
    }

### GET https://build.phonegap.com/api/v1/keys/:platform

特定のプラットフォームのアカウントに関連付けられているすべての署名キーの JSON エンコードリストを取得します。このプラットフォームは、`ios`、`android` または `blackberry` のいずれかです。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/keys/ios</strong></pre>
    {
        "keys":[
            {
                "id":8,
                "title":"My Dev Certificate",
                "default":false,
                "cert_name":"My_Dev_Cert.p12",
                "provision":"My_Devices.mobileprovision"
                "link":"/api/v1/keys/ios/8",
                "role":"developer",
                "locked":true
            }
        ],
        "link":"/api/v1/keys/ios"
    }

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/keys/android</strong></pre>
    {
        "keys":[
            {
                "id":1,
                "title":"Android Release Key",
                "default":false,
                "alias":"releasing",
                "link":"/api/v1/keys/android/1",
                "locked":true
            }
        ],
        "link":"/api/v1/keys/android"
    }

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/keys/blackberry</strong></pre>
    {
        "keys":[
            {
                "id":1,
                "title":"I make bb apps too",
                "default":false,
                "link":"/api/v1/keys/blackberry/1",
                "locked":true
            }
        ],
        "link":"/api/v1/keys/blackberry"
    }

### GET https://build.phonegap.com/api/v1/keys/:platform/:id

1 つの署名キーの JSON エンコード表現を取得します。

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/keys/ios/8</strong></pre>
    {
        "id":8,
        "title":"My Dev Certificate",
        "default":false,
        "cert_name":"My_Dev_Cert.p12",
        "provision":"My_Devices.mobileprovision"
        "link":"/api/v1/keys/ios/8",
        "role":"developer",
        "locked":true
    }

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/keys/android/1</strong></pre>
    {
        "id":1,
        "title":"Android Release Key",
        "default":false,
        "alias":"releasing",
        "link":"/api/v1/keys/android/1",
        "locked":true
    }

<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/keys/blackberry/1</strong></pre>
    {
        "id":1,
        "title":"I make bb apps too",
        "default":false,
        "link":"/api/v1/keys/blackberry/1",
        "locked":true
    }

リクエストしたキーを取得できない場合は、JSON のエラーメッセージと共に 404 ステータスが返されます。


<pre><strong>$ curl -u andrew.lunny@nitobi.com https://build.phonegap.com/api/v1/keys/ios/8989898</strong></pre>
    {
        "error":"could not find ios key #8989898"
    }
