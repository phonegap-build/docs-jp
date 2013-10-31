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

# iOS のキー設定の署名

  Adobe® PhoneGap™ Build では、iOS デバイス向けのビルドがサポートされるようになりました。iOS ビルドの実行プロセスは、他のプラットフォームとは少し異なります。Apple 開発者アカウントおよびテストを実行するデバイスに関連付けられた開発者証明書とプロビジョニングプロファイルを使用して、すべての iOS ビルドに署名する必要があります。このドキュメントでは、この設定方法について説明します。

> 注意：PhoneGap Build では Apple の標準開発プロセスを使用してアプリケーションをビルドするので、PhoneGap Build で iOS アプリケーションをビルドするには、Apple の開発者プログラムにサインアップする必要があります。また、Mac を使用して証明書とプロビジョニングプロファイルを設定する必要もあります。

  新しいアプリケーションを PhoneGap Build にアップロードする際に、デフォルトの証明書とプロファイルのペアがアカウントに関連付けられていない場合は、iOS ビルドを実行できないことを示す以下の警告が表示されます。

  ![iOS キーが必要です](images/ios-builds/ios-key-required.png)

  キーは、実際には **証明書** と **プロビジョニングプロファイル** の 2 つのファイルで構成されます。Apple には、環境をローカルで設定するための[豊富なドキュメント](http://developer.apple.com/jp)が用意されています。環境をローカルで設定する最適な方法は、iOS アプリケーションを iOS デバイス向けにローカルでビルドできるかどうかを確認し、証明書とプロビジョニングプロファイルがコード署名用に正しく設定されていることを確認することです。

  証明書とプロビジョニングプロファイルが設定されていれば、これらのファイルを書き出して、PhoneGap Build にアップロードできます。プロビジョニングプロファイルについては、以下のような `mobileprovision` 拡張子のファイルが必要になります。

  ![Finder でのプロビジョニングプロファイル](images/ios-builds/team-provisioning-profile.png)

  このプロビジョニングプロファイルが、テストを実行するデバイスと正しく関連付けられていることを確認してください。

  プロファイルの作成時に、プロファイルにリンクされた App ID を指定します。この App ID は、PhoneGap Build を使用する際に重要です。`config.xml` 内（`widget` 要素の `id` 属性）またはアプリケーションを編集ページでアプリケーションに対して指定するパッケージ名は、プロビジョニングプロファイルの ID と一致する必要があります。一致しない場合、アプリケーションは正しくビルドされません。

  iOS Developer Center で生成したプロビジョニングプロファイルには、Apple によって「Bundle Seed ID（App ID Prefix とも呼ばれます）」が追加されます。PhoneGap Build で正しくビルドするには、`config.xml` にこの App ID Prefix を追加しないでください。逆ドメイン形式の Bundle Identifier（`com.domainname.appname`）のみが必要です。また、これは、他のプラットフォーム向けのビルドと最も互換性があります。

  証明書を準備するには、Mac で **キーチェーンアクセス** ユーティリティを起動し、iOS 開発で使用する証明書を指定します。その証明書を右クリックし、「書き出す...」を選択します。

  ![キーチェーンアクセスからの書き出し](images/ios-builds/keychain-export.png)

  覚えやすい場所に証明書を保存し、パスワードを入力します。このパスワードは PhoneGap Build に指定する必要があるので、忘れないでください。パスワードがわからないと、証明書を使用できません。

  ![証明書のパスワードの入力](images/ios-builds/keychain-password.png)

  次に、Web サイトに戻ります。アプリケーションの詳細ページで、対象となるアプリケーションの「署名キー」ドロップダウンから「新規キー...」オプションを選択し、署名を利用できるプラットフォームのリストで、iOS の「キーを追加」をクリックします。フォームに情報を入力します。`p12` 証明書ファイルと `mobileprovision` ファイルを追加し、証明書に関連付けられたパスワードを入力します。

  ![PhoneGap Build への証明書の追加](images/ios-builds/ios-key-form.png)

  キーが追加されると、iOS 向けのアプリケーションの再ビルドが試行されます。再ビルドに成功した場合は、ビルドされた `ipa` ファイルへのリンクが表示されます。

  その後、この `ipa` ファイルをダウンロードし、iTunes を使用して、プロビジョニングされた iOS デバイスにこのファイルを直接インストールできます。

  それでは、ビルドをお楽しみください。
