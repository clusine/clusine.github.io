---
layout:     post
title:      "Github Pages - Jekyll Blog 설치"
subtitle:   "jekyll"
date:       2019-06-15
author:     "CiEL"
tags:
    - Github
    - jekyll
    - Blog
---

## 1. Github Repository 생성

_username_/_username_.github.io 로 생성한다.  
참고 : [https://pages.github.com/](https://pages.github.com/)

```bash
git clone https://github.com/username/username.github.io
cd username.github.io
echo "Hello World" > index.html
git add --all
git commit -m "Initial commit"
git push -u origin master
```

_username_.github.io 로 접속 (https 지원)

**repository 소유 계정으로 push 해야만 정상적으로 github-pages 로 deploy 된다**  
collaborator 로 push 하면 안됨

## 2. Jekyll 설치 - Mac OSX

git clone 경로에서

[https://jekyllrb-ko.github.io/docs/installation/](https://jekyllrb-ko.github.io/docs/installation/)

```bash
gem install bundler jekyll
bundle init
bundle add jekyll

# 충돌 방지를 위해 local 에 설치하길 권장
bundle install --path vendor/bundler
```

```bash
bundle exec jekyll serve
```

[http://localhost:4000](http://localhost:4000) 으로 접속 확인

## issue

-   gem install bundler 로 설치가 안될 경우

```bash
    /Library/Ruby/Site/2.0.0/rubygems/dependency.rb:308:in `to_specs': Could not find 'bundler' (>= 0) among 71 total gem(s) (Gem::MissingSpecError)
    Checked in 'GEM_PATH=/Users/username/.gem/ruby/2.0.0:/Library/Ruby/Gems/2.0.0:/System/Library/Frameworks/Ruby.framework/Versions/2.0/usr/lib/ruby/gems/2.0.0', execute `gem env` for more information
    from /Library/Ruby/Site/2.0.0/rubygems/dependency.rb:320:in `to_spec'
    from /Library/Ruby/Site/2.0.0/rubygems/core_ext/kernel_gem.rb:65:in `gem'
    from /usr/local/bin/bundle:22:in `<main>'
```

```bash
ERROR:  While executing gem ... (Errno::EPERM)
    Operation not permitted - /usr/bin/bundle
```

bundler 2.x 이하 버전 테마 설치했다가 bundler 를 삭제하고 0.0.1 이 설치되고 꼬이는 문제가 생길 때  
bundler 를 현재 user 에 설치하여 해결

```bash
sudo gem install -n /usr/local/bin bundler
```