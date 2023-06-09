# condaを用いたPython仮想環境の運用

---
[toc]
---

前章でpyenvを使ってPython環境が構築できました．
次はcondaを使ってPythonの仮想環境を作成します．

Pythonは様々なパッケージを使えるのが特徴ですが，
パッケージはお互いに依存関係（あるパッケージを使うには他のパッケージが必要になること）があり，
多数のパッケージを使おうとすると依存関係も複雑になります．
必要なペッケージをその都度インストールし，
アップデートを繰り返していくうちにパッケージの依存関係が解決できなくなり，
プログラムが実行できなくなることもあります．

このような事態を避けるためにもインストールするパッケージはなるべく少なくしたいところですが，
実際には様々なプログラムを実行しなくてはならないのでそう簡単には行きません．

Pythonの仮想環境はこの問題を解決してくれます．
Python仮想環境は切替可能な複数のPythonを作り，
それぞれに別々のパッケージをインストールできます．

このため，プログラムAは仮想環境Aで動かし，プログラムBは仮想環境Bで動かすことが可能です．
それぞれの仮想環境にはそこで動かすプログラムに必要なパッケージのみをインストールすれば良いので，
不要なパッケージが増えることによる依存関係の複雑化を避けることができます．

このPython仮想環境の構築・管理・削除を行うのがcondaコマンドです．

## 現在インストールされているconda仮想環境の確認とパッケージのアップデート

前章でインストールしたPythonであるminiforgeにはcondaコマンドが用意されており，
condaコマンドを使ってPython仮想環境の構築・管理・削除やパッケージのインストールとアップデートができます．

miniforgeには基本となる仮想環境が用意されています．
現在の仮想環境のリストを見てみます．

```sh
conda info -e
```

現在のPython仮想環境の一覧が表示されます．
インストール直後はbaseという基本の仮想環境のみがあり，
このbaseがアクティブ（星印がついている）になっています．
したがって，この状態でPythonプログラムを走らせるとbase環境の中のPythonでプログラムが実行されます．

base環境はほぼ「素」のPythonですので，標準以外のパッケーはインストールされていません．
ですが，base環境にパッケージをあれこれ追加していくのはあまり得策とは言えません．
base環境はそのままの状態にしておいて，目的ごとに仮想環境を作成してそこでプログラムを実行したほうが良いでしょう．

仮想環境を作成するにあたってbase環境をアップデートします．
base環境にはcondaなどが含まれているので，1〜2週間に一度くらいはアップデートしたほうが良いでしょう．

base環境のアップデートは以下になります．

```sh
conda update -n base --all
```

アップデート可能なパッケージの検索に少し時間がかかりますが，
検索終了後にアップデートするかどうか聞かれますのでyを押してアップデートを行います．

## conda仮想環境の作成

マルチエージェントシミュレーションを実行するための仮想環境`mesa`を作成しましょう．
この環境にインストールするパッケージは以下になります．

- mesa
- jupyterlab
- geopandas
- gdal
- matplotlib
- ffmpeg

まずは`mesa`という名前の仮想環境を作成します．

```sh
conda create -n mesa
```

作成した仮想環境をアクティベート（有効化）します．

```sh
conda activate mesa
```

プロンプトの先頭が`mesa`に変わり，mesa環境に切り替わりました．この状態でPythonプログラムを実行すると，mesa仮想環境中のPythonが実行されます．

パッケージ`mesa`をインストールします．

```sh
conda install mesa
```

condaが`mesa`に必要なパッケージを検索して自動的にインストールします．
あるパッケージをインストールするには他のパッケージがインストールされている必要がある場合には，
condaが自動的に必要なパッケージをインストールしてくれます．

次に`jupyterlab`をインストールしてみましょう．

```sh
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

```sh
conda install geopandas gdal matplotlib ffmpeg
```

jupyterlabを起動します．

```sh
jupyter lab
```

実行するとメッセージがたくさん出てきますが，その中に下記のようなURLがあります（token以下は実行するたびに変わります）．

```sh
http://127.0.0.1:8888/lab?token=42220bdf357a0bef730bbf205a9710d34a3734ff557062cb
```

Windowsのブラウザに上記URLを張り付けるとUbuntuで動いているJupyter Labにアクセスできるようになり，
Pythonプログラムを実行できるようになります．

Jupyter Labを終了するには，
まずブラウザのJupyter LabのファイルメニューからShutdownを選びます．
もしくはターミナルでCtrl+Cを2回押します．
