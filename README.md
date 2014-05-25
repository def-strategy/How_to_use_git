How_to_use_git
==============

Git及びGitHubの使い方を簡単に説明する（予定）ためのリポジトリです。

## そもそもGitって何さ
分散バージョン管理ツールです。  
バージョン管理ツールと言えばSubversion辺りが良く知られていますが、
Gitは分散管理という点がSubversionと異なります。  
ローカル上でもバージョン管理ができる、というのが大きなメリット（かもしれません）。

## Gitインストール
1. [git for Windows](http://msysgit.github.io/) からgitのインストーラをダウンロードする
2. インストールを進めていくとこんな画面が出てきます。PATHの設定画面です。
   ![環境設定](images/git\_path\_env.PNG)  
   どれでも構わない感はありますが、2番目(Use Git from the Windows...)を選ぶのが無難と思います。

3. 次画面はちょっと重要です。結論から言うと、2番目をお勧めします。
   ![改行コード変換設定](images/git\_endingConversion\_env.PNG)  
   何をしようとしているかというと、リポジトリへのチェックイン時、及びリポジトリからの  
   チェックアウト時における改行コードの扱いをどうするか決めようとしています。  
   WindowsとUnix系では改行コードに違いがあり（WindowsはCR+LF, UNIX系はLF）、改行コードが  
   そのままだとUnix系OSの使用者とWindowsの使用者が共同作業するときに困ることになるので、  
   チェックアウト時に  LF -> CR+LFに変換しようというのが一番上の選択肢です。  
   ...が、個人的には2番目の選択肢を選んで、改行コードを自動判別できるエディタを使うのが  
   最良かと思います（ていうか大体のコーディング用エディタはそうなってるはず）。

4. Nextをクリックするとインストールが始まって、ほどなくして終わります。  
   これでインストールは完了です。

## Gitセットアップ
1. まず、適当なところで右クリックして、Git Bashを選択、起動します。
2. Gitで利用する名前とメールアドレスを設定します。名前は英字で入力してください。
   以下のようにコマンドを打ちます。  
   (""で囲まれた部分は適宜読み替えてください)  
```
$ git config --global user.name "hogehoge"  
$ git config --global user.email "hogehoge@example.com"  
```
ここで設定する名前はGitのコミットログなどに使われます。GitHubを使う際にも公開されます。  
ひとまず初期設定は完了です。他にも色々設定できる項目があるので、適宜ググってみてください。

## ssh keyの設定
gitサーバーとのやり取りはSSHによる公開鍵認証で行うので、そのための公開鍵と秘密鍵のペアを作成します。

* Git Bashを起動
* 以下のコマンドを実行
```
$ ssh-keygen -t rsa -C "hogehoge@example.com"
Generating public/private rsa key pair.
Enter file in which to save the key ((秘密鍵が保存されるフォルダ)/.ssh/id_rsa):何も入れずにEnter
Enter passphrare (empty for no passphrase):好きなパスフレーズを入力 画面に出力されないので注意
Enter same passphrase again:同じパスフレーズを入力 画面に出力されないので注意
Your identification has been saved in (秘密鍵が保存されるフォルダ)/.ssh/id_rsa.
Your public key has been saved in (秘密鍵が保存されるフォルダ)/.ssh/id_rsa.pub.
The key fingerprint is:
(SSH Fingerprintが表示される) hogehoge@example.com
```
* GitHubページの右上にある工具のようなアイコン(Account Settings)を開いて、  
   ウィンドウ左部のSSH keysを選択。Add SSH keyをクリックして、先程作成した  
   (秘密鍵が保存されるフォルダ)/.ssh/id_rsaの中身をkeyフォームに丸々コピー&ペースト。  
   Titleは何でも良いと思います。  
   私はデスクトップとラップトップ両方でGitHubと通信するつもりなので、Desktop_ssh_keyと付けました。
* 入力したらAdd keyをクリック。正しく公開鍵が登録されていれば、アカウント作成時に  
   登録したメールアドレスにメールが来ているはずです。
* 以下コマンドを実行。
```
$ ssh -T git@github.com
Enter passphrase for key '(秘密鍵が保存されるフォルダ)/.ssh/id_rsa': パスフレーズを入力 画面に表示され(ry
```
以下のように表示されればOKです。  
```
Hi (ユーザー名)! You've successfully authenticated, but GitHub does not provide shell access.
```

## SourceTreeの導入
ここを参考にしてください。。。  
[SourceTree for WindowsからGitを利用する](http://codezine.jp/article/detail/7400)
