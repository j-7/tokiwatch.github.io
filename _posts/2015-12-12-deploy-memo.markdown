---
layout: post
title: "blogをデプロイするまでの作業手順"
date: 2015-12-12 08:56:50 +0900
comments: false
categories:
---

Octopressでghithub.comにブログを公開するまでの手順を以下にざっくりまとめます。
(主に自分用)

note: _username.github.ioは適宜変更_

1. githubに公開用のリポジトリを作る

1. Octopressをローカルに持ってくる

    ```
    git clone git@github.com:imathis/octopress.git username.github.io
    ```

1. bundlerで諸々インストール

    ```
    cd username.github.io
    gem install bundler
    bundle install --path vendor/bundle
    bundle exec rake setup_github_pages # あとは表示に従う
    ```

1. bitbucketのリポジトリを作ってとりあえずコミットする

    ```
    # bitbucketのサイトでリポジトリを作っておく
    git remote add origin git@bitbucket.org:username/username.github.io.git
    git add -A
    git commit -m"First Commit"
    git push -u origin master
    ```

1. 初期設定をする

    ```
    vim _config.yml
    ```

1. DNSを設定する
    - Aレコードの場合
        - https://help.github.com/articles/tips-for-configuring-a-cname-record-with-your-dns-provider/
    - CNAMEの場合
        - https://help.github.com/articles/about-custom-domains-for-github-pages-sites/#subdomains

1. 記事を書き、確認して、公開する

    ```
    rake new_post["Hello World!"]
    rake preview
    rake gen_deploy
    rake deploy
    ```

1. bitbucketにコミットする
