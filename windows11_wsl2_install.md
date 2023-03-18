- コントロールパネルを検索して実行する．
![picture 1](images/windows11_wsl2_install/20230319_085237.png)  
---

- プログラムを押す．
![picture 3](images/windows11_wsl2_install/20230319_085415.png)  
---

- Windowsの機能の有効化または無効化．
![picture 4](images/windows11_wsl2_install/20230319_085436.png)  
---

- 仮想マシンプラットフォームとLinux用Windowsサブシステムにチェックを入れる．
![picture 5](images/windows11_wsl2_install/20230319_085502.png)  
![picture 6](images/windows11_wsl2_install/20230319_085510.png)  
---

- PCを再起動する．
---

- スタートメニューを右クリックし，ターミナル（管理者）を起動する．
![picture 7](images/windows11_wsl2_install/20230319_085530.png)  
---

- プロンプトに以下のコマンドを入力する．
```wsl --set-default-version 2```
![picture 9](images/windows11_wsl2_install/20230319_085601.png)  
- 「この操作を正しく終了しました。」と表示されたら次に進む．
---

- プロンプトに以下のコマンドを入力する．
```wsl --update```
![picture 11](images/windows11_wsl2_install/20230319_085631.png)  
- 「Linux 用 Windows サブシステム はインストールされました。」と表示されたら次に進む．
---

- Microsoft Storeを開き，「ubuntu」を検索する．
- Ubuntu 22.04.1 LTSを開く．
![picture 13](images/windows11_wsl2_install/20230319_085658.png)  
---

- インストールボタンを押してUbuntu 22.04.1 LTSをインストールする．
![picture 14](images/windows11_wsl2_install/20230319_085714.png)  
---

- スタートメニューからUbuntu 22.04.1 LTSを起動する．
![picture 15](images/windows11_wsl2_install/20230319_085730.png)  
---

- ユーザー名の入力を求められるので，好きなユーザー名を入力する．ユーザー名は半角アルファベットを使うこと．スペースは使えない．このユーザー名がWSL2上のUbuntuの管理者ユーザー名（ログイン名）になる．
![picture 16](images/windows11_wsl2_install/20230319_085745.png)  
---

- パスワードを設定する．パスワードは自由だがこのパスワードはWSL2上のUbuntuの管理者ユーザーのパスワードになるため，Ubuntuシステムのアップデートや管理・アプリのインストール時に必要になる．忘れないようにすること．
- パスワードの確認のため，パスワードの入力が再度求められる．
- PCの再起動を求められたら指示に従ってPCを再起動する．
![picture 17](images/windows11_wsl2_install/20230319_085805.png)  
---

- 再起動後にスタートメニューからUbuntu 22.04.1 LTSを起動する．
- 再起動しなくても以下のようなメッセージが出たらWSL2とUbuntu22.04.1 LTSのインストールは完了．
![picture 18](images/windows11_wsl2_install/20230319_085825.png)  
