---
title: dockerに触ってみよう（非公開）
date: "2021-09-23T16:12:37.121Z"
---

### dockerって何？触ってみよう！
以下のさくらのナレッジに実際の手順が記載されていますので、これを見ながら実際に動かしてみるとよく分かります。
私は一回動かしただけでは覚えきれず理解できなかったので、「centOSにnginxをインストールして手順をDokerFileにする」とかしてコマンド類を覚えました。
[さくらのナレッジDoker入門](https://knowledge.sakura.ad.jp/13265/)

## 作ってみたdocker ファイル
まずcentOS-7にnginxをインストールする場合、yumリポジトリからインストールするために設定ファイルを追加する必要があります。
以下サイトを参考にさせて頂きました。
[Nginx を CentOS 7 にインストールする手順](https://weblabo.oscasierra.net/nginx-centos7-install/)
事前にテキストエディタで以下のnginx.repoを作成しておきます。DockerFileと同じ階層に以下ファイルを置いておきます。
```markdown
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/7/$basearch/
gpgcheck=0
enabled=1
```
そのファイルをdockerコンテナ内の
/etc/yum.repos.d/nginx.repo
として追加してあげる必要があるので、DockerFile内にその記述を記載します。

centos内に配置するのではなく、コンテナを個別に分けた方が良いのでは？
```markdown

```


### dockerコマンド
```markdown
 411  docker run -it -d -p 18080:8080 -v --name nginx centos:7
  412  docker ps -a
  413  pwd
  414  docker stop 83632206e391
  415  docker rm 83632206e391
  416  cd
  417  ll
  418  cd docker/
  419  ll
  420  docker run --help
  421  docker images
  422  docker run -it -d -p 18080:8080 -v --name centos:7
  423  docker ps -a
  424  docker stop a71a84136b63
  425  docker run -it -d -p 18090:80  --name  testContainer2 centos:7
  426  docker ps -a
  427  docker rm a71a84136b63
  428  history
  docker$ docker exec -it testContainer2 bash

```

docker内でsystemctlは使用できない
直接nginxやapacheの起動コマンドをたたいて起動するのが一般的
/usr/sbin/nginx

[参考：nginxの起動方法](https://www.server-memo.net/server-setting/nginx/nginx-command.html)

