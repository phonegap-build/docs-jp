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

# アプリケーションについて

PhoneGap Build では、アプリケーションをある特定の方法でパッケージ化する必要が
ありますが、最初はこの方法が直感的なものだと感じられないでしょう。

PhoneGap Build では、[W3C によるウィジェットのパッケージ化の仕様](http://www.w3.org/TR/widgets/)に準拠したオープンのパッケージ化モデルを使用しています。

以下に、PhoneGap Build 用にアプリケーションをパッケージ化するためのガイドを示します。

##目次

1. [アップロードするもの](#what_do_i_upload)
2. [アプリケーションの設定方法](#configure_application)
3. [次の手順](#whats_next)
4. [ヘルプの場所](#whats_next)


<a id="#what_do_i_upload"></a>
###アップロードするもの

####アセットの準備

PhoneGap Build ではアプリケーションのアセットのみを必要とします。これは基本的には、html、css、画像、js ファイルなどを含む www ディレクトリを指します。

ネイティブファイル（.h、.m、.java など）をアップロードすると、ほとんどの場合、PhoneGap Build ではアプリケーションのコンパイルに失敗します。

####不要なファイルの削除

必要なアセットを追加したら、Build によってコンパイル時に自動的に挿入される `phonegap.js`（cordova.js）を削除します。

####`phonegap.js` を削除する理由

PhoneGap では、プラットフォームごとに異なる JavaScript ファイルが必要であり、互換性のない `phonegap.js` を使用すると、アプリケーションの実行時にエラーが発生します。

####PhoneGap API へのアクセスの確認

`phonegap.js` を削除した後、アプリケーションが PhoneGap API にアクセスできることを確認する必要があります。

そのためには、`index.html` 内に以下の参照が指定されていることを確認してください。

    <script src="phonegap.js"></script>

<a id="#configure_application"></a>
###アプリケーションの設定方法

PhoneGap Build では、`config.xml` という設定 XML ファイルをサポートしています。

この設定ファイルを使用して、アプリケーションのタイトル、アイコン、スプラッシュスクリーン、その他のプロパティを変更できます。

config.xml について詳しくは、[関連ドキュメント](/docs/config-xml)を参照してください。

<a id="whats_next"></a>
###次の手順

以上で、PhoneGap Build でアプリケーションをビルドする準備ができました。

ただし、以下のドキュメントも参照することをお勧めします。これらのドキュメントは、PhoneGap Build の理解を深めるのに役立ちます。

* [PhoneGap Build でのコンパイルの開始](/docs/start)

* [PhoneGap Build を使用したアプリケーションのデバッグ](/docs/phonegap-debug)

<a id="help"></a>
###ヘルプの場所

コンパイル中にエラーが発生した場合に備え、[よくあるエラーとその解決策](/docs/build-failed)のリストを提供しています。

質問が解決されない場合や、弊社のチームにフィードバックを提供する場合、弊社では主なコミュニケーションの手段として[コミュニティサポートチャンネル](http://community.phonegap.com)を利用しています。
遠慮なくご連絡ください。
