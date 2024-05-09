# VirtualBox に CentOS Stream 9をインストールする

## CentOS Stream 9のイメージをダウンロード

下記URLからCentOS Stream 9のイメージをダウンロード

https://www.centos.org/

※ダウンロードに時間がかかる場合は、[コチラ](https://drive.google.com/file/d/11A_h40pmYaYzP_ozPBaRSnOncTeYbXez/view?usp=drive_link)のGoogleドライブからダウンロード

![](images/001.png)
![](images/002.png)
![](images/003.png)

`ダウンロード`フォルダに保存  
※サイズが大きいので時間がかかる
![](images/004.png)

## VirtualBoxの設定

`新規`をクリック  
![](images/005.png)

`名前`に`CentOS9`と入力して`ISOイメージ`の`↓`をクリック  
![](images/006.png)

`その他`をクリック
![](images/006-2.png)

`ダウンロード`フォルダからダウンロードした`CentOS-Stream-9～.iso`ファイルを選択して`開く`をクリック
![](images/006-3.png)

`自動インストールをスキップ`にチェックを入れて`次へ`をクリック  
![](images/006-4.png)

`EFIを有効化(一部のOSのみ)`にチェックを入れて`次へ`をクリック  
![](images/007.png)

`次へ`をクリック  
![](images/008.png)

`完了`をクリック  
![](images/009.png)

### ポートフォワーディングの設定

`設定`をクリック  
![](images/010.png)

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

`OK`をクリック  
![](images/016.png)

## CentOS Stream 9のインスール

`起動`をクリック  
![](images/017.png)

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

※画面がバグって見切れてしまう場合  
- VirtualBoxの`設定`→`ディスプレイ`→`グラフィックコントローラ`を`VBoxVGA`または`VMSVGA`に変更する
  - 途中で`表示`の`仮想スクリーン１`を`1024×768`に設定を変更する

※マウス操作ができない場合  
- VirtualBoxの`設定`→`システム`→`ポインティングデバイス`を`USBタブレット`または`PS/2マウス`に変更する

※上記手順で直らない場合は、一旦Windowsを再起動してみる

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

インストール中  
※少し時間がかかる  
![](images/039-2.png)

`システムの再起動`をクリック  
![](images/040.png)

## CentOS Stream 9の初期設定

ユーザー名をクリック  
![](images/041.png)

パスワードを入力  
![](images/042.png)

`必要ありません`をクリック  
![](images/043.png)

インストール完了
![](images/043-1.png)

## Tera TermからSSH接続

- `ホスト` : localhost  
- `TCPポート` : 22

![](images/060.png)

`続行`をクリック  
![](images/061.png)

`ユーザー名`、`パスフレーズ(パスワード)`を入力  
![](images/062.png)

SSH接続成功
![](images/063.png)

### DeleteキーとMetaキーの設定

`設定`→`キーボード`をクリック  
![](images/070.png)

- `Deleteキー`のチェックを外す
- `Metaキー`を`on`に変える
- `OK`をクリック

![](images/071.png)


`設定`→`設定の保存`をクリック
![](images/073.png)

`保存`をクリック  
![](images/074.png)

`はい`をクリック  
![](images/075.png)

## アップデート

下記コマンドを実行してCentOSをアップデートする

```bash
sudo dnf upgrade -y
```

![](images/080.png)

パスワードを入力する  
※入力されていないように見えるが、入力されている  
![](images/081.png)

インストール中  
※エラーが出る場合は、`ユーザーの作成`で`このユーザーを管理者にする`にチェックしなかった場合

対処方法  
```bash
su -
visudo /etc/sudoers

# 101行目付近rootの下に下記を追記
lightbox    ALL=(ALL)       ALL
```

![](images/082.png)

`完了しました！`が表示されたらOK  
![](images/083.png)

## 終了方法

VirtualBoxの`✕ボタン`をクリック  
![](images/090.png)

`仮想マシンの状態を保存`をクリック  
![](images/091.png)

## 起動方法

起動したい対象を選択して`起動`ボタンをクリック  
![](images/092.png)

起動後は最小化しておく  
![](images/093.png)
