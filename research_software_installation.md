
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

```
sudo echo 'Types: deb deb-src' >> /etc/apt/sources.list.d/qgis.sources
sudo echo 'URIs: https://qgis.org/debian' >> /etc/apt/sources.list.d/qgis.sources
sudo echo 'Suites: jammy' >> /etc/apt/sources.list.d/qgis.sources
sudo echo 'Architectures: amd64' >> /etc/apt/sources.list.d/qgis.sources
sudo echo 'Components: main' >> /etc/apt/sources.list.d/qgis.sources
sudo echo 'Signed-By: /etc/apt/keyrings/qgis-archive-keyring.gpg' >> /etc/apt/sources.list.d/qgis.sources
```

もしくはテキストエディタ`nano`などで`/etc/apt/sources.list.d/qgis.sources`を開き，
以下の内容を貼り付けても構いません．

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

確認のためQGISを起動します．

```
qgis &
```

Pluginメニューから`Processing SAGA NextGen Provider`をインストールします．
これでQGISのプロセッシングメニューでSAGAが使えるようになります．