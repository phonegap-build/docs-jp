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

# Android のキー設定の署名

Adobe® PhoneGap Build™ では Android ビルドに署名できます。これにより、[Android Market](http://market.android.com/) へアプリケーションを適切に送信することができます。

リリースビルドを準備するには、まず署名キーストアファイルを生成する必要があります。詳しくは、[Android のドキュメント](http://developer.android.com/guide/publishing/app-signing.html)に記載されています。
キーストアに設定する **エイリアス** 、 **キーストアのパスワード** および **キーのパスワード** を記録してください。

次の手順では、[アカウントの編集](/people/edit)を行ない、キーを追加します。
下にスクロールすると、署名キーおよび証明書のための新しいパネルが表示されます。

![署名キーパネル](images/android-signing/signing-keys-panel.png)

「キーを追加」をクリックし、詳細情報をすべて入力します。「 **エイリアス** 」、「 **キーのパスワード** 」、「 **キーストアのパスワード** 」の各フィールドには、キーの作成時に入力した値と同じものを入力してください。「 **タイトル** 」フィールドには、キーを識別するための任意の情報を入力できます。

![Android キーモーダルフォーム](images/android-signing/android-key-modal.png)

「保存」をクリックすると、下部にあるキーのリストが更新され、新しいキーが追加されます。新しいキーをデフォルトに設定します。

PhoneGap Build によってアプリケーションのリリースビルドが作成される際に、ユーザーのキーストアを使用してバイナリへの署名が行われ、さらに `zipalign` ツールを使用してそのバイナリが最適化されます。

これで準備ができました。今後のすべての Android ビルドで、選択したデフォルトのキーが使用され、リリースできるようになります。
