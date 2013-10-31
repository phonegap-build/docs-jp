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

# 一般的なエラー

Adobe® PhoneGap™ Build では、ユーザーが送信したすべてのパッケージを取得し、そのパッケージからクロスプラットフォームのモバイルアプリケーションをビルドできるように最善を尽くしています。しかし、このビルドが成功しない場合もあります。各プラットフォーム独自の特性や、PhoneGap Build が持つ一部の特性がその原因です。ここでは、受け取る可能性のあるエラーと、それらのエラーの修正方法について説明します。

## すべてのプラットフォームでアプリケーションが 10 分以上保留中です

これは通常、PhoneGap Build 側に問題が発生していることを示しています。[お問い合わせ](http://community.phonegap.com)ください。

<a name="no_index"></a>
## アプリケーションに `index.html` がありません

PhoneGap Build および一般的な PhoneGap/Cordova アプリケーションでは、アプリケーション内に `index.html` というファイルを含める必要があります。このファイルは、アプリケーションの初期処理が行われる開始点として使用されます。

アプリケーションのルートに `index.html` があることを確認してください。このファイルがある場合は、ビルドが正常に実行されます。

<a name="phonegap_unsupported"></a>
## PhoneGap バージョンはサポートされていません

このエラーが発生する理由は以下の 2 つです。

1. PhoneGap Build で現在サポートされていない `phonegap-version` を `config.xml` ファイル内で指定している場合。[config.xml のドキュメント](/docs/config-xml)で、現在サポートされているリリースを確認してください。
2. ビルド対象のいずれかのプラットフォームで、お使いの PhoneGap バージョンがサポートされていない場合（例えば、1.5.0 より前の PhoneGap リリースでは、Windows Phone アプリケーションはビルドされません）。この問題を修正するには、アプリケーションの編集ページまたは `config.xml` ファイル内で、PhoneGap バージョンを更新してください。

<a name="invalid_filename"></a>
## ファイル名またはディレクトリ名が無効です

モバイルファイルシステムは特定のファイル名を受け付けません。特に、中国語の文字やアラビア文字などの非 ASCII 文字を含むファイル名は許可されません。ファイル名に非 ASCII 文字が含まれる場合は名前を変更してください。そうすることで、アプリケーションが正常にビルドされます。

<a name="malformed_config"></a>
## 不正な形式の config.xml です

指定された `config.xml` ファイルを解析できませんでした。整形式の XML ではない可能性があります。

`config.xml` が有効な XML であるかを確認し（[W3C バリデーター](http://validator.w3.org)を使用できます）、必要な変更を行って問題を修正してください。

## BlackBerry のビルドに失敗しました

PhoneGap で使用している BlackBerry WebWorks フレームワークには独自の特性が多くあります（詳しくは、[この gist を参照](https://gist.github.com/778233)）。BlackBerry でビルドが失敗する場合、その他のよくある原因は以下のとおりです。

<a name="signing_timeout"></a>
#### 署名がタイムアウトしました

デバイスで実行するには、すべての BlackBerry ビルドが RIM の署名サーバーによって署名されている必要があります。PhoneGap Build はすべての BlackBerry ビルドに対してこの署名を試行しますが、一時的に停止する問題があり、サーバーが応答しない場合はビルドがタイムアウトします。この場合は「再ビルド」をクリックして、BlackBerry ビルドを再度実行してください。

<a name="invalid_characters"></a>
#### ファイル名やディレクトリ内の文字が無効です

BlackBerry Widget Packager（アプリケーションのアセットを取得してパッケージ化し、BlackBerry 互換のバイナリを作成するための RIM のツール）には、ファイル名とディレクトリに使用できる文字に関する非常に厳しいルールがあります。ファイル名およびディレクトリのすべてに英数字のみが使用されていることを確認してください。RIM がこの問題を修正しない限り、PhoneGap Build ではこの問題に対応できません。

<a name="invalid_directory_names"></a>
#### ディレクトリ名が無効です

BlackBerry Widget Packager には、もう一つの特性があります。それは、ディレクトリ名には `bin` および `src` という 2 つの名前が予約されていることです。アプリケーションパッケージにこれらのいずれかの名前のディレクトリが含まれている場合は、Widget Packager は失敗します。そのようなディレクトリの名前は変更してください。

<a name="icons_too_large"></a>
#### アイコンが大きすぎます

[BlackBerry Widget Packager のソースコード](https://github.com/blackberry/WebWorks/blob/master/packager/src/net/rim/tumbler/rapc/Rapc.java#L177-178)によると、BlackBerry WebWorks アプリケーションのアイコン画像のデフォルトの最大サイズは 16,384 バイトです。このサイズよりも大きいアイコンがある場合は、Packager でエラーが発生し、その結果ビルド内でエラーが発生します。

<a name="invalid_pw"></a>
#### CSK パスワードが無効です：署名が検証されませんでした

BlackBerry WebWorks Signing Tool では、ユーザーがアップロードしたキーと指定したパスワードを使用して署名を検証できませんでした。これは通常、指定したパスワードに誤りがある場合に発生します。正しいパスワードを指定したかを確認し、必要な場合はキーを再度アップロードしてください。

また、BlackBerry WebWorks Signing Tool では、8 文字以上のパスワードが必要です。パスワードが 8 文字未満の場合にもこのエラーが発生します。

<a name="too_many_files"></a>
#### www ディレクトリ内のファイルが多すぎます

BlackBerry WebWorks Packager では、アプリケーションパッケージ内に含めることができるファイルの数が制限されており、このファイル数を超過するとアプリケーションがビルドされません。経験的に、この制限は 200 ～ 250 ファイル程度であることがわかっています。

このエラーを受け取った場合は、アプリケーションをビルドするために、`www` ディレクトリからファイルをいくつか削除する必要があります。

<a name="invalid_metadata_characters"></a>
#### メタデータ内の文字が無効です

BlackBerry WebWorks Packager にはもう一つの制限があります。それは、アプリケーションのメタデータ（名前、説明など）ではラテン文字のみが使用できるということです。アプリケーションのメタデータ内でラテン文字以外の文字が使用されていると、BBWP コンパイラーでアプリケーションをビルドできません。

このエラーを受け取った場合は、アプリケーションのメタデータを編集して（PhoneGap Build を使用するか `config.xml` ファイルを編集）、違反している文字を削除する必要があります。

<a name="data_section_too_large"></a>
#### データセクションが大きすぎます

「データセクション」（`www` データの任意の一部分）が大きすぎて Packager で処理できない場合にも、BlackBerry ビルドは失敗します。これは通常、アプリケーションパッケージ内に高解像度の画像などの大きなアセット（通常 200 KB 以上）が含まれている場合に発生します。

BlackBerry 向けにアプリケーションをビルドするには、パッケージからそのような大きなアセットを削除してください。

<a name="long_description"></a>
#### 説明が長すぎます

BlackBerry WebWorks Packager は、アプリケーションの説明を含むアプリケーション設定（`config.xml` ファイル）をアプリケーションパッケージの一部として処理します。
この説明が長すぎる場合は、BBWP 向けに生成される `config.xml` が原因となって、Packager から例外がスローされます。

BlackBerry 向けにアプリケーションを正常にビルドする場合は、この説明を短くしてください。

## iOS のビルドに失敗しました

<a name="libpng"></a>
### アイコンまたはスプラッシュスクリーンが png ファイルではありません

iOS 向けにビルドする場合、PhoneGap フレームワークでは、システムで表示するために指定された画像ファイル（アイコンやスプラッシュスクリーンなど）が Portable Network Graphics（`png`）形式であることを前提としています。このエラーが発生した場合は、異なる形式の画像ファイルまたは破損した png ファイルが指定されています。これらのファイルが有効な png であることを確認し、再ビルドしてください。

<a name="no_cert"></a>
### 証明書が見つかりません

関連付けられた署名証明書とキーチェーンのペアを含まないアプリケーションが送信されました。[PhoneGap Build アカウントにキーを追加し](/people/edit)、アプリケーションの編集ページでそのキーをアプリケーションに関連付けてください。

<a name="cert_import"></a>
### 証明書を読み込むことができません

ユーザーが指定した証明書と指定したパスワードをサーバーで使用できませんでした。キーチェーンに証明書を読み込めなかったので、その証明書を使用してアプリケーションに署名できませんでした。

証明書を再度アップロードし、証明書によって正しい資格情報が指定されていることを確認してください。

<a name="cert_profile_mismatch"></a>
### 証明書がプロファイルに一致しません

ユーザーがアップロードしたプロファイルおよび証明書を使用して、サーバーでアプリケーションに署名できませんでした。プロファイルに示されている ID が証明書の ID と一致しなかったことがその理由です。この原因として、開発者プロファイルを配布証明書と共にアップロードしたか、配布プロファイルを開発者証明書と共にアップロードした可能性があります。

証明書に一致する新しいプロビジョニングプロファイルを生成し、そのプロファイルを PhoneGap Build にアップロードしてください。

<a name="profile_expired"></a>
### プロビジョニングプロファイルの有効期限が切れています

ユーザーがアップロードしたプロファイルおよび証明書を使用して、サーバーでアプリケーションに署名できませんでした。プロビジョニングプロファイル自体の有効期限が切れていたことがその理由です。

アプリケーションを正常にビルドするためには、Apple Developer Portal で新しいプロビジョニングプロファイルを生成し、そのプロファイルを PhoneGap Build にアップロードする必要があります。

<a name="unreadable_profile"></a>
### プロビジョニングプロファイルを読み取ることができません

ユーザーがアップロードしたプロファイルおよび証明書を使用して、サーバーでアプリケーションに署名できませんでした。プロビジョニングプロファイルを読み取りまたは解析できなかったことがその理由です。

アップロードした `mobileprovision` ファイルが、Apple Developer Portal で生成した有効なプロビジョニングプロファイルであることを確認してください。プロファイルに誤りがあった場合は、有効なプロファイルを用意して、そのプロファイルを PhoneGap Build にアップロードしてから、アプリケーションを再ビルドしてください。

## Android のビルドに失敗しました

<a name="keystore"></a>
### キーストアの問題

以下のすべてのエラーメッセージは、Android 署名キーに問題があることを表しています。

* `キーストアエイリアスが認識されませんでした`
* `キーストア形式が無効です`
* `キーストアのパスワードが正しくありません`
* `エイリアスがプライベートキーに関連付けられていません`

以上のいずれかのエラーを受け取った場合、Android `jarsigner` では、ユーザーが指定したキーとキーストアを使用してアプリケーションに署名できていません。

エイリアスが認識されない場合は、ユーザーがアップロードした `keystore` ファイルに、指定された `alias` フィールドがありません。キーストア形式が無効の場合は、正しいファイルをアップロードしなかった可能性があります。パスワードが正しくない場合は、パスワードを誤って入力した可能性があります。

それぞれのケースで、キーストアファイルが正しく、キーストアのパスワードとエイリアスの詳細が正しいことを確認してください。署名付きビルドを正常に実行するために、場合によっては Android キーを再度アップロードする必要があります。

<a name="identical_filenames"></a>
## ファイル名が同一です

Android ファイルシステムでは、多くのデスクトップオペレーティングシステムとは異なり、大文字と小文字が区別されません。例えば、`index.html` というファイルと `index.HTML` というファイルを、同じ Android アプリケーションパッケージに含めることはできません。

どちらかのファイルを削除すれば、アプリケーションは正常にビルドされます。

## webOS のビルドに失敗しました

webOS パッケージャー（`palm-package` という実行ファイル）は、アプリケーションのバージョン番号とパッケージ名について特に厳密です。バージョン番号は `1.1.1` という形式（メジャーバージョン、マイナーバージョン、パッチバージョンの順）に従う必要があります。`1.0` などのバージョンを使用すると `palm-package` で失敗します。

同様に、パッケージ名は `com.yourcompany.app1` という形式（逆ドメイン形式、すべて小文字、すべて英数字）に従う必要があります。webOS でビルドに失敗した場合は、これらのいずれかが根本原因の可能性があります。

<a name="plugin-error"></a>
## プラグインエラー

このエラーは、アプリケーションパッケージにプラグインの javascript ファイル（barcodescanner.js、GAPlugin.js、cdv-plugin-fb-connect.js または childbrowser のアセットディレクトリなどのその他のプラグイン）を含めたことが原因である可能性があります。

以前は、プラグインをインストールするために、アプリケーション内のファイルを単に上書きする pluginstall を使用していましたが、最近 plugman に移行しました。plugman ではファイルが上書きされず、代わりに失敗します。ファイルを必ず削除するようにしてください。

その他のエラーを受け取った場合は、[お知らせください](http://community.phonegap.com)。その内容に基づいて、このドキュメントが更新されます。
