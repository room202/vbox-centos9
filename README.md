# VirtualBox に CentOS9をインストールする

## VirtualBoxの設定  



## CentOS9のインスール

`ESCキー`を押してスキップする  
![](images/030.png)

`続行`をクリック  
![](images/031.png)

`インスール先`をクリック  
![](images/032.png)

`完了`をクリック  
![](images/033.png)

`rootパスワード`をクリック  
![](images/034.png)

パスワードを２回入力して、`完了`を２回クリック  
![](images/035.png)

`ユーザーの作成`をクリック  
![](images/036.png)

- `フルネーム`を入力
- `□このユーザーを管理者にする`にチェックを入れる
- パスワードを２回入力する
- `完了`を２回クリック 

![](images/038.png)

`インストールの開始`をクリック
![](images/039.png)

`システムの再起動`をクリック  
![](images/040.png)

## 初期設定

ユーザー名をクリック  
![](images/041.png)

パスワードを入力  
![](images/042.png)

`必要ありません`をクリック  
![](images/043.png)

`ターミナル`アプリをクリック  
![](images/044.png)

下記コマンドを実行

```bash
sudo dnf upgrade -y
```

パスワードを入力する  
※入力されていないように見えるが、入力されている  
![](images/045.png)

`完了しました！`が表示されたらOK  
![](images/046.png)

下記コマンドを実行

```bash
LANG=C xdg-user-dirs-gtk-update
```

![](images/047.png)

`Update Names`をクリック  
![](images/048.png)

右上のエリアから再起動をする  
![](images/049.png)
![](images/050.png)
![](images/051.png)

再度ログインする  
![](images/052.png)
![](images/053.png)

`次回から表示しない`にチェックを入れて`古い名前のままにする`をクリック
![](images/054.png)

## SSHサーバーの起動

`ターミナル`アプリをクリック  
![](images/055.png)

下記コマンドを実行

```bash
sudo systemctl start sshd.service
```

![](images/056.png)

パスワードを入力する 
![](images/057.png)

```bash
sudo systemctl status sshd.service
```

![](images/058.png)

Active: active (running) になっていれば起動成功です。  
![](images/059.png)

## Tera TermからSSH接続

- `ホスト` : localhost  

![](images/060.png)

`続行`をクリック  
![](images/061.png)

`ユーザー名`、`パスフレーズ(パスワード)`を入力  
![](images/062.png)

SSH接続成功
![](images/063.png)
