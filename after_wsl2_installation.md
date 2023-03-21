# WSL2でインストールしたUbuntuの基本設定

## WindowsのマイドキュメントフォルダをWSL2のホームディレクトにマウントする

WSL2のUbuntuからWindowsのマイドキュメントフォルダへは
`/mnt/c/Users/ユーザ名/Documents`からアクセスできますが，
簡単にアクセスするためにWindowsのマイドキュメントフォルダの
シンボリックリンクをUbuntuのホームディレクトリ以下に張ります．

手順は以下になります．

1. スタートメニューからUbuntuを起動する．
1.  WindowsホームディレクトリのシンボリックリンクをUbuntuに張る（ユーザ名の部分は自分のWindowsユーザー名に置き換えること）．
   
```
ln -s /mnt/c/Users/ユーザ名/Documents/ Documents
ln -s /mnt/c/Users/ユーザ名/Downloads/ Downloads
```

これでUbuntuの`~/Documents`がWindowsのマイドキュメントフォルダが，`~/Download`がWindowsのダウンロードフォルダに紐付けられます．

## インストール済みパッケージのアップデート

WSL2にインストールしたUbuntuのシステムをアップデートします．
これはaptコマンドでインストールしたアプリケーションのアップデートになります．セキュリティ対策のためにも週に1回程度はアップデートをした方がよいでしょう．初回のアップデートには時間がかかることがあります．

```
sudo apt update && sudo apt upgrade -y
```

## 日本語入力システムのインストール

コンソールでの日本語表示はできますが，UbuntuのGUIソフトウエアでの日本語表示と日本語入力のための設定を行います．
まずは必要最低限の日本語フォントをUbuntuにインストールします．

フリーのtakaoフォントとRictyフォントをインストールします．

```
sudo apt install fonts-takao
sudo apt install fonts-ricty-diminished
```

日本語変換プログラムmozcをインストールします．
GUIソフトウエアでの日本語入力に必要です．

```
sudo apt install fcitx-mozc
fcitx
im-config -n fcitx
fcitx-config-gtk3
```

日本語入力システムの起動設定を行います．

```
cat 'export GTK_IM_MODULE=fcitx' >> ~/.bashrc
cat 'export QT_IM_MODULE=fcitx' >> ~/.bashrc
cat 'export XMODIFIERS="@im=fcitx"' >> ~/.bashrc
cat 'export DefaultIMModule=fcitx' >> ~/.bashrc
cat 'fcitx-autostart > /dev/null 2>&1' >> ~/.bashrc
```

# 研究用アプリケーションのインストール

## Cコンパイラのインストール

gccなどのC言語開発をインストールします．
Cプログラムのコンパイルをしない方はインストールする必要はありません．

```
sudo apt update
sudo apt install build-essential
```

## Fortranコンパイラのインストール

Fortran95コンパイラ（gfortran）をインストールします．
Fortranプログラムのコンパイルをしない方はインストールする必要はありません．

```
sudo apt update
sudo apt install gfortran
```

## 地図ソフトウエアのインストール
GrADSとGMTをインストールします．
GrADSやGMTが何かわからない人はインストールする必要はありません．

GrADSをインストールします．

```
sudo apt update
sudo apt install grads
```

GMTをインストールします．

```
sudo apt update
sudo apt install gmt
```

## 統計解析ソフトウエアRのインストール

R本体とRStudio Serverをインストールします．
これにより，WSL2上で動くRStudioにWindowsのWebブラウザでアクセスできます．

RStudioは非常に便利なRのフロントエンドですが，
Windows上でRtoRStudioを動かすのは文字コードやライブラリのインストールなどで実行が難しくなることがあります．

Ubuntu上でRとRStudioサーバーを動かしてWindowsのWebブラウザからアクセスるることにより，上記の問題を解決しやすくなります．

- R本体のインストール

公式HPのインストール手順は以下になります．

[http://cran.rstudio.com/bin/linux/ubuntu/](http://cran.rstudio.com/bin/linux/ubuntu/)

公式HPのの手順では最新版のRをインストールできますが，
Ubuntuのリポジトリにあるものもそれほど古いものではありません．
ここではUbuntuリポジトリからのインストールを紹介します．

```
sudo apt install r-base
```

Rstudio Serverをインストールいます．
こちらは公式HPの手順に基づいています．

```
wget https://download2.rstudio.org/server/jammy/amd64/rstudio-server-2023.03.0-386-amd64.deb
sudo apt install ./rstudio-server-2023.03.0-386-amd64.deb
```

### QGISのインストール

こちらも公式HPの手順になります．

必要なパッケージをインストールします．

```
sudo apt install gnupg software-properties-common
```

署名キーをインストールします．

```
sudo wget -O /etc/apt/keyrings/qgis-archive-keyring.gpg https://download.qgis.org/downloads/qgis-archive-keyring.gpg
```

QGISリポジトリを追加します．
テキストエディタ`nano`でリポジトリ情報のファイルを開きます．
```
sudo nano /etc/apt/sources.list.d/qgis.sources
```

開いたファイルに以下の内容を貼り付けて保存します．

```
Types: deb deb-src
URIs: https://qgis.org/debian
Suites: jammy
Architectures: amd64
Components: main
Signed-By: /etc/apt/keyrings/qgis-archive-keyring.gpg
```

リポジトリ情報をアップデートします．
```
sudo apt update
```

QGISをインストールします．

```
sudo apt install qgis
```

SAGAもインストールします．

```
sudo apt install saga
```

QGISを起動します．

```
qgis&
```

Pluginメニューから`Processing SAGA NextGen Provider`をインストールします．
これでQGISのプロセッシングメニューでSAGAが使えるようになります．