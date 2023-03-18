- コントロールパネルを検索して実行する．

ScreenClip.png








![picture 1](images/59e6afc93342de82477fd5b6b1377319de9a596d3995d1ab3857ba0f2eeada56.png)  
---

- プログラムを押す．
![picture 2](images/61646a2e6a12cee7d5442f17d45a5d4c9ff320269495c6ec3cffe42737d61ef9.png)  
---

- Windowsの機能の有効化または無効化．
![picture 3](images/13145ba51ad22c546d064c0bab3306580025022d5a6b04672a1f45e8aad7a80f.png)  
---

- 仮想マシンプラットフォームとLinux用Windowsサブシステムにチェックを入れる．
![picture 4](images/68c7c41a0bb9dc0850e92d41626c58a6f084f2958662c1706de9bab13d8b102d.png)  
![picture 5](images/4fbc031794ba204dc87f4752441aac801c93f30278b636ccb3040f9c8d297f01.png)  
---

- PCを再起動する．
---

- スタートメニューを右クリックし，ターミナル（管理者）を起動する．
![picture 6](images/8881aa9cd27b3c3ea99458c46ced90de322251abf5aac7beed34a43da8b4a5af.png)  
---

- プロンプトに以下のコマンドを入力する．
```wsl --set-default-version 2```
![picture 7](images/92cacfb1939385c9ce8276be47c7ba9f8f0f06ebd6fe5b8abe71d5692967d48a.png)  
- 「この操作を正しく終了しました。」と表示されたら次に進む．
---

- プロンプトに以下のコマンドを入力する．
```wsl --update```
![picture 8](images/884ba811e515485aad731b8c173fe7de67d8b676e4a80442524679192db57da5.png)  
- 「Linux 用 Windows サブシステム はインストールされました。」と表示されたら次に進む．
---

- Microsoft Storeを開き，「ubuntu」を検索する．
- Ubuntu 22.04.1 LTSを開く．
![picture 10](images/2fd7e4326563ca1f86b149ff5ebe4ecc9b7fe8b8a482c8b718fc705dda09a689.png)  
---

- インストールボタンを押してUbuntu 22.04.1 LTSをインストールする．
![picture 11](images/f14ce2a523e869f21eadc72f27a50a5f535de771cef3845cf093efb04f7d2b37.png)  
---

- スタートメニューからUbuntu 22.04.1 LTSを起動する．
![picture 12](images/c2a2c16ec277f83061f578cd0994329745533b129043c44b3303b5b7a0834c53.png)  
---

- ユーザー名の入力を求められるので，好きなユーザー名を入力する．ユーザー名は半角アルファベットを使うこと．スペースは使えない．このユーザー名がWSL2上のUbuntuの管理者ユーザー名（ログイン名）になる．
![picture 13](images/1146904422a3295f357064a15d8266204aaddd5bfde685777f8568ac34817d69.png)  
---

- パスワードを設定する．パスワードは自由だがこのパスワードはWSL2上のUbuntuの管理者ユーザーのパスワードになるため，Ubuntuシステムのアップデートや管理・アプリのインストール時に必要になる．忘れないようにすること．
- パスワードの確認のため，パスワードの入力が再度求められる．
- PCの再起動を求められたら指示に従ってPCを再起動する．
![picture 14](images/894a6c71c0a9c59fabd0e79a3d8f7a2762db1d7b9ec22cfb6585a05df5452b46.png)  
---

- 再起動後にスタートメニューからUbuntu 22.04.1 LTSを起動する．
- 再起動しなくても以下のようなメッセージが出たらWSL2とUbuntu22.04.1 LTSのインストールは完了．
![picture 15](images/42e6affe817c2dd44914cf2931ca3e0e42963f5ab18a05c8e39532856168fc7d.png)  


![picture 19](images/%24%7Bmdname%7D/20230317_222409.jpg)  


![picture 20](images/windiws11_wsl2_install/20230317_222613.jpg)  
