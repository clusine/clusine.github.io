---
layout:     post
title:      "Github 복수 계정 SSH Key 설정"
subtitle:   "하나의 서버에서 SSH Key를 이용한 다수의 Github 계정 사용"
date:       2019-07-01
author:     "CiEL"
tags:
    - github
    - ssh
---

## 순서
1. ssh-keygen 을 이용해 각 계정에서 사용할 Key 생성
1. ~/.ssh/config 작성
1. git config 수정 또는 clone


## Key 생성

```bash
$ ssh-keygen -t rsa -C 'a@example.com'
```

id_rsa 말고 별도 이름으로 키를 생성한다.
```bash
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): id_rsa_a
```

동일한 방식으로 b@example.com 생성

```bash
$ ssh-keygen -t rsa -C 'b@example.com'
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): id_rsa_b
```

생성한 Key 추가 및 저장
```bash
$ ssh-add ~/.ssh/id_rsa_a
$ ssh-add ~/.ssh/id_rsa_b
$ ssh-add -l
```

~/.ssh/config 생성 및 수정
```bash
$ touch ~/.ssh/config

$ vi ~/.ssh/config

Host github.com-a
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_a

Host github.com-b
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_b
```

이전에 Repository를 Clone하여 사용 중인 경우, .git/config 를 수정
```bash
[remote "orgin"]
  url = git@github.com-a:a@example.com/{RepositoryName}.git
``` 
url 과 사용자 이름 부분을 주의하여 수정한다.

새로 Clone 하려는 경우, 위와 동일한 방식으로 url을 변경하여 Clone 한다.
```git
$ git clone git@github.com-b:b@example.com/{RepositoryName}.git
```
