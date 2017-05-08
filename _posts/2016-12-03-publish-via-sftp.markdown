---
layout: post
title: "Octopressでサイトをsftpで公開"
date: 2016-12-03 22:01:55 +0900
comments: false
categories:
published: true
---

このblogをgithub pagesからレンタルサーバに移行したので、手順を下記にまとめておく

<!-- more -->

Rakefileに以下を記入

```
## --  SFTP Configs -- ##

lftp_command = "lftpコマンドの絶対パス"
lftp_method = "sftp"
lftp_user = "ユーザ名"
lftp_target = "アップロードしたいサーバ"
upload_dir = "blogのコンテンツを格納するディレクトリ"
deploy_default = "lftp"

desc "Deploy website via LFTP"
task :lftp do
        puts "## Deploying website via LFTP"
        lftp_command_str = "#{lftp_command} -c '" + "open #{lftp_method}://#{lftp_user}@#{lftp_target}; lcd #{public_dir}; cd #{upload_dir}; mirror -R --only-newer . ;" + "'"
        ok_failed system(lftp_command_str)
end
```



解説

- sftpだとログインした後にディレクトリを移動したりするのが面倒なので、lftpを使う
- コマンドに食わせるオプションを文字列で作って、system関数で処理
- rake deployする際、SSH鍵にパスフレーズを設定している場合は、パスフレーズが聞かれるので都度入力する
- 例えば、sftpではなく、ftpにしたい場合などは、lftpのブックマークにしておくなどすれば便利かもしれない

