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
echo 'export GTK_IM_MODULE=fcitx' >> ~/.bashrc
echo 'export QT_IM_MODULE=fcitx' >> ~/.bashrc
echo 'export XMODIFIERS="@im=fcitx"' >> ~/.bashrc
echo 'export DefaultIMModule=fcitx' >> ~/.bashrc
echo 'fcitx-autostart > /dev/null 2>&1' >> ~/.bashrc
```
