# Pythonのインストール

---
[toc]
---


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
それとは別個に研究用のPythonをインストールします．
このときに研究用のPythonをpyenv経由でインストールすると，
研究用のPythonはpyenvの管理下に入ってシステム用のPythonと切り離されます．
これにより，システム用のPythonに影響を与えずに研究用Pythonを動かせます．

miniforgeはパッケージ管理システムにcondaを使うPythonです．
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

pyenv updateをインストールします．

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

## pyenvを使って研究用のPythonをインストールする

pyenv上でインストール可能なパッケージの一覧を取得します．

```
pyenv install --list
```

pyenvでインストール可能なPythonが表示されるので，
miniforgeの最新バージョン（miniforge3-22.9.0-2）をインストールします.

```
pyenv install miniforge3-22.9.0-2
```

インストールが終了したら，
pyenvで切り替え可能なPythonパッケージのリストを確認します．

```
pyenv versions
```

星印がついているのが現在のデフォルトのPython．おそらく`system`（最初から入っているPython）に星印がついているので，先ほどインストールしたminiforge3-22.9.0-2をデフォルトのPythonに変更します．
このときシステム標準のPythonは変えず，~/Documents以下のフォルダでPythonを実行したときにminiforgeのPythonが動くように設定します．

```
cd ~/Documents
pyenv local miniforge3-22.9.0-2
```

`cd`コマンドを使ってホームディレクトリ（`~`）の`Documents`フォルダに移動し，ホームディレクトリ以下でPythonを実行したときにminiforgeでインストールしたPythonを実行するようにします．そのためには`pyenv local`を使います．

次に`conda init`を使ってcondaの環境変数をセットします．
`conda init`は標準シェルを検出して設定を書き込みます．
Ubuntuの標準シェルはbash，Macの標準シェルzshです．
`conda init`はシェルの設定ファイルである.bashrcもしくは.zshrcに設定を書き込みます．

```
conda init
```

設定を反映させるためにターミナルを終了して再起動します．

```
exit
```

ターミナルが終了したら，Ubuntuの場合はスタートメニューからUbuntuを再度起動し，
Macの場合はユーティリティーからターミナルを起動してください．
これでpyenvでインストールしたminiforgeのPythonが実行できるようになります．
