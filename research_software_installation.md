
# 研究用アプリケーションのインストール

---
[toc]
---

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
sudo apt install -y build-essential
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
sudo apt install -y gfortran
```

## GrADSとGMTのインストール
GrADSとGMTをインストールします．
GrADSやGMTが何かわからない人はインストールする必要はありません．

GrADSをインストールします．

```
# Ubuntu版
sudo apt update
sudo apt install -y grads
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
sudo apt install -y gmt
```

```
# Homebrew版
brew update
brew install gmt
```

## 統計解析ソフトウエアRのインストール

R本体とRStudioをインストールします．


### Rのインストール

#### Ubuntu版Rのインストール

Ubuntuのリポジトリに登録されているRは最新版のものではありませんが，
それほど古いものではないので実用上は問題ないでしょう．

一方，Rの公式HPに書かれている手順では最新版のRをインストールできます．
最新版のRをインストールしたい場合は公式HPの手順でRをインストールしてください．

まずはUbuntuリポジトリからのインストールについて説明します．
最新版のRをインストールしたい場合はこのステップを飛ばして次に進んでください．

リポジトリ情報をアップデートしてRをインストールします．

```
# Ubuntu版
sudo apt update
sudo apt install -y r-base
```

最新版のRをインストールしたい場合は以下のステップを実行します．
これは公式HPのインストール手順の要約です．
公式ページのインストール手順は以下になります．
[https://cran.r-project.org/](https://cran.r-project.org/)

まとめると以下になります．

リポジトリのアップデートをします．
```
sudo apt update -qq
```

必要なパッケージをインストールします．
```
sudo apt install -y --no-install-recommends software-properties-common dirmngr
```

PGPキーをインストールします．
```
wget -qO- https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc | sudo tee -a /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc
```

Rのリポジトリを設定します．
コマンドを実行した後にエンターキーを押します．

```
sudo add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/"
```

リポジトリの更新をします．

```
sudo apt update
```

Rをインストールします．

```
sudo apt install -y r-base
```

これでUbuntuへのRのインストールは終了です．

#### Homebrew版Rのインストール

公式HP (CRAN) の手順は[http://cran.rstudio.com/bin/macosx/](http://cran.rstudio.com/bin/macosx/)になりますが，
Homebrewでも最新のRをインストールできます．
Homebreでインストールした方がアップデートなどの管理がしやすくなるので，
ここではHomebrewからのインストールを紹介します．

リポジトリをアップデートしてRをインストールします．

```
# Homebrew版
brew update
brew install --cask r
```

パスワードの入力を求められたらログインパスワードを入力してください．
これでMacへのRのインストールは終了です．

### RStudioのインストール
#### Ubuntu版RStudioのインストール

まずは必要なライブラリのダウンロードとインストールを行います．

```
# Ubuntu版
wget http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2_amd64.deb
sudo apt install -y ./libssl1.1_1.1.1f-1ubuntu2_amd64.deb
```

次にRStudio本体のダウンロードとインストールを行います．

```
# Ubuntu版
wget https://download1.rstudio.org/electron/bionic/amd64/rstudio-2023.03.1-446-amd64.deb
sudo apt install -y ./rstudio-2023.03.1-446-amd64.deb
```

#### Homebrew版RStudioのインストール

Homebrewのリポジトリからインストールできます．

```
# Homebrew版
brew update
brew install rstudio
```

## QGISのインストール
### Ubuntu版QGISのインストール

公式HP（[https://qgis.org/ja/site/forusers/alldownloads.html#debian-ubuntu](https://qgis.org/ja/site/forusers/alldownloads.html#debian-ubuntu)）の要約です．

まず必要なパッケージをインストールします．

```
# Ubuntu版
sudo apt install -y gnupg software-properties-common
```

署名キーをインストールします．

```
# Ubuntu版
sudo wget -O /etc/apt/keyrings/qgis-archive-keyring.gpg https://download.qgis.org/downloads/qgis-archive-keyring.gpg
```

QGISリポジトリを追加します．

```
# Ubuntu版
sudo cat << 'EOS' | sudo tee /etc/apt/sources.list.d/qgis.sources
Types: deb deb-src
URIs: https://qgis.org/debian
Suites: jammy
Architectures: amd64
Components: main
Signed-By: /etc/apt/keyrings/qgis-archive-keyring.gpg
EOS
```

リポジトリ情報をアップデートします．
```
# Ubuntu版
sudo apt update
```

QGISをインストールします．

```
# Ubuntu版
sudo apt install -y qgis
```

SAGAもインストールします．

```
# Ubuntu版
sudo apt install -y saga
```

確認のためQGISを起動します．

```
# Ubuntu版
qgis &
```

Pluginメニューから`Processing SAGA NextGen Provider`をインストールします．
これでQGISのプロセッシングメニューでSAGAが使えるようになります．

### Homebrew版QGISのインストール

Homebrewのリポジトリに最新バージョンがありますのでそれをインストールします．

```
# Homebrew版
brew update
brew install qgis
```

Pluginメニューから`Processing SAGA NextGen Provider`をインストールします．
これでQGISのプロセッシングメニューでSAGAが使えるようになります．