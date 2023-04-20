# Pythonのインストール

Pythonは人気があって比較的手軽にプログラミングができる言語ですが，
必要なモジュールをどんどん追加していくとモジュール同士の衝突が起きて最悪の場合動かなくなってしまいます．

またPythonはOSXやUbuntuなどに最初からインストールされていますが，
これはシステム用に使われることを想定しているため，
研究用途のモジュールなどを追加して「汚して」しまうのはあまり得策とは言えません．

このため，研究用に別途Pythonを用意し，システム用と切り離して運用するのが良いでしょう．
いろいろな考え方がありますが，研究・科学計算用のPythonとしてはAnacondaが有名です．
Anacondaはcondaというパッケージ管理システムを使っており，
多数の科学技術計算用のモジュールが用意されています．
その一方でかなり大規模なシステムであること，
使用目的によっては無償で使えないなどの制限があるなどというデメリットもあります．

またこれはPythonに限りませんが，もし何らかの原因でソフトウエアやプログラム環境が動かなくなってしまった場合に，
他の部分に影響を及ばさずに再インストールできることはとても重要です．

Pythonでは仮想環境を使うことにより，
周囲に影響を及ぼさないプログラミング環境を作成することができます．
もしあるプログラミング環境の調子が悪くなってしまっても，
その仮想環境を削除して作成し直すことにより，
他のプログラミング環境に影響を与えずに復旧することができます．

これらのことを考えて，本章では以下のようなPython環境を構築します．

- pyenvを用いて研究用のPythonをインストールする．
- 研究用のPythonとしてminiforgeをインストールする．
- miniforgeのcondaを使って，用途ごとにPython仮想環境を作成する
- 各Python環境にはJupyterをインストールしてブラウザを用いてプログラミングができるようにする．

pyenvは複数のPythonを切り替える事ができるシステムです．
ここでは最初からインストールされているシステム用のPythonをそのまま残し，
それとは別個に研究用のpythonをインストールします．
このときに研究用のpythonをpyenv経由でインストールすると，
研究用のpythonはpyenvの管理下に入ってシステム用のpythonと切り離されます．
これにより，システム用のpythonに影響を与えずに研究用pythonを動かせます．

miniforgeはパッケージ管理システムにcondaを使うpythonです．
Anacondaは用途によっては有償になってしまいますが，
minicondaは無償で使用できます．
また，Anacondaは巨大なシステムなのですが，
miniforgeはミニマムなAnacondaという位置づけで非常に軽量です．
軽量であっても必要なものは必要なときにインストールすれば良いので
特に困るようなことはありません．

condaはPythonの仮想環境の作成・管理・削除，モジュールのインストールなど非常に多岐な役割を持つコマンドです．
ここではcondaを使ってPython仮想環境を作成していきます．

## pyenvのインストール

複数のPythonを切り替えるコマンドであるpyenvをインストールします．

### Ubuntu版のインストール方法

pyenv公式ページの手順の要約です．
まずgitを使ってpyenvをインストールします．

```
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

.bashrcにpyenvの設定を書き込みます．

```
cat << 'EOS' | tee -a ~/.bashrc

# pyenv
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
EOS
```


.profileにもpyenvの設定を書き込みます．

```
cat << 'EOS' | tee -a ~/.profile

# pyenv
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
EOS
```

exitコマンドでターミナルを終了します．

```
exit
```

ターミナルを終了したらスタートメニューからUbuntuを再度起動してください．

`pyenv update`をインストールします．

```
git clone https://github.com/pyenv/pyenv-update.git $(pyenv root)/plugins/pyenv-update
```

以上でUbuntuにpyenvがインストールされました．

### Homebrew版のインストール方法

Homebrewを使ってpyenvをインストールします．

```
brew install pyenv
```

.zshrcにpyenvの設定を書き込みます．

```
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zshrc
```

書き込んだ設定を有効にします．

```
source ~/.zshrc
```

以上でMacへのpyenvインストールが完了しました．

## pyenvを使って研究用のpythonをインストールする

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

## conda仮想環境の作成

マルチエージェントシミュレーションを実行するための仮想環境`mesa`を作成します．
この環境にインストールするパッケージは以下になります．

- mesa
- jupyterlab
- geopandas
- gdal
- matplotlib
- ffmpeg

まずは`mesa`という名前の仮想環境を作成します．

```
conda create -n mesa
```

作成した仮想環境をアクティベート（有効化）します．
```
conda activate mesa
```

パッケージ`mesa`をインストールする
```
conda install mesa
```

condaが`mesa`に必要なパッケージを検索して自動的にインストールします．
あるパッケージをインストールするには他の必須パッケージがインストールされている必要があり，
それらのパッケージの依存関係を自動的に解決して最適なパッケージをインストールします．

次に`jupyterlab`をインストールします．

```
conda install jupyterlab
```

`jupyterlab`も比較的大規模なパッケージであるため，必須パッケージも多数あります．
`jupyterlab`の必須パッケージとmesaの必須パッケージには共通のがありますが，
condaはコンフリクトするパッケージのバージョン管理なども自動でやってくれます．

以下のようにすればcondaで複数のパッケージを同時にインストールすることも可能ですが，
インストールするパッケージが多くなると依存関係の解決に時間がかかります．

複数パッケージをインストールしようとしても依存関係が解決できずにエラーが出る場合は，
パッケージを一つずつインストールしてみてください．

残りのライブラリもインストールしましょう．

```
conda install geopandas gdal matplotlib ffmpeg
```
