# VirtualBox に CentOS Stream 9をインストールする

## CentOS Stream 9のイメージをダウンロード

下記URLからCentOS Stream 9のイメージをダウンロード

https://www.centos.org/

![](images/001.png)
![](images/002.png)
![](images/003.png)

`ダウンロード`フォルダに保存  
※サイズが大きいので時間がかかる
![](images/004.png)

## VirtualBoxの設定

`新規`をクリック  
![](images/005.png)

`名前`に`CentOS9`と入力して`次へ`をクリック  
![](images/006.png)

`EFIを有効化(一部のOSのみ)`にチェックを入れて`次へ`をクリック  
![](images/007.png)

`次へ`をクリック  
![](images/008.png)

`完了`をクリック  
![](images/009.png)

`設定`をクリック  
![](images/010.png)

### ポートフォワーディングの設定

`ネットワーク`をクリック  
![](images/011.png)

`高度`をクリック  
![](images/012.png)

`ポートフォワーディング`をクリック  
![](images/013.png)

`+`マークをクリック  
![](images/014.png)

下記設定の通りRuleを追加して`OK`をクリック  
![](images/015.png)

**設定**

| ポート | 用途 |
| ----- | ---|
| 22   | SSH用    |
| 80   | HTTP用   |
| 3306 | MySQL用  |
| 8080 | Tomcat用 |
| 20   | FTP用    |
| 21   | FTP用    |
| 445  | Samba用  |

`OK`をクリック  
![](images/016.png)

## CentOS Stream 9のインスール

`起動`をクリック  
![](images/017.png)

`↓`をクリック  
![](images/018.png)

`その他`をクリック  
![](images/019.png)

`ダウンロード`フォルダにダウンロードしたCentOS Stream 9の`.iso`ファイルを選択して`開く`をクリック
![](images/020.png)

`マウントとブートのリトライ`をクリック  
![](images/021.png)

このような画面が表示されたら`次回からこのメッセージを表示しない`にチェックして`キャプチャー`をクリック  
※右Ctrlキーで抜け出せる  
![](images/022.png)

`Test this media & install CentOS Stream 9`のまま`Enter`  
![](images/023.png)

右のウィンドウが表示されていたら邪魔なので、赤枠のアイコンをクリックして閉じる  
![](images/024.png)
![](images/025.png)

`ESCキー`を押してスキップする  
![](images/030.png)

`続行`をクリック  
![](images/031.png)

`インストール先`をクリック  
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

## CentOS Stream 9の初期設定

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

### Deleteキーの設定

`設定`→`キーボード`をクリック  
![](images/070.png)

`Deleteキー`のチェックを外して`OK`をクリック  
![](images/071.png)
![](images/072.png)

`設定`→`設定の保存`をクリック
![](images/073.png)

`保存`をクリック  
![](images/074.png)

`はい`をクリック  
![](images/075.png)



