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

# Hydration ビルド

Adobe® PhoneGap Build には、ユーザー向けに Hydration 機能が用意されています。Hydration は、開発者およびテスターに以下の 2 つの主要な メリットを提供するツールです。

1. コンパイル時間の大幅な向上
2. デバイスにインストールされたアプリケーションに更新を直接プッシュ

PhoneGap では、モバイルアプリケーションのコンテナとして動作するネイティブバイナリをコンパイルすることで、このようなメリットを実現しています。開発者が新しいビルドをアップロードすると、アプリケーションの再起動時に、アプリケーションのエンドユーザー（テスターなど）に通知されます。エンドユーザーが新しいコードベースの実行を決定すると、Hydration が有効になっているアプリケーションでは自動的に最新のコードベースを取得して実行します。

質問がある場合や、弊社のチームにフィードバックを提供する場合、弊社では主なコミュニケーションの手段として[コミュニティサポートチャンネル](http://community.phonegap.com)を利用しています。遠慮なくご連絡ください。

## 目次

1. [Hydration を使用するためのプロジェクトの設定](#create_hydration_build)
    1. [新しいアプリケーションでの Hydration の有効化](#new_build_project)
    2. [既存のアプリケーションでの Hydration の有効化](#existing_build_project)
2. [Hydration を使用したアプリケーションのビルド](#build_app)
    1. [アプリケーションのビルド](#build_application)
    2. [Hydration が有効になったアプリケーションのインストール](#installing_application)
    3. [アプリケーションの更新](#update_application)
    4. [Hydration の無効化](#disable_hydration)
    
<a id="create_hydration_build"></a>
##Hydration を使用するためのプロジェクトの設定

Hydration の有効と無効の切り替えは、新しいプロジェクトでも既存のプロジェクトでも実行できますが、プロジェクトで以下の PhoneGap バージョンを使用する必要があります。

    サポートされるバージョン：2.0.0 以上
    サポートされるプラットフォーム：iOS、Android 

<a id="new_build_project"></a>
###新しいアプリケーションでの Hydration の有効化

ログイン後、[https://build.phonegap.com/](https://build.phonegap.com/) に移動し、「+ 新規アプリケーション」ボタンをクリックします。

「設定」カテゴリで、「アプリケーションに Hydration を設定」というオプションを選択し、他のオプションを設定して、「作成」をクリックします。

無効化するまでは、ビルドを実行するたびに、このアプリケーションについては Hydration が有効になったバージョンが生成されます。

<a id="existing_build_project"></a>
###既存のアプリケーションでの Hydration の有効化

ログイン後、
[https://build.phonegap.com/](https://build.phonegap.com/) に移動します。
次に、タイトルまたはアイコンをクリックして、アプリケーションを選択します。アプリケーションの詳細ページで、設定パネルを開きます。次に、「基本」ヘッダーの下の「Hydration を有効にする」チェックボックスをオンにします。

無効化するまでは、ビルドを実行するたびに、このアプリケーションについては Hydration が有効になったバージョンが生成されます。

##Hydration を使用したアプリケーションのビルド

<a id="build_application"></a>
###アプリケーションのビルド

Hydration を使用したアプリケーションのビルドは、通常のビルドを使用した他のアプリケーションのビルドと同様に簡単です。Hydration を有効にした後は、「再ビルド」ボタンをクリックするだけで、Hydration が有効になったビルドが生成されます。

プロジェクトの設定に対する変更が検出された場合は、Build によって新しいバイナリが生成されます。

プロジェクトの設定には、以下のような項目があります。

    名前、バージョン、バージョンコード、アイコン、スプラッシュスクリーン、環境設定、
    機能およびアクセスタグ

ネイティブバイナリが生成されるたびに、エンドユーザーは自分が使用しているバイナリを更新する必要がある点に注意してください。

<a id="installing_application"></a>
###Hydration が有効になったアプリケーションのインストール

ビルドによって生成されたバイナリは、Hydration が有効になっていない場合とまったく同様なバイナリになります。Hydration が有効になっていないバージョンと同様にアプリケーションをインストールしてください。このインストールは、QR コード経由か、プラットフォーム固有のツール（iTunes、adb など）で実行できます。

Hydration ビルドに対しても、ネイティブバイナリに対する制約が適用される点に注意してください。例えば、アドホック配布（iOS）ビルドをプロビジョニングできるのは 100 個のデバイスまでです。

<a href="update_application"></a>
###アプリケーションの更新

開発者が新しいビルドをコンパイルすると、エンドユーザーは Hydration が有効になったアプリケーションを更新できます。この更新プロセスは、アプリケーションを再起動するたびに実行されます。

ユーザーがアプリケーションを再起動すると、アプリケーションの更新を求めるダイアログが表示されます。

ユーザーがアプリケーションを更新する場合、新しいビルドがダウンロードされて実行されます。

ユーザーが更新をスキップする場合は、現在のビルドがそのまま残り、次回の再起動時に更新を求めるダイアログが表示されます。

Hydration を有効にできないビルドを開発者が生成した場合、ユーザーはコンパイルされた新しいバージョンのバイナリを取得する必要があります。ユーザーは、バイナリをダウンロードするか、その他のいずれかの方法を使用することで、バイナリを取得できます。

<a id="disable_hydration"></a>
###Hydration の無効化 

ログイン後、[https://build.phonegap.com/](https://build.phonegap.com/) に移動し、タイトルまたはアイコンをクリックしてアプリケーションを選択します。アプリケーションの詳細ページで、設定パネルを開きます。次に、「基本」ヘッダーの下の「Hydration を有効にする」チェックボックスをオフにして、最後に「保存」をクリックします。

これで、Hydration を無効にできました。

これ以降は、ユーザーはアプリケーション用の更新プログラムを手動でダウンロードする必要があることに注意してください。 
