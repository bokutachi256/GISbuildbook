
# 研究用アプリケーションのインストール

## Cコンパイラのインストール

gccなどのC言語開発環境をインストールします．
Cプログラムのコンパイルをしない方はインストールする必要はありません．

Ubuntuの場合はgccを含む開発ツールをインストールする必要がありますが，
Homebrewはすでにコマンドラインツールとxcodeがインストールされているので，
すぐにCコンパイラ（gccやclangなど）が使えます．
ただし，Macでgfortranを使う際にはHomebrewでgccをインストールする必要があります．

```
# Ubuntu版
sudo apt update
sudo apt install build-essential
```

```
# Homebrew版
brew update
brew install gcc
```

## Fortranコンパイラのインストール

Fortran95コンパイラ（gfortran）をインストールします．
Fortranプログラムのコンパイルをしない方はインストールする必要はありません．
Homebrewはgccにgfortranが含まれているので，上記のCコンパイラのインストールを行えばgfortranもインストールされます．

```
# Ubuntu版
sudo apt update
sudo apt install gfortran
```

## GrADSとGMTのインストール
GrADSとGMTをインストールします．
GrADSやGMTが何かわからない人はインストールする必要はありません．

GrADSをインストールします．

```
# Ubuntu版
sudo apt update
sudo apt install grads
```

```
# Homebrew版
brew update
brew install grads
```

GMTをインストールします．

```
# Ubuntu版
sudo apt update
sudo apt install gmt
```

```
# Homebrew版
brew update
brew install gmt
```

## 統計解析ソフトウエアRのインストール

R本体とRStudioをインストールします．


### Rのインストール

#### Ubuntu版のインストール

公式HPのインストール手順は以下になります．

[http://cran.rstudio.com/bin/linux/ubuntu/](http://cran.rstudio.com/bin/linux/ubuntu/)

公式HPの手順では最新版のRをインストールできますが，
Ubuntuのリポジトリにあるものもそれほど古いものではありません．
ここではUbuntuリポジトリからのインストールを紹介します．

```
# Ubuntu版
sudo apt update
sudo apt install r-base
```

#### Mac版のインストール

公式HPの手順は[http://cran.rstudio.com/bin/macosx/](http://cran.rstudio.com/bin/macosx/)になりますが，
Homebrewでインストールした方がアップデートなどの管理がしやすくなります．
ここではHomebrewからのインストールを紹介します．

```
# Homebrew版
brew update
brew install --cask r
```

パスワードの入力を求められたらログインパスワードを入力してください．

### RStudioのインストール
#### Ubuntu版のインストール

RStudioは非常に便利なRのフロントエンドですが，
Windows上でRとRStudioを動かすのは文字コードやライブラリのインストールなどで実行が難しくなることがあります．

Ubuntu上でRとRStudioサーバーを動かしてWindowsのWebブラウザからアクセスすることにより，上記の問題を解決しやすくなります．

UbuntuにRstudio Serverをインストールします．
こちらは公式HPの手順（[https://posit.co/download/rstudio-server/](https://posit.co/download/rstudio-server/)）に基づいています．

```
# Ubuntu版
wget https://download2.rstudio.org/server/jammy/amd64/rstudio-server-2023.03.0-386-amd64.deb
sudo apt install ./rstudio-server-2023.03.0-386-amd64.deb
```


#### Homebrew版のインストール

Homebrewのリポジトリからインストールできます．

```
# Homebrew版
brew update
brew install rstudio
```


## QGISのインストール
### Ubuntu版のインストール

公式HP（[https://qgis.org/ja/site/forusers/alldownloads.html#debian-ubuntu](https://qgis.org/ja/site/forusers/alldownloads.html#debian-ubuntu)）の要約です．

まず必要なパッケージをインストールします．

```
# Ubuntu版
sudo apt install gnupg software-properties-common
```

署名キーをインストールします．

```
# Ubuntu版
sudo wget -O /etc/apt/keyrings/qgis-archive-keyring.gpg https://download.qgis.org/downloads/qgis-archive-keyring.gpg
```

QGISリポジトリを追加します．

```
# Ubuntu版
sudo echo 'Types: deb deb-src' >> /etc/apt/sources.list.d/qgis.sources
sudo echo 'URIs: https://qgis.org/debian' >> /etc/apt/sources.list.d/qgis.sources
sudo echo 'Suites: jammy' >> /etc/apt/sources.list.d/qgis.sources
sudo echo 'Architectures: amd64' >> /etc/apt/sources.list.d/qgis.sources
sudo echo 'Components: main' >> /etc/apt/sources.list.d/qgis.sources
sudo echo 'Signed-By: /etc/apt/keyrings/qgis-archive-keyring.gpg' >> /etc/apt/sources.list.d/qgis.sources
```

もしくはテキストエディタ`nano`などで`/etc/apt/sources.list.d/qgis.sources`を開き，
以下の内容を貼り付けて保存しても構いません．

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
# Ubuntu版
sudo apt update
```

QGISをインストールします．

```
# Ubuntu版
sudo apt install qgis
```

SAGAもインストールします．

```
# Ubuntu版
sudo apt install saga
```

確認のためQGISを起動します．

```
# Ubuntu版
qgis &
```

Pluginメニューから`Processing SAGA NextGen Provider`をインストールします．
これでQGISのプロセッシングメニューでSAGAが使えるようになります．

### Homebrew版のインストール

Homebrewのリポジトリに最新バージョンがありますのでそれをインストールします．

```
# Homebrew版
brew update
brew install qgis
```

Pluginメニューから`Processing SAGA NextGen Provider`をインストールします．
これでQGISのプロセッシングメニューでSAGAが使えるようになります．