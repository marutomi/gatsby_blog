---
title: さくらVPS ubuntu　ファイヤーウォールの起動方法
date: "2021-09-23T16:12:37.121Z"
---

### さくらVPS ubuntu 初期状態のファイヤーウォールについて
マインクラフトのサーバーとしてさくらのスタートアップスクリプトを実行しましたが、ファイヤーウォールがデフォルトで起動していませんでした。最低限のセキュリティ対策を施す必要があるので、以下手順を示します。   

  
### ファイヤーウォールの状態確認と起動
[こちらのサイトが非常に参考になりますね。](https://freepc.jp/post-42705)
以下コマンドで状態を確認します。

```markdown
sudo ufw status
```

初期状態では
```markdown
Status: inactive
```
と表示されてしまいますので、以下コマンドでSSHのポートを開けてやります。マインクラフト用のサーバーの場合は、専用ポートも解放してあげます。
```markdown
sudo ufw allow 22
sudo ufw allow マインクラフト用のポート番号
```

で、起動
```markdown
sudo ufw enable
Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
Firewall is active and enabled on system startup
```

途中で「コマンド実行するとssh途切れるかもだけど良い？」という質問がくるのでyで先に進むとファイヤーウォールが有効になります。

確認で以下のような内容が出ればOK
```markdown
sudo ufw status
Status: active

To                         Action      From
--                         ------      ----
22                         ALLOW       Anywhere
22 (v6)                    ALLOW       Anywhere 
```

