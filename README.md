GitHubにアップロードしてある公開鍵を自動で配置するスクリプト

## 公開鍵をGitHubにアップロード
1. 右上のアイコンをクリックして「Settings」を選択します。  
2. SSH and GPG keysを選択します。
3. New SSH keyを選択します。
4. Titleに任意の名前を入力します。
5. Keyに公開鍵を入力します。
6. Add SSH keyを選択します。

## サーバーへ公開鍵を配置
以下の手順に従って公開鍵を配置します。
wgetとvimなどの任意のエディタが必要です。
ない場合はdnf install wget vimやapt install wget vimなどでインストールしてください。
```
## ユーザーの切り替え(公開鍵を配置したいユーザーへ)
su [ユーザー名]

## スクリプトのダウンロード
wget https://raw.githubusercontent.com/dodolia907/ssh/main/auth.sh

## 自分のGitHubアカウントに変更
## https://github.com/dodolia907.keys を https://github.com/[自分のGitHubアカウント名].keys に変更
vim auth.sh

## 実行
bash auth.sh
```
アカウントを変更せずに実行する場合は以下のコマンドを実行します。
```
curl -s https://raw.githubusercontent.com/dodolia907/ssh/main/auth.sh | bash
```

## 公開鍵認証でSSH接続
~/.ssh/configに以下の内容を追記して保存します。
```config
Host [任意のホスト名]
    HostName [ホスト名]
    User [ユーザー名]
    IdentityFile ~/.ssh/[秘密鍵のファイル名]
```
ターミナルで　`ssh [任意のホスト名]` と入力すると接続できます。
