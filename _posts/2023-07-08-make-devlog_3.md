---
title: 따라 하다 보면 쉬운 Github Blog 만들기_3
date: 2023-07-08 12:50:00 +0900
lastmod: 2023-07-08 12:50:00 +0900
categories: [Blog, jekyll]
tags: [github.io, devlog, theme, repository, chirpy]
description: jekyll, github, 블로그, blog, 꾸미기, chirpy, 테마적용, gun1507
toc: true
toc_sticky: true
toc_label: 목차
math: true
mermaid: true
---

> 세 번째 Step은 chirpy 테마를 적용할꺼에요😃\
> chirpy 테마가 깔끔해서 선택했지만 다른 테마를 적용하셔도 무방합니다.

<br>

<h2> chirpy 테마 다운로드 </h2>
---
chirpy 테마가 아닌 다른 테마를 선택하고 싶다면 [jekyllthemes.org](http://jekyllthemes.org) 에서 선택해주세요.\
chirpy 테마를 다운받기 위해서 [jekyll-theme-chirpy](https://github.com/cotes2020/jekyll-theme-chirpy) 에서 소스를 다운받겠습니다.

![jekyll-theme-chirpy](/assets/img/jekyll-theme-chirpy.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;" }

<br>

테마 적용을 위해서 다운받은 소스는 이전 강의에서 clone했던 root 디렉토리에 복사+붙여넣기를 하겠습니다.\
저의 경우 ~/Workspace/gun1507-test.github.io 입니다.\
이름이 겹치는 파일들은 모두 덮어쓰기(대치) 하겠습니다.

![theme-source-download](/assets/img/theme-source-download.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;" }

<br>

<h2> 로컬 환경에서 확인하기 </h2>
---
적용한 chirpy 테마를 로컬에서 제대로 뜨는지 확인해보겠습니다.
```bash
bundle exec jekyll serve
```

<br>

```bash
 Incremental build: disabled. Enable with --incremental
      Generating... 
          Conflict: The following destination is shared by multiple files.
                    The written file may end up with unexpected contents.
                    /Users/Workspace/gun1507-test.github.io/_site/404.html
                     - assets/404.html
                     - 404.html
                    
          Conflict: The following destination is shared by multiple files.
                    The written file may end up with unexpected contents.
                    /Users/Workspace/gun1507-test.github.io/_site/about/index.html
                     - about.markdown
                     - /Users/Workspace/gun1507-test.github.io/_tabs/about.md
                    
          Conflict: The following destination is shared by multiple files.
                    The written file may end up with unexpected contents.
                    /Users/Workspace/gun1507-test.github.io/_site/index.html
                     - index.html
                     - index.markdown
                    
                    done in 0.769 seconds.
```
> 로컬에서 정상적으로 뜨긴 했지만, 위와 같은 오류가 발생했습니다.\
> 이름이 같은 파일이 있어 충돌이 났기 때문에 파일 삭제를 하겠습니다.

<br>

```bash
rm -f 404.html
rm -f about.markdown
rm -f index.markdown
```

<br>

```bash
Configuration file: /Workspace/gun1507-test.github.io/_config.yml
 Theme Config file: /Workspace/gun1507-test.github.io/_config.yml
            Source: /Workspace/gun1507-test.github.io
       Destination: /Workspace/gun1507-test.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
                    done in 0.523 seconds.
 Auto-regeneration: enabled for '/Workspace/gun1507-test.github.io'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.

```
> 정상적으로 로컬에 나온걸 알 수 있습니다.

<br>

![local-chirpy-theme](/assets/img/local-chirpy-theme.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;" }

<h2> 배포하기 </h2>
---
로컬에서는 정상 확인했지만 꼭 배포를 하면 오류가 났습니다.\
배포하기 전에 _config.yml 파일을 수정하겠습니다.
```yml
lang: en -> ko

timezone: Asia/Shanghai -> Asia/Seoul

title: Chirpy -> gun1507-test Blog

tagline: A text-focused Jekyll theme  -> chirpy 테마 테스트 블로그 입니다.

url: "" -> 'https://gun1507-test.github.io'

github:
  username: github_username -> gun1507-test
```
> _config.yml 파일 수정 후에 add,commit,push를 진행합니다.

<br>

<h2> 🔥만났던 오류🔥 </h2>
---
<h3> deploy 과정에서의 오류 </h3>

tools/deploy.sh 파일이 없다는 오류가 나타났습니다.
```bash
bash: tools/deploy.sh: No such file or directory
Error: Process completed with exit code 127.
```

<br>

tools/deploy.sh 가 없기 때문에 제 [저장소](https://github.com/gun1507/gun1507.github.io/tree/main)에서 다운로드 한 이후 복붙 해주세요!\
tools 전체를 복사 붙여넣기 하겠습니다.

<h3> deploy 과정에서의 권한 오류 </h3>

build 과정에서 `fatal: unable to access 'https://github.com/gun1507-test/gun1507-test.github.io/': The requested URL returned error: 403` 오류가 나타났습니다.

![github-actions-405](/assets/img/github-actions-403.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;" }

Actions의 권한 문제라고 생각이 들어 github 접속 후 Actions Settings를 확인했습니다.

<br>

![github-workflow-permission](/assets/img/github-workflow-permission.png){:style="border:1px solid #eaeaea; border-radius: 7px; padding: 0px;" }
> repository -> settings -> Actions -> Workflow Permissions -> Read and write permissions
> 읽기와 쓰기 모두 가능하도록 변경합니다.