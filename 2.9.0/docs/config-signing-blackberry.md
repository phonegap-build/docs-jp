---
license: Licensed to the Apache Software Foundation (ASF) under one
         or more contributor license agreements.  See the NOTICE file
         distributed with this work for additional information
         regarding copyright ownership.  The ASF licenses this file
         to you under the Apache License, Version 2.0 (the
         "License"); you may not use this file except in compliance
         with the License.  You may obtain a copy of the License at

           http://www.apache.org/licenses/LICENSE-2.0

         Unless required by applicable law or agreed to in writing,
         software distributed under the License is distributed on an
         "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
         KIND, either express or implied.  See the License for the
         specific language governing permissions and limitations
         under the License.
---

# BlackBerry のキー設定の署名

Adobe® PhoneGap™ Build では現在、すべてのユーザーに対してデフォルトの BlackBerry 開発バージョンを提供しています。この開発バージョンでは、PhoneGap アプリケーションの Over-The-Air インストールを使用できます。ただし、独自の BlackBerry アプリケーションを配布するには、RIM に独自のキーを登録し、それらのキーを PhoneGap Build に読み込む必要があります。

登録するには、[RIM のサイトのフォーム](https://www.blackberry.com/SignedKeys/)に情報を入力し、キーを受け取ったら、ローカルでインストールプロセスを実行してください。

__重要__ ：PhoneGap Build では現在、スマートフォン用の BlackBerry ビルドのみをサポートしています。タブレット用のビルドはサポートしていません。取得して読み込むキーは、スマートフォン用のキーであることを確認してください。

## キーの検索

独自のシステムにキーをインストールした後は、そのキーを取得して PhoneGap Build に送信できます。このプロセスは簡単です。

1. キーをインストールした SDK ディレクトリの検索
-------------------------------------------------------

### Eclipse を使用してインストールした場合

    C:\Eclipse-3.5.2\plugins\net.rim.ejde.componentpack5.0.0_5.0.0.25\components\

- Eclipse ディレクトリパスは `C:\Eclipse-3.5.2\` とは異なる場合があります。
- プラグインコンポーネントのパスは `net.rim.ejde.componentpack5.0.0_5.0.0.25` とは異なる場合があります。
- 一般的な形式は net.rim.ejde.componentpackX.X.X_X.X.X.X です。
- その他のパスの例： `C:\Program Files\eclipse\plugins\net.rim.ejde\vmTools`

### インストール済みの BlackBerry Widget/WebWorks Packager Standalone SDK

# 32 ビット
    C:\Program Files\Research In Motion\BlackBerry Widget Packager\

# 64 ビット
    C:\Program Files (x86)\Research In Motion\BlackBerry Widget Packager\

# PhoneGap Wiki の推奨ディレクトリ
    C:\bbwp\

2. コード署名ファイルの検索
-------------------------------

    C:\SDK_PATH\bin\sigtool.csk
    C:\SDK_PATH\bin\sigtool.db

`sigtool.csk` には、データベースのプライベートキーとその他の情報（パスワードと、インストール中に割り当てたランダムのマウス入力およびキーボード入力）が含まれる場合があります。

`sigtool.db` には、RIM のサーバーに接続するための資格情報が含まれる場合があります。

## PhoneGap Build へのキーの読み込み

**PhoneGap Build** では、アプリケーションのビルドと署名のために、これらの両方のファイルが必要です。

キーを読み込むには、[プロファイルページ](/people/edit)に移動し、下にスクロールして署名キーを表示して、 _BlackBerry_ の下の「キーを追加」をクリックします。

  ![BlackBerry キーモーダルフォーム](images/blackberry-keys/blackberry-form.png)

ローカルでのキーのインストール時に入力したパスワードと同じパスワードを入力してください。「タイトル」にはキーを識別するための任意の情報を入力できます。

インストール後のキーは、デフォルトの BlackBerry キーとして設定できます（これにより、すべての BlackBerry ビルドでこのキーが自動的に使用されます）。または、アプリケーションごとに、このキーを使用することもできます。それでは、ビルドをお楽しみください。
