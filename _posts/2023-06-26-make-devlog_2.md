---
title: 따라 하다 보면 쉬운 Github Blog 만들기_2
date: 2023-06-26 21:36:00 +0900
lastmod: 2023-06-26 21:36:00 +0900
categories: [Blog, jekyll]
tags: [github.io, devlog, theme, repository, chirpy]
description: jekyll, github, 블로그, blog, 꾸미기, chirpy, 테마적용, gun1507
toc: true
toc_sticky: true
toc_label: 목차
math: true
mermaid: true
---

> 두 번째 Step은 로컬에 Jekyll을 띄우고 원격에 push까지 할꺼에요😃\
> 설치 순서는 순서는 **rbenv > ruby > jekyll** 입니다.

<br>

<h2> 1. Ruby 설치 </h2>
---
ruby를 설치하기 전에 rbenv먼저 설치하겠습니다.\
rbenv는 루비 버전을 관리할 수 있는 툴입니다.
```bash
brew install rbenv
```

<br>

설치 가능한 버전을 확인해보겠습니다.
저의 경우에는 3.2.2 버전을 다운받을 수 있어 3.2.2 버전을 다운받겠습니다.
```bash
rbenv install -l

3.0.6
3.1.4
3.2.2
jruby-9.4.3.0
mruby-3.2.0
picoruby-3.0.0
truffleruby-23.0.0
truffleruby+graalvm-23.0.0

rbenv install 3.2.2
```
> Jekyll은 Ruby를 통해 개발된 사이트 생성기입니다.
> 따라서 Jekyll을 설치하기 전 Ruby를 먼저 설치합니다.

<br>

루비 버전은 3.2.2로 설정하고 현재 버전을 확인해보겠습니다.
```bash
rbenv global 3.2.2

rbenv versions
  system
  2.6.9
  2.7.0
  2.7.2
* 3.2.2
```

<br>

본인이 어떤 Shell을 사용하는지 확인하기 위해 아래 명령어를 입력합니다.
```bash
echo $SHELL

/bin/zsh
```

<br>

본인이 이용하는 shell에 따라서 아래 명령어를 통해 환경변수 세팅을 합니다.
```bash
# zsh의 경우
echo 'eval "$(rbenv init -)"' >> ~/.zshrc

# bash의 경우
echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
```

<br>

<h2> 2. bundler 설치 및 index.html 삭제</h2>
---
ruby에서 사용하는 패키지인 Gem의 의존성관리를 위한 의존성 관리 도구인 bundler를 설치합니다.
```bash
gem install bundler
```

<br>

[이전 강의](https://gun1507.github.io/posts/make-devlog_1/)에서 만들었던 index.html을 삭제합니다.
```bash
rm -f index.html
```

<br>

<h2> 3. Jekyll 설치 </h2>
---
[jekyll](https://ko.wikipedia.org/wiki/%EC%A7%80%ED%82%AC_(%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4)#%EC%97%AD%EC%82%AC)은 정적인 사이트 생성기라고 합니다.\
정말 신기하게도 깃허브의 공동 설립자 톰 프레스턴 워너에 의해 개발되었습니다.
```bash
gem install jekyll
```

<br>

jekyll 기본 블로그를 설치합니다.
```bash
# jekyll new {소스 root 디렉토리}
jekyll new ./
```
> 반드시 clone한 소스의 root 디렉토리에서 위 명령어를 입력해야 합니다.\
> 저의 경우 ~/Workspace/gun1507-test.github.io 가 되겠네요.

<br>

`ll`을 통해 확인해 보면 기본 파일들이 있습니다.
```bash
ll

404.html
Gemfile
Gemfile.lock
README.md
_config.yml
_posts
about.markdown
index.markdown
```

<br>

<h2> 4. 원격 저장소 push </h2>
---
git add, commit, push를 진행합니다.
```bash
git add .
git commit -m "add - jekyll install"
git push origin main
```

<br>

<h2> 5. 블로그 접근 및 확인 </h2>
---
`{Owner}.github.io` 페이지 접속 후 index.html에 작성한 내용이 표출되는지 확인합니다.
![jekyll-base-site](/assets/img/jekyll-base-site.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;" }

<br>

<h2> 🔥만났던 오류🔥 </h2>
---
<h3> 1. jekyll이 이미 존재하고 있는 경우 </h3>

`jekyll new ./`명령어 입력 시 오류가 나는 경우가 있습니다.\
이 경우에는 `jekyll new -f ./`명령어를 입력해주세요.
```bash
Conflict: /Users/Workspace/gun1507-test.github.io exists and is not empty.
Ensure /Users/Workspace/gun1507-test.github.io is empty or else try again with `--force` to proceed and overwrite any files.
```

<br>

<h3> 2. push 이후 githug-pages 에서 Gemfile 의존성을 충족할 수 없는 경우 </h3>

build 과정에서 `Warning:  github-pages can't satisfy your Gemfile's dependencies.` 오류가 나타났습니다.
![깃헙 gemfile 오류](/assets/img/github-gemfile-error.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;" }

github docs에서 [내용](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-from-a-branch)을 확인할 수 있었습니다.

<br>

<h4> 1) 게시 소스로 사용하려는 분기가 저장소에 이미 있는지 확인하십시오. </h4>

<h4> 2) GitHub에서 사이트의 리포지토리로 이동합니다. </h4>

<h4> 3) 리포지토리 이름 아래에서 Settings 을 클릭합니다. Settings 탭이 보이지 않으면 드롭다운 메뉴를 선택한 다음 설정을 클릭합니다. </h4>
![깃헙 셋팅](/assets/img/github-settings.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;" }

<h4> 4) 사이드바의 "Code and automation" 섹션에서 Pages 를 클릭합니다. </h4>

이후에 Jekyll Configure을 진행합니다.
![github-jekyll-configure](/assets/img/github-jekyll-configure.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;" }

workflows를 만들 수 있는데 Workflow란 Actions의 상위 개념으로 작업흐름 자동화 과정입니다.
![깃헙 워크플로우](/assets/img/github-pages-deploy.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;" }\
아래 내용대로 입력해주세요.
```yml
name: 'Automatic build'
on:
  push:
    branches:
      - main
    paths-ignore:
      - .gitignore
      - README.md
      - LICENSE

jobs:
  continuous-delivery:

    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v2
        with:
          fetch-depth: 0  # for posts's lastmod

      - name: Setup Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: 2.7
          bundler-cache: true

      - name: Deploy
        run: bash tools/deploy.sh
```
> 복사, 붙여넣기 후 오른쪽 위 Commit changes 를 진행합니다.

<br>

<h3> 3. github Actions에서 Setup Ruby 과정 중 오류 발생한 경우 </h3>

workfolw 내용을 만든 뒤 push를 진행했지만 `Error: The process '/opt/hostedtoolcache/Ruby/2.7.8/x64/bin/bundle' failed with exit code`라는 오류가 발생했습니다.
![github-setup-ruby-error](/assets/img/github-setup-ruby-error.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;" }

<br>

원격 저장소에서 직접 Gemfile.lock 을 삭제 후 로컬에 pull을 진행하겠습니다.
![github-delete-file](/assets/img/github-delete-file.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;" }
```bash
git fetch
git pull origin main
```

<br>

Gemfile.lock에 x86_64-linux 플랫폼이 없기 때문에 추가하도록 하겠습니다.
```bash
bundle lock --add-platform x86_64-linux
```

<br>

🚨이제 다시 push를 하기 전 꼭 `.gitignore` 파일을 수정합니다.
```
# hidden files
.*
!.git*
!.editorconfig
!.nojekyll
!.travis.yml

# bundler cache
_site
vendor

# rubygem
*.gem

# npm dependencies
node_modules
package-lock.json
Gemfile.lock
```

<br>

<h3> 4. deploy 과정에서의 오류 </h3>

다시 한번 push를 진행했지만 `Error: Process completed with exit code`라는 오류가 발생했습니다.

![github-deploy-error](/assets/img/github-deploy-error.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;" }

<br>

tools/deploy.sh 가 없기 때문에 제 [저장소](https://github.com/gun1507/gun1507.github.io/tree/main)에서 다운로드 한 이후 복붙 해주세요!
tools 전체를 복붙 하고 push 하겠습니다.

<h3> 5. Sass 버전 문제로 인한 '/' 함수 오류 </h3>

로컬에서 테스트 하기 위해 `bundle install`을 다시한번 진행하고 아래 명령어를 통해 로컬에서 실행시켰습니다.
하지만 '/' 나누기 함수를 실행할 수 없다고 합니다. 버전 문제인듯 해요.
```bash
bundle exec jekyll serve

Deprecation Warning: Using / for division outside of calc() is deprecated and will be removed in Dart Sass 2.0.0.
...
```

<br>

수많은 해결 방법이 있겠지만 저는 '/' 를 사용하지 않기로 했습니다.
scss 파일의 '/'를 전부 '* 0.5' 으로 변경합니다.
```bash
npm install -g sass-migrator
sass-migrator division **/*.scss
```
