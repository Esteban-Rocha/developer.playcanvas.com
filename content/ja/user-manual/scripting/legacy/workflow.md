---
title: ワークフロー
template: usermanual-page.tmpl.html
position: 3
---

PlayCanvasアプリケーションを開発しながら、アプリケーションのスクリプトを実行する方法は2つあります。開発や反復をしている際はコードにローカルサーバを使用します。共有や公開するためには、コードリポジトリを使用します。それぞれには異なる利点があるので、2つの間で切り替えて使用します。

## PlayCanvas コードディレクトリ

<img src="/images/platform/playcanvas_repo.jpg" style="max-width: 100%" />

現時点でPlayCanvasアプリケーション用のスクリプトを開発する最も簡単な方法は、内蔵のコードエディタを使用して、サーバがいつでもそれらにアクセスできるよう、PlayCanvasでスクリプトを格納することです。

プロジェクト作成時、デフォルトでこのように設定されます。外部コードのリポジトリにプロジェクトをリンクしている場合は、いつでもコードリポジトリの同期を外してコードディレクトリの使用に戻すことができます。

### 新規スクリプトの追加

<img src="/images/user-manual/scenes/components/component-script.png" style="width: 300px; float: right; padding: 20px; padding-top: 0px;"/>

新しいスクリプトを追加するには、Add Scriptをクリックするか、PlayCanvasエディタでシーンを開き、スクリプトを追加したいエンティティでScript Componentを選択するか、追加します。その後、スクリプトピッカーコントロールでURLフィールドをクリックし、スクリプトの名前を入力してEnterキーを押します。スクリプトの名前はリンクになるので、それをクリックしてコードエディタを開きます。スクリプト名の横にあるXをクリックしてこのコンポーネントからスクリプトを削除します。

代わりに、アセットパネルからスクリプトコンポーネントにスクリプトをドラッグ＆ドロップすることができます。

<div class="alert alert-info small">
PlayCanvasを使用してスクリプトを格納している場合のみ、スクリプトを編集することができます。外部のコードリポジトリを設定している場合は、PlayCanvas経由でスクリプトを編集することはできません。ローカルサーバを使用するか、リポジトリにコードをコミットする必要があります。
</div>

スクリプトリンクをクリックすると新しいタブで内蔵のコードエディタが開きます。新しいタブを表示するにはplaycanvas.comからのポップアップを許可する必要があります。初めてスクリプトを編集するとき、それは作成され、保存されます。次に、プロジェクトダッシュボードの[Code][1]タブ、またはエディタの [Scripts Explorer][2] で全てのスクリプトを確認することができます。

## ローカルサーバ

ゲームを開発するには迅速な反復時間が重要です。スクリプトファイルは、ローカルコンピュータ上に存在そこで編集します。ローカルマシンで小さなウェブサーバーを実行することで、スクリプトに加える変更はブラウザを更新してアプリケーションに即座に組み込まれるようになります。

ウェブサーバの実行は簡単です。コンピュータ上でコードが存在するフォルダ内に起動スクリプトをドロップしてから、サーバを起動します。 ローカルサーバのインストールと設定は、プラットフォームごとに若干異なります。

### Windows

* まず[こちら][3]からPythonをインストールします。デフォルトでは`localserver.bat`はPython2.7を使用しますが、最近のバージョンで動作するように変更することができます。

* [サーバスクリプトをダウンロード][4]

* `localserver.bat`ファイルをスクリプトが含まれているフォルダに保存。

* サーバをダブルクリックして実行。次のようなメッセージを持つ端末プロンプトが表示されます：
~~~sh~~~
Serving HTTP on 0.0.0.0 port 51000 ...
~~~

### OS X と Linux

* [サーバスクリプトをダウンロード][5]

* スクリプトが含まれているフォルダに`localserver`ファイルを保存。

* サーバーを実行可能にする。コマンドラインで次を入力
~~~sh~~~
chmod a+x /path/to/scripts/localserver
~~~

* LocalServerファイルをダブルクリックしてサーバを起動することができます。次のようなメッセージを持つ端末プロンプトが表示されます：
~~~sh~~~
Serving HTTP on 0.0.0.0 port 51000 ...
~~~

### ローカルサーバに対してアプリケーションを実行

ローカルサーバを起動したら、 ウェブブラウザから`http://localhost:51000` に移行してサーバが正しく実行されているかをテストして確認することができます。 次のようなファイルのディレクトリが表示されます：

![served directory](/images/platform/localserver.png "ローカルサーバディレクトリ")

`Launch Local`コマンドを使用してPlayCanvasエディタからシーンを起動すると、アプリケーションは`http://localhost:51000` でスクリプトを検索します。つまり、ローカルサーバを実行している場合、ブラウザはマシンからスクリプトを読み込みます。プロジェクトのためにコードリポジトリを設定している場合（ 次のセクションを参照してください ）、通常の`Launch`コマンドを使用して実行することができ、スクリプトは完全にコードリポジトリから提供されます。

## コードリポジトリ

ローカルサーバの実行は簡単ですが、アーティストや制作スタッフなど、コードの編集を行わないチームメンバーには必要のないものです。 さらに、アプリケーションを公開可能な形式でエクスポートするには、スクリプトコードをエクスポートされたパッケージに含めることができるように、 PlayCanvasサーバーにアクセス可能な場所に置く必要があります。

このようなケースのために外部コードリポジトリへの対応を提供しています。つまり、ソース管理システムと当社のサーバー間の接続です。

<img src="/images/platform/external_repo.jpg" style="max-width:100%" />

GitとMercurialリポジトリに完全に対応しています。

リポジトリをクローンするためには、最上位の入力フィールドにクローンのURLを入力する必要があります。次に、Enterを押します。PlayCanvasは、裏でコードのコピーをクローンまたは同期させ、サーバ上で保持します。この同期オペレーションのステータスはコードページに表示されます。ステータスが'グリーン'になると、リポジトリのクローンが完成します。

有効なクローンURLの例は次の通りです：
* `ssh://hg@bitbucket.org/username/repository`
* `https://username@bitbucket.org/username/repository`
* `git@github.com:username/repository.git`
* `https://github.com/username/repository.git`
* PlayCanvasからアクセス可能なその他のGit またはMercurial URL。

PlayCanvas1Editorからアプリケーションを実行すると、その際にコードが含まれるようになりました。ローカルサーバを実行する必要はありません。また、コードリポジトリが設定されているシーンをエクスポートする場合、コードがエクスポートに含まれます。

## すべてのリポジトリのアクセス権を付与する方法

URLの下のボックスに表示されるパブリックキーは、リポジトリのクローンを作成する権限を取得するために使用されます。例えば <a href="https://bitbucket.org" target="_blank">Bitbucket</a> または <a href="https://github.com" target="_blank">Github</a>でアクセスできるリポジトリをクローンする許可を取得するあめには次のことを行う必要があります：

1. パブリックキーをコピー
2. <a href="https://bitbucket.org" target="_blank">Bitbucket</a>または<a href="https://github.com" target="_blank">Github</a>のアカウントに移行。
3. SSH Keysセクションでパブリックキーを追加。
4. リポジトリを同期。

アカウントに対して、一度のみ実行する必要があります。

## ひとつのリポジトリへのアクセス権を付与する方法

特定のリポジトリのみにアクセスしたい場合、次のようにします：

1. パブリックキーをコピー
2. <a href="https://bitbucket.org" target="_blank">Bitbucket</a>または<a href="https://github.com" target="_blank">Github</a>のリポジトリ設定に移行。
3. Deploy Keysセクションでパブリックキーを追加。
4. リポジトリを同期。

## 切り替え

<img src="/images/user-manual/launch-options.jpg" style="float: right; padding: 20px; padding-top: 0px;"/>

ローカルで実行されるサーバで起動する場合はUse Local Serverを選択します。サーバ上のコードを使用して起動する場合は選択を外します。例えば、コードリポジトリーまたはコードディレクトリーです。

シーンのエクスポートは、PlayCanvasサーバのソースコードリソースのみを使用します。エクスポートする前に弊社サイトにコードをアップロードまたは同期してください。

[1]: /user-manual/dashboard/code
[2]: /user-manual/designer/assets
[3]: http://www.python.org/download/
[4]: /downloads/localserver.bat
[5]: /downloads/localserver

