---
layout: post
title: "SSHパスフレーズがKeychainに保存されなくなったら"
date: 2016-12-29 13:55:12 +0900
comments: false
categories: 
published: true
---

先日、MacOS10.12.2にアップデートしたところ、ターミナルで入力したSSHのパスフレーズがKeychainに保存されなくなった。

以下に解決方法手順を書いておく。

1. ~/.ssh/config を開く（なかったら作成する）
2. 以下を記述
```
IdentityFile ~/.ssh/id_rsa
AddKeysToAgent yes
```
以上
