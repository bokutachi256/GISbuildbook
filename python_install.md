# Pythonのインストール

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
