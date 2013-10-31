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

# config.xml を使用したアプリケーションの設定

Adobe® PhoneGap™ Build を使用してビルドされるアプリケーションは、PhoneGap の Web インターフェイスまたは `config.xml` を使用して設定できます。[W3C のウィジェット仕様](http://www.w3.org/TR/widgets/)で定義されているように、`config.xml` ファイルを使用すると、開発者はアプリケーションに関するメタデータを容易に指定できます。サンプルの `config.xml` については、[PhoneGap Start](https://github.com/phonegap/phonegap-start/blob/master/www/config.xml) アプリケーションで確認できます。

注意：`config.xml` ファイルは、アプリケーションの最上位の階層（`index.html` ファイルと同じ階層）に必ず配置してください。この場所に配置しない場合、正しくロードされません。

PhoneGap Build 開発者がアプリケーションをより詳細にカスタマイズできるように、サポートされる `config.xml` に対して継続的に機能を追加しています。サポートを希望する具体的な機能がある場合は、[お知らせください](http://getsatisfaction.com/nitobi/products/nitobi_phonegap_build)。

## 重要なプロパティ

* `<widget>`：widget 要素は XML ドキュメントのルートである必要があります。この要素は、W3C 仕様に従っていることを通知します。PhoneGap Build を使用するときは、widget 要素に以下の属性を設定してください。
* `id`：アプリケーションの一意の識別子。サポート対象のすべてのプラットフォームをサポートするには、この属性を逆ドメイン形式（例：`com.yourcompany.yourapp`）で指定する必要があります。
* `version`：最適な結果を得るために、メジャー/マイナー/パッチ形式のバージョンを 3 つの番号で指定します（例：`0.0.1`）。
* `versionCode`：（オプション）Android 向けにビルドする場合、versionCode を *config.xml* 内に指定することで設定できます。Android の versionCode 属性について詳しくは、[Android のドキュメント](http://developer.android.com/guide/publishing/versioning.html)を参照してください。 

* `<name>`：アプリケーションの名前。

* `<description>`：アプリケーションの説明。 

#### 注意：
  
BlackBerry では、`<name>` 属性内でラテン文字のみをサポートしています。

BlackBerry では `<description>` 要素にあまり長い文字列は設定できません。

#### 使用法：
    
    <?xml version="1.0" encoding="UTF-8" ?>
        <widget xmlns = "http://www.w3.org/ns/widgets"
            xmlns:gap = "http://phonegap.com/ns/1.0"
            id        = "com.phonegap.example"
            versionCode="10" 
            version   = "1.0.0">
        
        <!-- versionCode is optional and Android only -->

        <name>PhoneGap Example</name>

        <description>
            An example for phonegap build docs. 
        </description>

        <author href="https://build.phonegap.com" email="support@phonegap.com">
            Hardeep Shoker 
        </author>

    </widget>

<a name="preferences"></a>
## 環境設定

* `<preference>`：`config.xml` 内にはこの要素をゼロ個以上指定できます。1 つも指定しない場合は、デフォルトのプロパティが適用されます。
* `name`：必須
* `value`：必須

### マルチプラットフォーム

#### PhoneGap バージョン

* `phonegap-version`（選択した PhoneGap のリリースを指定）
* 例： `<preference name="phonegap-version" value="2.5.0" />`
* 現在サポートされているバージョンは、__2.5.0__、__2.7.0__、__2.9.0__、__3.0.0__ および __3.1.0__ です（デフォルト）。
* __2.0.0__ 以前のすべてのバージョンは非推奨です。
* `phonegap-version` 環境設定を指定した場合、すべてのビルドがそのバージョンに設定されます。指定しない場合は、アプリケーションは現在のデフォルトのバージョンに設定されます。どちらの場合でも、後で変更することができます。
* サポートされていないバージョン番号を指定した場合は、アプリケーションはビルドされません。

#### デバイスの向き

* `orientation`（指定可能な値は `default`、`landscape` または `portrait`）
* 例： `<preference name="orientation" value="landscape" />`
* `default` では、横（landscape）と縦（portrait）の __両方__ が有効になります。各プラットフォームのデフォルト設定（通常は縦のみ）を使用する場合は、`config.xml` からこのタグを削除してください。

#### 特定デバイスのターゲット設定

* `target-device`（指定可能な値は `handset`、`tablet` または `universal`）
* 例： `<preference name="target-device" value="universal" />`
* 注意：この設定は現時点では iOS ビルドのみに適用されます（デフォルトではすべてのビルドが universal です）。 

#### フルスクリーンモード

* `fullscreen`（値は `true` または `false`）
* 例： `<preference name="fullscreen" value="true" />`
* 画面上部のステータスバーを非表示にします。デフォルトは false です。

<a name="ios-prefs"></a>
### iOS 固有設定

#### WebView バウンス

* `webviewbounce`（値は `true` または `false`）
* 例： `<preference name="webviewbounce" value="false" />`
* iOS で画面の上部または下部よりも先にスクロールしようとした場合に、画面を「バウンス（跳ねるように戻す）」させるかどうかを制御します。デフォルトでは、バウンスはオンです。

#### アイコンの事前レンダリング

* `prerendered-icon`（値は `true` または `false`）
* 例： `<preference name="prerendered-icon" value="true" />`
* アイコンが事前にレンダリングされている場合、iOS ではユーザーのホーム画面上に配置されるアプリケーションのアイコンに光沢を適用しません。
* デフォルトは _false_ です。

#### WebView ですべてのリンクを開く

* __非推奨__ -- ターゲットが '_self'（webview）、'_blank'（InAppBrowser）、'_system'（システム Web ブラウザー）の場合は、<a href="http://docs.phonegap.com/jp/2.7.0/cordova_inappbrowser_inappbrowser.md.html#InAppBrowser">InAppBrowser</a> を使用してください。 
* `stay-in-webview`（値は `true` または `false`）
* 例： `<preference name="stay-in-webview" value="true" />`
* true に設定した場合、すべてのリンク（ターゲットを空に設定しているものを含む）がアプリケーションの WebView で開きます。
* サーバーから取得したページにアプリケーション全体を引き継がせる場合にのみ、この環境設定を使用してください。
* デフォルトは _false_ です。

<a name="ios-statusbarstyle"></a>
#### ステータスバーのスタイル

* `ios-statusbarstyle`（値は `default`、`black-opaque` または `black-translucent`）
* 例： `<preference name="ios-statusbarstyle" value="black-opaque" />`
* デフォルトは灰色のステータスバーです。`black-opaque` の場合は黒で表示されます。
* `black-translucent` もサポートされていますが、PhoneGap WebView はステータスバーの下側に開かないので、アプリケーションを実行した後は `black-opaque` と同様に表示されます。

<a name="ios-datadetector"></a>
#### データ型の検出

* `detect-data-types`（値は `true` または `false`）
* 例： `<preference name="detect-data-types" value="false" />`
* 特定のデータ型（電話番号や日付など）をシステムで自動的にリンクに変換するかどうかを制御します。デフォルトは「true」です（システムの web view と同様）。
* PhoneGap 2.0.0 以降でサポートされます。

#### 一時停止時に終了

* `exit-on-suspend`（値は `true` または `false`）
* 例： `<preference name="exit-on-suspend" value="true" />`
* true に設定した場合、一時停止したときに（ホームボタンを押した場合など）、アプリケーションが終了します。
* デフォルトは _false_ です。

#### スプラッシュスクリーンスピナーの表示

* `show-splash-screen-spinner`（値は `true` または `false`）
* 例： `<preference name="show-splash-screen-spinner" value="false" />`
* false に設定した場合、アプリケーションをロードしているときに、スプラッシュスクリーンにスピナーが表示されません。
* デフォルトは _true_ です。

#### スプラッシュスクリーンを自動で非表示

* `auto-hide-splash-screen`（値は `true` または `false`）
* 例： `<preference name="auto-hide-splash-screen" value="false" />`
* false に設定した場合、スプラッシュスクリーンを非表示にするには JavaScript API を使用する必要があります。
* デフォルトは _true_ です。

<a name="bb-prefs"></a>
### BlackBerry 固有設定

#### カーソルの無効化

* `disable-cursor`（値は `true` または `false`）
* 例： `<preference name="disable-cursor" value="true" />`
* マウスアイコンまたはカーソルがアプリケーション上に表示されなくなります。`<rim:navigation />` に脱糖されます。詳しくは、[BlackBerry のドキュメント](https://bdsc.webapps.blackberry.com/html5/documentation/ww_developing/rim_navigation_element_1582456_11.html)を参照してください。
* デフォルトは _false_ です。

<a name="android-prefs"></a>
### Android 固有設定

#### 最小および最大の SDK バージョン

* `android-minSdkVersion` と `android-maxSdkVersion`（整数値）
* minSdkVersion の例： `<preference name="android-minSdkVersion" value="10" />`
* maxSdkVersion の例： `<preference name="android-maxSdkVersion" value="15" />`
* `AndroidManifest.xml` ファイルの `usesSdk` 属性に対応します。詳しくは、[Android のドキュメント](http://developer.android.com/guide/topics/manifest/uses-sdk-element.html)を参照してください。
* minSdkVersion のデフォルトは 7（Android 2.1）です。maxSdkVersion はデフォルトでは設定されません。

#### インストールの場所

* `android-installLocation`（値は `internalOnly`、`auto` または `preferExternal`）
* 例： `<preference name="android-installLocation" value="auto" />`
* アプリケーションをインストールできる場所。デフォルトは `internalOnly` です（Android SDK と同様）。
* `auto` または `preferExternal` を指定すると、アプリケーションを SD カード上にインストールできます。この結果、予期しない動作が発生する場合があります。
* 詳しくは、[Android のドキュメント](http://developer.android.com/guide/appendix/install-location.html)を参照してください。

#### スプラッシュスクリーンの表示時間

* `splash-screen-duration`（値をミリ秒単位で指定）
* デフォルトは 5000（5 秒）です。
* 例： `<preference name="splash-screen-duration" value="10000" />`
* 自動非表示にするには、device-ready メソッドで `navigator.splashscreen.hide();` を呼び出します。
* PhoneGap 2.1.0 以降でサポートされます。
  
#### URL ロードのタイムアウト

* `load-url-timeout`（値をミリ秒単位で指定）
* デフォルトは 20000（20 秒）です。
* 例： `<preference name="load-url-timeout" value="15000" />`

## その他の便利な要素

<a name="icons"></a>
### アイコンサポート

* `<icon>`：`config.xml` 内にはこの要素をゼロ個以上指定できます。アイコンを指定しない場合は、PhoneGap ロゴがアプリケーションのアイコンとして使用されます。 
* `src`：（必須）画像ファイルの場所を、`www` ディレクトリとの相対パスで指定します。
* `width`：（オプション）ただし、指定することをお勧めします。ピクセル単位の幅を表します。
* `height`：（オプション）ただし、指定することをお勧めします。ピクセル単位の高さを表します。

#### 使用法と追加情報：

config.xml で指定していない場合、各プラットフォームではコンパイル時にデフォルトの `icon.png` を使用することを試みます。プラットフォーム固有のアイコンを定義する場合は、以下のガイドに従ってください。

アイコンファイルは、以下の例に示すファイル形式にする必要があります。他のファイル形式では、複数のプラットフォームでの動作は保証されません。

#### デフォルト

デフォルトアイコンは、名前を `icon.png` として、アプリケーションフォルダーのルートに配置する必要があります。

    <icon src="icon.png" />

#### iOS

従来型のディスプレイ、Retina ディスプレイ、iPad ディスプレイ（および PhoneGap 2.5.0+ では Retina iPad ディスプレイ）をサポートします。以下は、それぞれのスクリーンタイプに応じたアイコンを定義しています。

    <icon src="icons/ios/icon.png" gap:platform="ios" width="57" height="57" />
    <icon src="icons/ios/icon-72.png" gap:platform="ios" width="72" height="72" />
    <icon src="icons/ios/icon_at_2x.png" gap:platform="ios" width="114" height="114" />

	<!-- retina iPad support: PhoneGap 2.5.0+ only -->
	<icon src="icons/ios/icon-72_at_2x.png" gap:platform="ios" width="144" height="144" />

#### Android

ldpi、mdpi、hdpi および xhdpi の各ディスプレイをサポートします。以下は、それぞれのスクリーンタイプに応じたアイコンを定義しています。

    <icon src="icons/android/ldpi.png" gap:platform="android" gap:density="ldpi" />
    <icon src="icons/android/mdpi.png" gap:platform="android" gap:density="mdpi" />
    <icon src="icons/android/hdpi.png" gap:platform="android" gap:density="hdpi" />
    <icon src="icons/android/xhdpi.png" gap:platform="android" gap:density="xhdpi" />

#### BlackBerry

BlackBerry アイコンのサイズは 16 KB __未満__ にする必要があります。BlackBerry では、オプションのマウスホバー状態も定義します。この状態によって、ユーザーがトラックパッドを使用してアイコン画像の上にカーソルをあてたときに別のアイコンを表示できます。デフォルトでは、ホバー状態としてホバーなしのアイコンが使用されます。

    <icon src="icons/bb/icon.png" gap:platform="blackberry" />
    <icon src="icons/bb/icon_hover.png" gap:platform="blackberry" gap:state="hover"/>

#### Windows Phone

Windows Phone に対して、通常のアイコンとタイトル画像の 2 つのアイコンをサポートしています。

    <icon src="icons/winphone/icon.png" gap:platform="winphone" />
    <icon src="icons/winphone/tileicon.png" gap:platform="winphone" gap:role="background" />

#### WebOS 

WebOs では、デフォルトアイコンと、通知に使用できるミニアイコンをサポートしています。

    <icon src="icons/webos/icon.png" gap:platform="webos" />
    <icon src="icons/webos/miniicon.png" gap:platform="webos" gap:role="mini" />

<a name="splashes"></a>
### スプラッシュスクリーン

`config.xml` 内にはこの要素をゼロ個以上指定できます。この要素には、前述の `<icon>` 要素と同様に、`src`、`gap:platform`、`width` および `height` 属性を指定できます。アイコンファイルと同様に、スプラッシュスクリーンも `png` ファイルとして保存する必要があります。

	<gap:splash src="splash/ios/Default-568h@2x~iphone.png" gap:platform="ios" width="320" height="480" />


#### 使用法と追加情報：

config.xml で指定していない場合、各プラットフォームではコンパイル時にデフォルトの `splash.png` を使用することを試みます。プラットフォーム固有のスプラッシュスクリーンを定義する場合は、以下のガイドに従ってください。

スプラッシュファイルは、以下の例に示すファイル形式にする必要があります。他のファイル形式では、複数のプラットフォームでの動作は保証されません。
##### 警告：
`gap:platform` 属性を指定しないと、参照される画像がすべてのプラットフォームにコピーされ、アプリケーションパッケージのサイズが増えます。

#### デフォルト

デフォルトスプラッシュは、名前を `splash.png` として、アプリケーションフォルダーのルートに配置する必要があります。

    <gap:splash src="splash.png" />

#### iOS

従来型のディスプレイ、Retina ディスプレイ、iPhone 5 ディスプレイおよび iPad ディスプレイをサポートします。以下は、それぞれのディスプレイに応じたスプラッシュスクリーンを定義します。標準の iPad には、縦と横の 2 種類のスプラッシュスクリーンがあります。Retina iPad には、さらに 2 種類のスプラッシュスクリーン、Retina 縦と Retina 横があります（PhoneGap 2.5.0+ のみ）。

    <gap:splash src="splash/ios/Default.png" gap:platform="ios" width="320" height="480" />
    <gap:splash src="splash/ios/Default_at_2x.png" gap:platform="ios" width="640" height="960" />
    <gap:splash src="splash/ios/Default_iphone5.png" gap:platform="ios" width="640" height="1136" />
    <gap:splash src="splash/ios/Default-Landscape.png" gap:platform="ios" width="1024" height="768" />
    <gap:splash src="splash/ios/Default-Portrait.png" gap:platform="ios" width="768" height="1024" />

	<!-- retina iPad support: PhoneGap 2.5.0+ only -->
    <gap:splash src="splash/ios/Default-Landscape_at_2x.png" gap:platform="ios" width="2048" height="1496" />
    <gap:splash src="splash/ios/Default-Portrait_at_2x.png" gap:platform="ios" width="1536" height="2008" />

#### Android

ldpi、mdpi、hdpi および xhdpi の各ディスプレイをサポートします。以下は、それぞれのスクリーンタイプに応じたスプラッシュスクリーンを定義しています。

    <gap:splash src="splash/android/ldpi.png" gap:platform="android" gap:density="ldpi" />
    <gap:splash src="splash/android/mdpi.png" gap:platform="android" gap:density="mdpi" />
    <gap:splash src="splash/android/hdpi.png" gap:platform="android" gap:density="hdpi" />
    <gap:splash src="splash/android/xhdpi.png" gap:platform="android" gap:density="xhdpi" />

#### BlackBerry 

BlackBerry では、1 つのスプラッシュ画像をサポートしており、以下のように定義できます。

    <gap:splash src="splash/bb/splash.png" gap:platform="blackberry" />

#### Windows Phone

Windows Phone では、1 つのスプラッシュ画像をサポートしており、以下のように定義できます。
サポート対象の他のプラットフォームとは異なり、Windows Phone のスプラッシュスクリーンは `jpg` 形式にする必要があります。

    <gap:splash src="splash/winphone/splash.jpg" gap:platform="winphone" />

<a name="url_schemes"></a>
### カスタム URL スキーム

iOS のみ。[カスタム URL スキーム](https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/AdvancedAppTricks/AdvancedAppTricks.html#//apple_ref/doc/uid/TP40007072-CH7-SW50)の登録を許可します。

    <gap:url-scheme name="com.acme.myscheme" role="None">
      <scheme>pgbr</scheme>
      <scheme>pgbw</scheme>
    </gap:url-scheme>

* 複数の `gap:url-scheme` エレメントを含めることができます。
* `name`、オプション。デフォルトはアプリケーションバンドル ID です。一意の値である必要があります。重複する値が見つかると、ビルドは失敗します。
* `role` は `Editor`、`Viewer`、`Shell` または `None` である必要があります。オプション。デフォルトは `None` です。
* 少なくとも 1 つの `scheme` を含める必要があります。

<a name="features"></a>
### PhoneGap API の機能 

* `<feature>`：feature 要素は、アプリケーションで使用する機能を指定するために使用できます。PhoneGap API の機能を指定した場合、それらの機能は、アプリケーション向けの適切な Android および Windows Phone の権限に展開されます。このインターフェイスで現在サポートされるのは、以下の機能名です。

  * `http://api.phonegap.com/1.0/battery`
* `android:BROADCAST_STICKY` 権限にマッピングされます。

  * `http://api.phonegap.com/1.0/camera`
* `android:CAMERA`、`winphone:ID_CAP_ISV_CAMERA` および `winphone:ID_HW_FRONTCAMERA` 権限にマッピングされます。

  * `http://api.phonegap.com/1.0/contacts`
* `android:READ_CONTACTS`、`android:WRITE_CONTACTS`、`android:GET_ACCOUNTS` 
および `winphone:ID_CAP_CONTACTS` 権限にマッピングされます。

  * `http://api.phonegap.com/1.0/file`
* `WRITE_EXTERNAL_STORAGE` 権限にマッピングされます。

  * `http://api.phonegap.com/1.0/geolocation`
* `android:ACCESS_COARSE_LOCATION`、`android:ACCESS_FINE_LOCATION`、 
`android:ACCESS_LOCATION_EXTRA_COMMANDS` および `winphone:ID_CAP_LOCATION` 権限にマッピングされます。

  * `http://api.phonegap.com/1.0/media`
* `android:RECORD_AUDIO`、`android:RECORD_VIDEO`、`android:MODIFY_AUDIO_SETTINGS` 
および `winphone:ID_CAP_MICROPHONE` 権限にマッピングされます。

  * `http://api.phonegap.com/1.0/network`
* `android:ACCESS_NETWORK_STATE` および `winphone:ID_CAP_NETWORKING` 権限にマッピングされます。

  * `http://api.phonegap.com/1.0/notification`
* `VIBRATE` 権限にマッピングされます。

  * `http://api.phonegap.com/1.0/device`
* `winphone:ID_CAP_IDENTITY_DEVICE` 権限にマッピングされます。

#### 使用法

    <!-- If you do not want any permissions to be added to your app, add the
        following tag to your config.xml; you will still have the INTERNET
        permission on your app, which PhoneGap requires. -->
    <preference name="permissions" value="none"/>

    <!-- to enable individual permissions use the following examples -->
    <feature name="http://api.phonegap.com/1.0/battery"/>
    <feature name="http://api.phonegap.com/1.0/camera"/>
    <feature name="http://api.phonegap.com/1.0/contacts"/>
    <feature name="http://api.phonegap.com/1.0/file"/>
    <feature name="http://api.phonegap.com/1.0/geolocation"/>
    <feature name="http://api.phonegap.com/1.0/media"/>
    <feature name="http://api.phonegap.com/1.0/network"/>
    <feature name="http://api.phonegap.com/1.0/notification"/>

<a name="plugins"></a>
### プラグイン

* `<gap:plugin>`：生成されるアプリケーションにインクルードする PhoneGap Build 向けの PhoneGap プラグインを指定します。

現時点では、プラグインをインクルードするには、以下の要件を満たす必要があります。

* プラグインが PhoneGap Build によってサポートされていること
* JavaScript のスクリプトタグが `index.html` ファイル内に指定されていること

利用可能なプラグインのリストなどについて詳しくは、[プラグインのドキュメント](/docs/plugins)を参照してください。

<a name="access"></a>
### アクセス要素

* `<access>`：access 要素を使用すると、アプリケーションは他のドメインにあるリソースにアクセスすることができます。特に、この要素によって、webview 全体を引き継ぐことのできるページを外部ドメインからロードできます。

access タグが空の場合（`<access />`）、外部リソースへのアクセスが拒否されます。ワイルドカードを指定した場合（`<access origin="*" />`）、すべての外部リソースへのアクセスが許可されます。その他、許可されるドメインを個別に指定できます。

    <access origin="https://build.phonegap.com" />

また、以下のように `subdomains` 属性を使用してサブドメインを指定することもできます。

    <access origin="http://phonegap.com" subdomains="true" />

access 要素の動作は、デプロイ先のプラットフォームに大きく依存します。詳しくは、[このブログ記事](/blog/access-tags)を参照してください。また、その動作は PhoneGap のリリースによって異なる可能性もあります。PhoneGap Build では今後、PhoneGap Build ユーザーにとって妥当なデフォルト値や設定可能性の維持管理に努めていきます。
