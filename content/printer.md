# 学校のプリンターシステム(SUICAPRIN)を使う方法

## 学校のサーバーから印刷する方法

すでにプリンタがセットアップされているので、MyVolumeにどうにかしてファイルを置き、`lpr <ファイル名>`で印刷できる。

## 個人のPCから印刷する方法

### 学校のLinuxサーバーにsftpで接続する

`oli.sic.shibaura-it.ac.jp`もしくは`yli.sic.shibaura-it.ac.jp`に接続する。

### 京セラのプリンター(KX5052)のppdファイルをダウンロードする。

`get /etc/cups/ppd/KX5052.ppd`

### プリンターを登録する

学籍番号は自分のものに置き換える

`sudo lpadmin -p sit_kyocera -E  -v lpd://spl3.sic.shibaura-it.ac.jp/KX_学籍番号 -P ./KX5052.ppd`

### 印刷をテストする

`lpr ./report.pdf -P sit_kyocera`


キューに入っているか、以下のURLから確認する。

http://spl3.sic.shibaura-it.ac.jp
