# ホームディレクトリのマウントなど

- スタートメニューからUbuntuを起動する．
- WindowsホームディレクトリのシンボリックリンクをUbuntuに張る（ユーザ名の部分は自分のWindowsユーザー名に置き換えること）．
```
ln -s /mnt/c/Users/ユーザ名/Documents/ Documents
ln -s /mnt/c/Users/ユーザ名/Downloads/ Downloads
```

- インストール済みパッケージのアップデート（週に1回程度はアップデートをした方がよい．初回アップデートは時間がかかるかも）
```
sudo apt update && sudo apt upgrade -y
```

## 日本語入力システムのインストール
- 最低限の日本語フォントをインストールする
```
sudo apt install fonts-ricty-diminished
```
- mozc（日本語変換プログラム）のインストール
```
sudo apt install fcitx-mozc
fcitx
im-config -n fcitx
fcitx-config-gtk3
```
- .bashrcにfcitx周りの設定を書き込む
```
cat 'export GTK_IM_MODULE=fcitx' >> ~/.bashrc
cat 'export QT_IM_MODULE=fcitx' >> ~/.bashrc
cat 'export XMODIFIERS="@im=fcitx"' >> ~/.bashrc
cat 'export DefaultIMModule=fcitx' >> ~/.bashrc
cat 'fcitx-autostart > /dev/null 2>&1' >> ~/.bashrc
```

# 研究用アプリケーションのインストール

## Cコンパイラのインストール
- gccなどの開発環境をインストールする（C言語でプログラムを組まない人はインストールしなくてもよい）．
```

sudo apt update
sudo apt install build-essential
```

## Fortranコンパイラのインストール
- gfortran（Fortran 95コンパイラ）のインストール（Fortranでプログラムを組まない人はインストールしなくてもよい）

```
sudo apt update
sudo apt install gfortran
```

## 図化ソフトウエアのインストール
- GrADSのインストール（GrADSが何かわからない人はインストールする必要なし）

```
sudo apt update
sudo apt install grads
```

- GMTのインストール（GMTが何かわからない人はインストールする必要なし）
```
sudo apt update
sudo apt install gmt
```

## 統計解析ソフトウエアのインストール
- Rのインストール

```
sudo apt install r-base
```

## pythonのインストール

- Pythonのインストール（Ubuntu上で動くJupyter Labをインストールし，WindowsのWebブラウザからアクセスできるようにする）

### pyenvのインストール
```
	git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```
- .bashrcにpyenvの設定を書き込む
```
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
```


- .profileにpyenvの設定を書き込む
```
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
echo 'eval "$(pyenv init -)"' >> ~/.profile
```

- ターミナルを再起動する
```
exit
```
- スタートメニューからUbuntuを起動する
- pyenv updateのインストール
```
git clone https://github.com/pyenv/pyenv-update.git $(pyenv root)/plugins/pyenv-update
```
### pyenvでpythonをインストールする
- pyenv上でインストール可能なパッケージの一覧を取得する

```
pyenv install --list
```

- pyenvでインストール可能なPythonが表示されるので，miniforgeの最新バージョン（miniforge3-22.9.0-2）をインストールする.

```
pyenv install miniforge3-22.9.0-2
```

pyenvで切り替え可能なpythonパッケージのリストを確認する
```
pyenv versions
```

星印がついているのが現在のデフォルトのPython．たぶんsystem（最初から入っているPython）に星印がついているので，先ほどインストールしたminiforge3-4.10.3-10をデフォルトのPythonに変更する．このときシステム標準のPythonは変えずに，~/Documents以下のみにminiforgeを適用すように設定する

```
cd ~/Documents
pyenv local miniforge3-22.9.0-2
```

condaの環境変数をセットする．
```
conda init
```

ターミナルを再起動する．
```
exit
```

- スタートメニューからUbuntuを起動する
- condaパッケージのアップデート（週に一回くらいアップデートした方がよい）

```
conda update conda
conda update --all
```

- jupyterlabのインストール
```
conda install jupyterlab
```

- jupyterlabの起動
```
jupyter lab
```

Windowsのブラウザに上記アドレスを張り付けるとUbuntuで動いているJupyter Labにアクセスできる．

jupyterlabの終了はターミナルでCtrl+Cを2回押す．

### conda仮想環境の作成

- （例）mesaという名前の仮想環境を作成する
```
conda create -n mesa
```

- 作成した仮想環境に入る
```
conda activate mesa
```

- geopandasのインストール
```
conda install geopandas
```

### QGISのインストール
- 必要なパッケージのインストール

```
sudo apt install gnupg software-properties-common
```

- 署名キーのインストール（1行にペーストして実行）

```
sudo wget -O /etc/apt/keyrings/qgis-archive-keyring.gpg https://download.qgis.org/downloads/qgis-archive-keyring.gpg
```

リポジトリの追加
```
sudo nano /etc/apt/sources.list.d/qgis.sources
```
```
Types: deb deb-src
URIs: https://qgis.org/debian
Suites: jammy
Architectures: amd64
Components: main
Signed-By: /etc/apt/keyrings/qgis-archive-keyring.gpg
```

- リポジトリのアップデート
```
sudo apt update
```

- QGISのインストール

```
sudo apt install qgis
```

- SAGAのインストール
```
sudo apt install saga
```
