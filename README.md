# iRIC ソルバテンプレート

## フォルダ・ファイルの説明

### install

iRIC のインストーラに同梱したいファイルを置きます。ここに置くファイルの例を以下に示します。

* definition.xml
* ソルバの実行プログラム (例: solver.exe. solver.py)
* 辞書ファイル (translation_ja_JP.ts など)
* README
* LICENSE

### src

プログラムのソースコードをここに置きます。
FORTRAN のプログラムを開発する場合のサンプルとして、 main.f90, iric.f90 が最初から置いてあります。

@TODO

iric_v4_solver.sln などは solver.sln などに名前を変える？

### lib

最新の iriclib.lib が最初から置いてあります。

ソルバ開発者がこのフォルダの内容を変更する必要はありません。

### .github

Github actions の機能を使い、ソルバの自動ビルドや、ソルバのインストーラへの自動登録処理を実行する
ためのファイルが置いてあります。

ソルバ開発者がこのフォルダの内容を変更する必要はありません。

## プログラムの初期登録

### github へのリポジトリの作成

1. Github で、アカウントとリポジトリを作成します
2. リポジトリに、インストーラにファイルを同梱するためのトークンを登録します。トークンについては別途ご連絡します。

@TODO ちゃんと説明を書く

### 初期作業

config.json の内容を編集してください。

config.json の項目について以下に説明します。

#### solver_id

ソルバのインストール先フォルダ名などに使われるIDです。ソルバごとに違う値になるよう設定してください。
英数字と '-', '_' などで構成される文字列を指定し、'\', '/' などファイル名に使用できない文字は使わないでください。

#### public

true を指定すると、 developer 版、公開版両方に登録されます。
false を指定すると、 developer 版にのみ登録されます。

#### build

true を指定すると、最新のソースコードから自動的にプログラムのビルドが実行されます。
ビルドには make.bat が使用されます。

false を指定すると、ビルドは実行されません。以下の場合は、 false を指定してください。

* 自分でプログラムをビルドして install フォルダに置き、それをそのまま公開してほしい場合
* ソルバが python で開発されている場合

### インストールするファイルの準備

#### 自動ビルドをしない場合

1. config.json で、 build に false を指定します。
2. install フォルダの下に、インストールしたいファイルを置きます。

#### 自動ビルドをする場合

1. config.json で、 build に true を指定します。
2. src フォルダの内容、make.bat の内容を編集し、make.bat を実行するとinstall フォルダ内に、
プログラムの実行ファイルが生成されるよう調整しておきます。

### github へのファイル一式の登録

ファイル一式を git でコミットし、 github にプッシュします。(プッシュとは、サーバへのアップロードのことです)
以上で、インストーラに最新のソルバが登録されます。

@TODO git を使ったことがない人でも簡単にできるよう準備する。 (例: Visual Studio からの登録、バッチファイルでの登録)

### 確認

1. Github のリポジトリの actions のタブで、無事にインストーラへの登録処理が行われたか確認します。
2. iRIC v4 のメンテナンスツールで、自分が登録したソルバが表示されることを確認します。

## プログラムの更新

プログラムの内容を変更した上で、上記の「github へのファイル一式の登録」処理を行います。すると、最新のプログラムがインストーラに登録されるようになります。

### 注意

ユーザに、ソルバの新しいバージョンが登録されたことが通知され、簡単に更新が行われるようにするためには、バージョン番号・リリース日付を更新する必要があります。

install フォルダ内の definition.xml の、version, release の値を更新した上で、ファイル一式の登録を行ってください。
