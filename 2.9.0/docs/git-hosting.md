# Git ホスティング

  注意：Adobe® PhoneGap™ Build での Git リポジトリのホスティングは段階的に廃止する予定です。既に作成済みのリポジトリのサポートは継続されますが、新しいリポジトリは作成できなくなります。

  現在、PhoneGap Build では、アプリケーション向けの認証済みの Git ホスティングが用意されています。このホスティングによって、既存のワークフローに PhoneGap Build を容易に統合できます。個人の資格情報を公開したり、お使いのプライベートリポジトリに対する認証を受けたりする必要はありません。

  このドキュメントでは、PhoneGap Build を Git と共に使用するためのサンプルワークフローについて説明します。ただし、Git を使用するメリットのひとつに、Git の最上位にある UI、プラグインまたは使い慣れた IDE との統合など、選択した任意のツールを使用して作業できることがあります。プロジェクトで Git とは異なるバージョン管理システムを使用し、`git-svn` などのツールだけを使用して PhoneGap Build に作成したアプリケーションをプッシュすることもできます。

  まず、ユーザーアカウントを設定し、弊社で正しく認証できるようにします。[ユーザー管理](/people/edit)に移動し、「 __ユーザー名__ 」フィールドが入力されていることを確認します（ユーザー名はリポジトリの固有の URL を生成するために使用されます）。また、弊社の Git サーバーでユーザーを認証するために、「 __公開 SSH キー__ 」を入力する必要もあります。`ssh-keygen` ユーティリティがシステムにインストールされている場合は、このユーティリティを使用して SSH キーを生成できます。詳しくは、お使いのプラットフォームのドキュメントを参照してください。

  以上の操作が完了したら、新しいリポジトリを作成できます。[アプリケーションのリスト](/apps)ページに移動し、「 __新規アプリケーション__ 」をクリックします。アプリケーションのタイトルを入力し、「新規 git リポジトリを作成」を選択して、「 __アップロード__ 」をクリックします。

  この時点では、アプリケーションのビルドは開始されません。ビルド対象のアプリケーションがまだ弊社にないからです。次の手順で、アプリケーションを作成してください。

  ファイルシステム上に新しいディレクトリを作成し、そのディレクトリ内に `index.html` ファイルを配置します。そのディレクトリで Git リポジトリを初期化します。この操作によって、アプリケーションを PhoneGap Build にプッシュして、ビルドを開始できます。以下のようなワークフローになります。

    ~ $ mkdir git-hosted-app
    ~ $ cd git-hosted-app/
    ~/git-hosted-app $ git init
    Initialized empty Git repository in /Users/andrewlunny/git-hosted-app/.git/
    ~/git-hosted-app $ echo "<h1>Hello World</h1>" > index.html
    ~/git-hosted-app $ git add .
    ~/git-hosted-app $ git commit -m "initial commit"
    [master (root-commit) 929f0d6] initial commit
     1 files changed, 1 insertions(+), 0 deletions(-)
     create mode 100644 index.html

  「[はじめに](/docs/start)」では、初心者向けに、アプリケーション内に他のファイル（`config.xml` や `icon.png`）も配置することを勧めていますが、この Hello World アプリケーションではこれらのファイルを配置する必要はありません。次に、アプリケーションを PhoneGap Build にプッシュします。弊社がリモートとして指定した URL を追加し、マスターブランチをプッシュします。

    ~/git-hosted-app $ git remote add phonegap git@git.phonegap.com:zubzub/61_GitHostedApp.git
    ~/git-hosted-app $ git push phonegap master
    Counting objects: 3, done.
    Writing objects: 100% (3/3), 227 bytes, done.
    Total 3 (delta 0), reused 0 (delta 0)
    remote: updating repo zubzub/61_GitHostedApp
    To git@git.phonegap.com:zubzub/61_GitHostedApp.git
     * [new branch]      master -> master
    
  リモート名 `phonegap` は任意です。`git remote add gitgap git@git.phonegap.com:zubzub/61_GitHostedApp.git` など、自由に選択したリモート名を指定できます。

  ただし、この時点ではまだ PhoneGap Build でアプリケーションを受信しておらず、アプリケーションはビルド用のキューに格納されています。数分後に、アプリケーションの設定がすべて完了し、ダウンロードできるようになります。

  ![ビルド完了](images/getting-started/downloads-ready.png)

  この段階で、アプリケーションをダウンロードしてテストし、動作の状況を確認して、変更を加えることができます。変更内容をビルドする場合は、変更をローカルの git リポジトリにコミットしてから、もう一度 `git push` を実行してください。

    ~/git-hosted-app $ git commit -m "fixed phone explosion bug"
    [master 57c6c11] fixed phone explosion bug
     1 files changed, 0 insertions(+), 42 deletions(-)
    ~/git-hosted-app $ git push phonegap master
    Counting objects: 5, done.
    Writing objects: 100% (3/3), 288 bytes, done.
    Total 3 (delta 0), reused 0 (delta 0)
    remote: updating repo zubzub/61_GitHostedApp
    To git@git.phonegap.com:zubzub/61_GitHostedApp.git
       b6ea0d9..57c6c11  master -> master

  ブラウザーに戻ると、アプリケーションが「保留中」状態である（PhoneGap Build によりアプリケーションが再度キューに格納されている）ことが表示されます。アプリケーションはまもなく使用できるようになります。
