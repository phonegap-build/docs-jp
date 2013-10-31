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

# プラグインの使用

Adobe® PhoneGap™ Build では、PhoneGap のネイティブアプリケーションコンテナで公開されているネイティブ機能を拡張する、精選された PhoneGap プラグインをサポートしています。

プラグインの実装方法はそれぞれのプラットフォームで異なります。また、プラグインは一部の PhoneGap プラットフォームではサポートされない場合があります。複数のプラットフォームに対してプラグインをデプロイする場合は、プラグインを利用できないユーザーに対しては、問題は発生しませんが、操作感が低下することに注意してください。

プラグインを PhoneGap Build に提供していただける場合は、[関連ドキュメント](contributing-plugins)を参照してください。

## プロジェクトへのプラグインのインクルード

プロジェクトにプラグインをインクルードするには、プラグイン用の JavaScript コードの参照、ネイティブコードの読み込みという 2 つの手順を実行します。

<a name="javascripts"></a>
### JavaScript コードの参照

`phonegap.js` と同様にプラグイン用の JavaScript コードも、ビルド時に PhoneGap Build によってプロジェクトに挿入されます。プラグインは通常、既にロードされている PhoneGap に依存しているので、以下のように `phonegap.js` タグの後に script タグを挿入します。

    <script src="phonegap.js"></script>
    <script src="barcodescanner.js"></script>

アプリケーションにプラグインの javascript またはその他のプラグインファイルを **含めない** でください。これらのファイルは PhoneGap Build によって挿入されますので、これらを含めておくと問題が発生する場合があります。

### ネイティブコードの読み込み

PhoneGap Build プロジェクトにネイティブコードを読み込むには、お使いの [config.xml](config-xml) ファイルに、正しい `<gap:plugin>` タグを追加する必要があります。Example プラグインのタグは以下のとおりです。

    <gap:plugin name="Example" />

実行するプラグインのバージョンを `version` 属性で指定できます。この属性はオプションです。

    <gap:plugin name="Example" version="2.2.1" />

また、チルダ（~）演算子を使用して、バージョンをあいまいに指定できます。これによって、メジャーバージョンの部分が同じである最新バージョンのプラグインを指定できます。
例えば、前述のタグを以下のように置き換えることができます。

    <gap:plugin name="Example" version="~2" />

この結果、最新の 2.x バージョンがロードされますが、メジャーバージョン（先頭のバージョン番号）の異なるバージョンはロードされません。また、以下のバージョンのタグがあるとします。

    <gap:plugin name="Example" version="~2.2" />

この場合、x が 2 以上の最新の 2.x バージョンがロードされます。また、以下のバージョンのタグがあるとします。

    <gap:plugin name="Example" version="~2.2.3" />

この場合、x が 3 以上の最新の 2.2.x バージョンがロードされます。

プラグインには、設定情報を記述する必要がある場合があります。これを行うには、`<gap:plugin>` タグに子の `<param>` を追加します。

    <gap:plugin name="ExampleAPI">
        <param name="APIKey" value="12345678" />
        <param name="APISecret" value="12345678" />
    </gap:plugin>

## サポートされるプラグイン

<a name="barcodescanner"></a>
### BarcodeScanner

* サポートされるプラットフォーム：`iOS`、`Android`

BarcodeScanner プラグインを使用すると、アプリケーションでは、デバイスのカメラを使用して様々な種類のバーコードからデータを取得できます。このプラグインはスキャナーインターフェイスを起動し、バーコードを検出したとき（またはユーザーがキャンセルしたとき）、アプリケーションに制御を返して JavaScript コールバックを呼び出します。

BarcodeScanner プラグインは PhoneGap 2.0.0 以降でサポートされます。

BarcodeScanner プラグインをインクルードするには、`index.html` ページに `<script>` タグを追加します。

    <script src="phonegap.js"></script>
    <script src="barcodescanner.js"></script>

さらに、`config.xml` に適切な `gap:plugin` タグを追加します。

    <gap:plugin name="BarcodeScanner" /> <!-- latest release -->

JavaScript API 一式については、[プラグインの README](https://github.com/wildabeast/BarcodeScanner/blob/master/README.md) を参照してください。

<a name="analytics"></a>
### Analytics

* サポートされるプラットフォーム：`iOS`、`Android`

Analytics プラグインを使用すると、アプリケーションで Google Analytics アカウントに利用状況のメトリックを送信できます。

Analytics プラグインは PhoneGap 2.0.0 以降でサポートされます。

Analytics プラグインをインクルードするには、`index.html` ページに `<script>` タグを追加します。

    <script src="phonegap.js"></script>
    <script src="GAPlugin.js"></script>

さらに、`config.xml` に適切な `gap:plugin` タグを追加します。

    <gap:plugin name="GAPlugin" /> <!-- latest release -->

JavaScript API 一式については、[プラグインの README](https://github.com/phonegap-build/GAPlugin/blob/master/README.md) を参照してください。

<a name="genericpush"></a>
### GenericPush

* サポートされるプラットフォーム：`iOS`、`Android`

GenericPush プラグインを使用すると、アプリケーションで、iOS の APNS サーバーまたは Android の GCM サーバーに登録したり、これらのサーバーからプッシュ通知を受信したりできます。

GenericPush プラグインは PhoneGap 2.0.0 以降でサポートされます。

GenericPush プラグインをインクルードするには、`index.html` ページに `<script>` タグを追加します。

    <script src="phonegap.js"></script>
    <script src="PushNotification.js"></script>

さらに、`config.xml` に適切な `gap:plugin` タグを追加します。

    <gap:plugin name="GenericPush" /> <!-- latest release -->

JavaScript API 一式については、[プラグインの README](https://github.com/phonegap-build/PushPlugin/blob/master/README.md) を参照してください。

また、[Example フォルダー](https://github.com/phonegap-build/PushPlugin/tree/master/Example)を調べて、全体的な構成を確認してください。

<a name="facebookconnect"></a>
### FacebookConnect

* サポートされるプラットフォーム：`iOS`、`Android`

FacebookConnect プラグインを使用すると、Web アプリケーションで使用するものと同じ JavaScript コードを Cordova アプリケーションで使用できます。ただし、ブラウザーとは異なり、Cordova アプリケーションではネイティブの Facebook アプリケーションを使用して、ユーザーのシングルサインオンを実行します。このシングルサインオンが実行できない場合は、サインオンは、標準のダイアログベースの認証を使用して適切に実施されます。

PhoneGap（Cordova）2.3.0 以降でサポートされます。

1. [https://developers.facebook.com/apps](https://developers.facebook.com/apps) に移動し、アプリケーションを登録します。以下の手順では、`App ID` および `Display Name` が必要になります。

2. `index.html` ページに以下の `<script>` タグを追加します。

        <script src="cdv-plugin-fb-connect.js"></script>
        <script src="facebook-js-sdk.js"></script>

3. アプリケーションの `APP_ID`（Facebook アプリケーション設定ページの「App ID」）および `APP_NAME`（Facebook アプリケーション設定ページの「Display Name」)を含む適切な `gap:plugin` タグを `config.xml` に追加します。

        <gap:plugin name="FacebookConnect">
          <param name="APP_ID" value="123456" />
          <param name="APP_NAME" value="ContosoMobile" />
        </gap:plugin>

4. Facebook API ドキュメントに記載されているとおり、APP_ID は JavaScript コード内にも指定する必要があります。

Facebook API ドキュメントは、[ここ](https://developers.facebook.com/docs/reference/apis/)にあります。

詳しくは、[プラグインの README](https://github.com/phonegap-build/FacebookConnect) を参照してください。

[サンプル](https://github.com/phonegap-build/FacebookConnect/tree/master/example)も同じリポジトリ内にあります。

## プラグインの提供

PhoneGap プラグインは、`plugin.xml` ファイルを使用することで PhoneGap Build との互換性を確保できます。このファイルは、ソフトウェアを使用するための README です。

現時点では、独自のプラグインを PhoneGap Build に送信して、弊社のシステムに追加することはできません。弊社ではこれをサポートするために、インフラストラクチャの変更に取りかかっています。

このファイルの形式は現時点では明確に定義されていません。例については、[BarcodeScanner の XML ファイル](https://github.com/phonegap-build/BarcodeScanner/blob/master/plugin.xml)を参照してください。`plugin.xml` ファイルをローカルでテストするために、[`pluginstall` スクリプト](https://github.com/alunny/pluginstall)を使用できます。このスクリプトを使用してプラグインをインストールできる場合は、そのプラグインは PhoneGap Build でも実行できる可能性があります。

プラグインの提供に関心がある場合、またはプラグインの仕様策定やツールの作成に関心がある場合は、[Twitter でお問い合わせください](http://twitter.com/PhoneGapBuild)。
