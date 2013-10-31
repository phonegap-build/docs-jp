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

# プラグインの提供

弊社では、開発者と協力して、PhoneGap Build で使用するためのプラグインの提供を考えています。現時点では、PhoneGap Build システムに追加されるすべてのプラグインに、すべての PhoneGap Build ユーザーがアクセスできますが、今後は、PhoneGap Build プラグインの使用法に別のメカニズムが導入される可能性があります。

PhoneGap Build では、iOS および Android 向けのプラグインをサポートしています。現時点では、これらの 2 つのプラットフォームでの優れたプラグインの操作性の実現に重点を置いています。

PhoneGap Build のプラグインの開発には、以下の 2 点の考慮事項があります。

1. プラグインコードの開発
2. 各種ツールで使用するためのプラグインのパッケージ化

ツールや仕様へリンクされたバージョンが、PhoneGap Build で使用されるバージョンです。

## プラグインコードの開発

PhoneGap プラグインは以下のものから構成されます。

* JavaScript ファイル：PhoneGap プラグインのインターフェイスを実装します。例外として扱う必要がある適切な理由がない限り、サポートされる両方のプラットフォームで同じ JavaScript コードを実行してください。
* サポートされるプラットフォームのそれぞれに対応するネイティブクラス：PhoneGap プラグインのインターフェイスを実装します。
* 関連する依存ファイルとアセット：例えば、プラグインロジック全体、ネイティブ側の UI アセットまたは www 側の UI アセットを実装するために、複数のネイティブクラスが必要になる場合があります。

PhoneGap Build 向けに開発するプラグインは常に、PhoneGap の最新リリース（このドキュメントの執筆時点では 2.1）を対象として開発し、テストする必要があります。

プラグイン開発に関する最新の情報は、[docs.phonegap.com][pgdocs] で参照できます。

## プラグインのパッケージ化

PhoneGap Build では [pluginstall][pins] ツールを使用して、ユーザー向けに生成されるネイティブプロジェクトにプラグインをインストールします。現時点で使用している pluginstall のリリースは `0.5.0` です。

pluginstall で使用するプラグインの正しい形式は、[個別の仕様][spec]に記載されています。その仕様に従ってビルドされたプラグインの例については、[ChildBrowser プラグイン][child]を参照してください。このプラグインは現在、PhoneGap Build でアクティブなプラグインです。

サポートされている各プラットフォーム向けにプラグインが正しくパッケージ化されているかを確認するには：

1. そのプラットフォーム向けの新しい Cordova プロジェクトを作成します。プラグインを参照し使用するように、生成された `index.html` ファイルを編集します。
2. 適切な pluginstall コマンドを実行します。例えば、`/Users/alunny/dev/plugin` に保存されたプラグインを `/Users/alunny/dev/my_project` に保存された iOS プロジェクトにインストールする場合、以下のコマンドを実行します。

    `pluginstall ios /Users/alunny/dev/my_project /Users/alunny/dev/plugin`

3. プロジェクトがエラーなしにビルドできること、プラグインがインクルードされていること、およびそのプラグインを使用する JavaScript コードが正しく実行されることを確認します。

上記のすべてのツールおよび仕様は、現在も開発が続いています。pluginstall または仕様に制約や誤りが見つかった場合は、該当する GitHub プロジェクトで問題点を報告してください。

## プラグインの送信

プラグインが問題のない状態になったら、[build@phonegap.com](mailto:build@phonegap.com) まで連絡してください。プラグインを PhoneGap Build に統合するための次の手順をお知らせします。

PhoneGap Build へのプラグインの追加基準は、大まかに言って以下のとおりです。

1. ユーザーとって有効な価値が、プラグインによって付加されると考えられる。
2. プラグインを使用してアプリケーションをビルドでき、それが動作することが確認できる。
3. ソースコードを簡単に確認でき、懸念事項（セキュリティリスク、コンパイラーの警告など）がある場合に通知できる。

以上のいずれかの条件を満たさない場合は、作成者に懸念事項について連絡します。解決策が見つかることを期待します。プラグインがこれらの標準を満たさないという懸念がある場合は、支援いたしますので開発時にお問い合わせください。

プラグインの開発手順は現在も検討中です。そのため、システムにプラグインを追加するまでの期間は現時点では明示できません。開発に関するプロセスが複数のプラグインに基づいて確認された場合は、このドキュメントが更新されます。

[pgdocs]:http://docs.phonegap.com/jp/2.7.0/guide_plugin-development_index.md.html
[pins]:https://github.com/alunny/pluginstall
[spec]:https://github.com/alunny/cordova-plugin-spec
[child]:https://github.com/alunny/ChildBrowser
