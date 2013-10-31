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

# デバッグ

Adobe® PhoneGap™ Build のユーザー用に、デバッグビルド機能が用意されています。このサービスを使用すると、アプリケーションの実行中に、アプリケーションのデバッグやアプリケーションの対話的な修正を行うことができます。新しく追加されたこの機能は、Web ベースのプロジェクトで作業する開発者にとっては必須のツールである Firebug や Google Chrome Inspector などと同様の機能を備えています。デバッグビルドを使用すると、PhoneGap の開発者は、これらのツールを使用した場合と同様のメリットを受けることができます。


## 目次

1. [Build を使用するためのプロジェクトの設定](#project_build)
    1. [新しいアプリケーション](#new_build_project)
    2. [既存のアプリケーション](#existing_build_project)
2. [デバッグモードの実行](#running_debug_mode)
    1. [要素](#running_debug_mode_elements)
    2. [コンソール](#running_debug_mode_console)
3. [使用法の例](#example_use_case)
4. [最後に](#closing_remarks)


<a id="project_build"></a>
##Build を使用するためのプロジェクトの設定

Build を設定する場合は、以下の 2 つのケースが考えられます。

<a id="new_build_project"></a>
###新しいアプリケーション

ログイン後、[https://build.phonegap.com/](https://build.phonegap.com/) に移動し、「+ 新規アプリケーション」ボタンをクリックします。

次に、デバッグモードを有効にするために、「デバッグを有効にする」を選択します。

これで設定は完了です。この時点より、すべてのビルドで、PhoneGap Debug Build を使用してデバッグを実行できます。後でデバッグを無効にするには、アプリケーションを編集ページ（下の節で説明）で「デバッグを有効にする」オプションの選択を解除し、変更を保存します。

<a id="existing_build_project"></a>
###既存のアプリケーション

ログイン後、[https://build.phonegap.com/apps](https://build.phonegap.com/apps) に移動し、デバッグを有効にするアプリケーションをクリックします。 

次のページに、ビルドのステータスを知るのに役立つ情報や、アプリケーションに関する一般的な情報が表示されます。右上隅の「編集」ボタンをクリックすると、以下のようなページが表示されます。

このページから、「デバッグを有効にする」をクリックしてデバッグビルドを有効にします。アプリケーションに対する変更を保存するには、「保存」をクリックします。これで設定は完了です。この時点より、すべてのビルドで、PhoneGap Debug Build を使用してデバッグを実行できます。後でデバッグを無効にするには、「デバッグを有効にする」オプションの選択を解除し、変更を保存します。

<a id="runnin_debug_mode"></a>
##デバッグモードの実行

アプリケーションをデバッグモードで実行するには、https://build.phonegap.com/apps に移動し、適切なリンクをクリックしてご利用のプラットフォーム向けのダウンロードを実行し、デバイスまたはエミュレーターでアプリケーションを実行します。次に、右上隅の「編集」の隣に、「デバッグ」オプションが表示されます。このリンクをクリックすると、この時点で利用できるオプション（「要素」および「コンソール」）を含むページが表示されます。

<a id="running_debug_mode_elements"></a>
###要素：

この強力なツールを使用して、アプリケーションをリアルタイムで変更できます。その場で細かい変更やバグ修正を行う場合に便利な機能です。例えば、エラーを修正するために javascript を編集する、css スタイルを変更する、html を編集するといった使い方があります。
<a id="running_debug_mode_console"></a>
###コンソール：

もう 1 つの強力な機能です。デバッグ出力の表示や、javascript の操作を実行できます。例えば、バグの追跡や、リアルタイムでのアプリケーションログ出力の表示などの使い方があります。

<a id="example_use_case"></a>
##使用法の例


以下の説明を学習することで、デバッグに使用できるワークフローをより詳細に理解できるようになります。  
   
サンプルアプリケーション「Hello Debugging World」は、以下の場所からダウンロードできます。  
[https://github.com/hardeep/PhoneGap-Build-Debug](https://github.com/hardeep/PhoneGap-Build-Debug)

1）Phonegap Build で、「Hello Debugging World」の内容を含む新しいアプリケーションを作成します。手順について詳しくは、[https://build.phonegap.com/docs/git-hosting](https://build.phonegap.com/docs/git-hosting) を参照してください。

2）デバッグコンソールを開き、新しくビルドしたアプリケーションをデバイスまたはシミュレーターで起動します。リモート／デバイスの下にデバイスが表示されます（場合によっては、ページを更新する必要があります）。

![アプリケーションを編集ページ](images/phonegap-debug/connected.jpg)

3）強力なデバッグオプションの一部を紹介するために、この例では JQuery が使用されています。最初に、「要素」と「コンソール」というラベルの付いたそれぞれのセクションをクリックして、これから主に説明するこの 2 つのセクションについて簡単に確認してください。

![アプリケーションを編集ページ](images/phonegap-debug/elements.jpg)

![アプリケーションを編集ページ](images/phonegap-debug/console.jpg)


4）お気づきのとおり、ヘッダー内の phonegap.js のインクルード部分にタイプミスがあります。この行は以下のように記述する必要があります。

    <script stype="text/javascript" src="phonegap.js"></script> 

この対話的なデバッグセッションを使用しない場合は、コードを再ビルドし、シミュレーターまたはデバイスにコードを再度デプロイする必要があります。ただし、ここでは単純に JQuery を使用して必要な javascript ファイルを動的に読み込むことで、このエラーを修正し、テストを続けることができます。

コンソールに移動し、以下のコードを挿入します。

    $.getScript('phonegap.js', function() { alert('Load was performed.'); })

これで、デバイスまたはシミュレーターを確認した場合に、PhoneGap がロードされたことを示す警告が表示されます。

5）アプリケーションを起動する「onLoad()」をコンソールで呼び出して、テストを続行します。html ドキュメント内にタイプミスがあるので、何も起こらないことに気づくでしょう。以下の行の id 属性を変更します（属性をダブルクリックします）。

    <input type="button" id="buh_button" value="Check For Bugs">

この行を、以下の内容に変更します。

    <input type="button" id="bug_button" value="Check For Bugs">

このような変更は、css、html、javascript など、アプリケーションのあらゆる属性に適用できます。

6）「バグをチェック」をクリックします。この時点では、「他にバグはありません」という警告が表示されます。


<a id="closing_remarks"></a>
##最後に

これで、デバッグビルドの簡単なデモンストレーションを終了します。これまでの説明で、このようなデバッグツールによって時間を節約し手間を省くことができることを示すことができました。他に質問やコメントがある場合は、[http://community.phonegap.com](http://community.phonegap.com/nitobi/products/nitobi_phonegap_build) にご遠慮なく投稿してください。
