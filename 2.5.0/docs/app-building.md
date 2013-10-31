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

# 最初のアプリケーションのビルド

PhoneGap Build にようこそ。PhoneGap Build では、シンプルな Web インターフェイスを使用して、HTML、CSS および JavaScript に基づいたクラスプラットフォームのモバイルアプリケーションを作成できます。PhoneGap Build ではパッケージ化とコンパイルがすべて実行され、ユーザーは数分でモバイルアプリケーションを入手できます。

最初の手順はアカウントを登録してログインすることです。ここでは、ユーザーがこの最初の手順を完了しており、現在 __+ 新規アプリケーション__ フォームを開いていることを前提としています。

![新規アプリケーションフォーム](images/getting-started/new-app-form.png)

PhoneGap Build では 2 つのオプションを使用できます。1 つは、既存の PhoneGap プロジェクトを 1 つの `index.html` または zip 形式のパッケージアーカイブのいずれかでアップロードするオプションです。もう 1 つは、サイトをソース管理リポジトリにリンクするオプションです（このリポジトリは公開リポジトリです。プライベートリポジトリは間もなくサポートされる予定です）。

ソース管理リポジトリの場合でも zip アーカイブの場合でも、プロジェクトには以下を含めることができます。

* `index.html`（アプリケーションのメインページ）
* アプリケーションで使用するその他のアセット（JavaScript または CSS ファイル、画像、オーディオ、ビデオなど）
* `config.xml` ファイル（[W3C ウィジェット仕様](http://www.w3.org/TR/widgets/)に準拠し、アプリケーションに関するデータが含まれるファイル）
* アプリケーションアイコン画像。`png` ファイルが最も広くサポートされており、現時点では最適なファイル形式です。

必須のファイルは `index.html` のみです。アプリケーションプロパティはすべて、Web インターフェイスを使用して編集できます。

アプリケーションをまだ準備していない場合、PhoneGap Build の使用を開始するには、[Getting Started](https://github.com/phonegap/phonegap-start) GitHub リポジトリを使用する方法が最も簡単です。

![PhoneGap の開始](images/getting-started/phonegap-start.png)

GitHub アカウントがない場合は、アプリケーションの `http` url（`http://github.com/phonegap/phonegap-start.git`）をコピーして、アプリケーションフィールドにペーストします。 

この操作によってアプリケーションがすぐにビルドされます。ただし、GitHub アカウントがある場合は、アプリケーションをフォークすることで、アプリケーションを簡単に編集することができます。「 __Fork__ 」をクリックして、ソースリポジトリの自分用のコピーを作成します。

![alunny での作業開始](images/getting-started/alunny-start.png)

この時点でアプリケーションのカスタマイズが必要になった場合は、リポジトリを複製します。

    $ git clone https://github.com/alunny/phonegap-start.git

次に、リポジトリのルートにある `config.xml` を開きます。以下の属性を編集します。

* `<name>` を `<name>alunny's Amazing app</name>` に変更します。</span>
* `<description>` を `<description>An Amazing app by alunny</description>` に変更します。
* ルート要素の `version` 属性を `99.999` に設定します。
* ルート要素の `id` 属性を `com.alunny.amazing` に設定します。
* 他の設定は現時点では無視できます。属性の大部分は、今後の PhoneGap Build 機能のためのプレースホルダーです。

次に、`icon.png` を新しいアイコンに変更します。

![新しいアイコン](images/getting-started/new-icon.png)

これらの変更をレポジトリにプッシュします。

    $ git push origin master

![alunny での作業（変更後）](images/getting-started/alunny-start-changes.png)

これで、アプリケーションの設定が完了しました。次に、この Amazing アプリケーションを PhoneGap Build 上に作成します。まず、フォームに情報を入力します。この公開 git の url は `http://github.com/alunny/phonegap-start.git` です。. レポジトリのフィールドにペーストすると、アプリケーションのアップロードがすぐに開始されます。

![新規アプリケーションの取得](images/getting-started/new-app-populated.png)

アプリケーションの取得が完了したら、必要に応じてデバッグや Hydration を有効にするかを選択できます。すべての設定が完了したら、「ビルド準備完了」をクリックします。

![新規アプリケーションの準備完了](images/getting-started/new-app-ready.png)

これで、処理が実行されます。PhoneGap Build の各サーバーが回転するように表示され、6 つのプラットフォームのアプリケーションが準備される様子を確認できます。

![スピナー](images/getting-started/spinners.png)

これで、ダウンロードできるようになりました。数秒でこの状態になります。

![ダウンロード準備完了](images/getting-started/downloads-ready.png)

アプリケーションのタイトルまたはアイコンをクリックすると、アプリケーションの詳細ページが表示されます。「設定」タブでは、`config.xml` に設定した詳細情報とアイコンが表示されます。変更する場合は、Git リポジトリで変更を行います。

GitHub にリンクされているので、Build に存在する最新のコミットへの直接のリンクが表示されます。また、PhoneGap アプリケーションを最新のコミットに更新するためのリンクもあります。このリンクは、選択したどのコードホストに対してでも動作します。現時点では、追加したリポジトリ URL で公開読み取りアクセスを許可する必要があります。

次に、アプリケーション自体について説明します。アプリケーションを直接インストールすることは、使用するプラットフォームによってはそれほど難しくありません。

* __Android__：お使いの Android デバイスで不明なソースから `apk` ファイルをインストールできるように設定しておきます。
* __設定__ ／ __アプリケーション__ を開き、「 __提供元不明のアプリ__ 」をオンにします。
* __webOS__：Web から直接 webOS パッケージ（`ipk` ファイル）をインストールすることはできません。インストールするには、Palm の `palm-install` ユーティリティを使用します。
* __Symbian__：デバイスに `wgz` ファイルをダウンロードして開けば、インストールが完了します。
* __BlackBerry__：デバイス上で `OTA インストール`リンクをクリックして、説明に従います。現時点では、BlackBerry OS 5.0 以降のみをサポートしています。
* __Windows Phone__：Web から直接 Windows Phone パッケージをインストールすることはできません。Microsoft のツールを使用する必要があります。

直接のインストールをサポートしているプラットフォーム（現時点では webOS 以外のすべて）では、サイトに移動して適切なリンクをタッチするか、お好きな QR コードリーダーを使用し、表示される QR コードを携帯電話のカメラで読み取る方法を利用できます。

優れたアプリケーションを作成しましょう。
