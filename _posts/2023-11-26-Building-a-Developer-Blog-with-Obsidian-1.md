---
title: 옵시디언으로 개발 블로그 구축하기 - (1)
date: 2023-11-26 22:11:11 +09:00
tags: [Git, Blog]
image: obsidian_github_logo.png
media_subpath: images/images_231126/
---


## 들어가는 글

과거 21년 즈음 **github pages**를 이용하여 개인 블로그를 개설했었으나, index 에러로 인해 형체를 알아볼 수 없는 수준으로 방치해두었다. 나는 아쉽게도 FE, BE 지식이 전혀 없다. 때문에 21년에도 그리고 23년 지금도 github을 통해 블로그를 구축하는 과정이 꽤 어렵게 느껴졌다. 아마 FE, BE 개발자들은 누워서 껌먹기지 않을까 싶은데, 블로그를 구축하는 과정에서 해당 기술 외에도 개발자라면 꼭 알아야 할 정보들이 꽤 많은 것 같아서 이렇게 공유하고자 한다. 어떤 분야의 지식이든 최소한을 지닐 수 있다면, 매우 큰 도움이 된다고 생각한다. 책을 많이 읽어야 하는 이유가 또 생겨버렸다. 언젠간 책 리뷰 글을 꼭 올릴테야.

<!--more-->



내 글의 순서는 다음과 같다.

- Jekyll을 통해 Github.io 블로그 구축하기
- obsidian md로 손쉽게 블로그 내용 채우기
- obsidian git으로 **Github-Vault** 효율적으로 연동하기

옵시디언을 사용하지 않는 사람은 1목차만 봐도 무방하다. 나는 윈도우 유저이기 때문에, 윈도우 환경에서 발생한 트러블슈팅 과정을 모두 내포하고 있다. 내가 참고한 블로그는 대부분 Mac OS 환경을 가정하고 튜토리얼을 진행했다. 혹시나 내가 서술하지 않은 오류가 발생한다면 꼭 알려주길 바란다. 이미 해결한 오류일 수도 있다. 또, 해당 글은 Git의 사용수준을 중급자 이상으로 가정하고 작성한 것이므로 다소 불친절할 수도 있다. 따라서 뭔가 생략된 명령어가 있는 것 같거나 Git 관련 오류가 발생하는 경우 꼭 알려주길 바란다.

## Jekyll을 통해 Github.io 블로그 구축하기

>Jekyll 은 정적 사이트 생성기입니다. 당신이 즐겨 사용하는 마크업 언어로 작성된 텍스트를 Jekyll 에 넘겨주면 레이아웃을 사용해 정적 웹사이트를 생성합니다. 사이트 URL 의 형식이나 어떤 데이터를 사이트에 표시할 것인지 등, 여러 동작을 조정할 수 있습니다. [Jekyll 공식 한글 문서](https://jekyllrb-ko.github.io/docs/)
### JeKyll Fork하기

먼저 마음에 드는 Jekyll Thema를 고르면 된다. 나는 [심플하면서 어두운 색상의 테마](https://github.com/cotes2020/jekyll-theme-chirpy)를 골랐다. 또 문서의 목차 기능, 카테고리 기능, 태그 기능 등이 내포되어 있어 더 좋았다. Jekyll Thema는 `jekyll theme 추천`으로 검색하면 다양한 테마들을 볼 수 있으니 본인이 마음에 드는 것을 고르면 된다.

Release 파일을 다운로드 받는 것보다 Fork의 장점은 언제든지 Sync를 할 수 있다는 점이라고 생각한다. 만약 버그가 있거나 중간에 업데이트가 있을 때, Fork 한 번만 해주면 해당 변경사항을 쉽게 반영할 수 있을 것이다. Repository name은 반드시 **github ID.github.io**의 형식으로 생성해야하며, 설정 후 Create Fork를 선택한다.

<img src='/images/images_231126/obsidian_github_io.png'>

그 다음, 로컬 레포지토리에 Clone 해주면 된다.

```bash
git clone "포크한 레포지토리의 url"
```

### Ruby를 설치하고 Bundle과 Jekyll 구동하기

이제 Ruby를 설치해줘야한다. [jekyll 공식 설치 가이드](https://jekyllrb.com/docs/installation/)를 참고하는 것이 더 도움이 될 것이다. Windows 사용자는 해당 홈페이지 설명을 보고 본인 버전에 맞는 적절한 Ruby 버전을 설치한다. 나는 Windows 11 64bit 환경이고, 홈페이지에서 권장하고 있는 `WITH DEVKIT [Ruby+Devkit 3.2.2-1 (x64)]`를 설치했다. Ruby 설치 파일은 `.exe`이므로 쉽게 설치할 수 있으며 별도의 환경 설정을 할 필요는 없다.

<img src='/images/images_231126/obsidian_ruby.png'>

인스톨러가 종료되면서 해당 cmd 창이 발생하는데, 공식 설치 가이드에서 설명하는대로 3을 입력해 개발 도구를 추가로 설치해준다. 전체 파일 용량은 꽤 큰데, 약 1GB 정도를 소모하는 것 같으니 미리 참고하면 좋다. 설치가 완료되면 아까 Clone 했던 Local Repo로 경로를 이동한 후 다음 명령어를 입력한다.

```bash
gem install jekyll bundler
```

<img src='/images/images_231126/obsidian_gem_install.png'>

그럼 jekyll과 의존하는 파일을 설치한다. 여기서 #오류 가 한 번 발생했다. gemfile을 찾을 수 없다는 오류였다. PowerShell에서는 안됐는데, git bash에서 실행했더니 잘 되었다. 위 방법으로 해결하면 될 것 같다는 생각이다. 이제 다음 명령어를 실행했을 때 정상 작동하는지 확인하자.

```bash
jekyll -v
gem -v
```

이제 `init.sh`을 실행해서 초기화를 수행해주면 되지만, 아쉽게도 우리 Windows 유저들은 리눅스 쉘 스크립트를 실행할 수 없다. 따라서 다음에 해당하는 폴더와 파일들을 수동으로 삭제해주면 된다... ㅠㅠ

**로컬 repo에서 삭제해야할 목록**

- `Gemfile.lock` 파일.

- `docs`폴더 및 디렉토리.

- `.travis.tml` 파일. **(난 없었음)**

- `_posts.docs` **(.md파일들이 있는데, 포스팅 예시이므로 참고해도 된다.)**

- `.github` 폴더에서 `workflows` 폴더를 남기고 삭제. **(? 검증을 안해봤는데 다 지워도 될 것 같다.)**

이제 `bundle install` 명령으로 의존성 파일을 설치해준다. 아마 이전 작업에서 설치가 이미 되었을 수도 있다. `bundle fund`는 직접 실행해야 한다는 안내 문구가 나오면 친절한 설명에 감사하며 직접 명령어를 따로 입력해 의존성 파일을 설치해준다.

### VS Code로 Github.io 배포를 위해 초기 설정하기

<img src='/images/images_231126/obsidian_vscode.png'>

이제  `_config.yml` 파일에서 내 블로그를 세팅하기 위해서 몇 가지 설정을 만져주면 된다.

- lang : 커스터마이징 하기 전까지는 의미없다.    
- timezone : `Asia/Seoul`로 바꾸자.    
- title : 블로그 좌상단에 크게 보이는 제목을 말한다.    
- tagline : 제목 밑에 보이는 간단한 설명을 말한다.    
- description : 블로그에 보이진 않지만 그래도 바꿔주자.    
- url : 내 `github.io` 링크를 입력한다.    
- github : 내 `github username`을 입력한다.    
- social : 이메일, 링크드인 등을 설정할 수 있다.    
- theme_mode : 기본 모드가 light라고 하길래 dark로 바꿨다. 확인은 안해봄.    
- avatar : 블로그 좌상단에 크게 보이는 프로필 사진을 말한다.    
- defaults -> scope -> path : favicons 경로를 설정해주자. 브라우저 탭에 작게 보이는 이미지 등을 말한다.    

수정을 완료했으면 파일을 저장하고, 만약 jekyll이 구동 중이라면 구동을 중지하고 다시 실행해야 수정사항이 반영된다. 이제 `jekyll serve`를 bash에 입력하면 내 `github.io pages`를 `localhost`로 미리 볼 수 있다.

여기서 윈도우는 오류가 발생할 수 있는데, 글의 목차가 보이지 않는 오류이다. `/asset/js/dist/` 경로에서의 `.js` 관련 오류였는데, 나는 해당 명령어를 통해서 해결했다. 명령어를 bash에서 입력해주니 경로에 .js 파일들이 잘 설치되었다. 

```js
npx rollup -c --bundleConfigAsCjs
```
### Markdown으로 블로그 글 내용 작성하기

이제 Markdown을 이용해서 블로그 글을 작성하면 된다. Markdown에 대한 이해도가 높지 않으면 에디터를 사용하는 것이 좋다. VS Code에 내장된 Editor도 좋지만, Notion이나 Obsidian과 같은 소프트웨어를 이용하는 것이 초심자에게는 좋을 것이다. 특히 Obsidian의 경우 잘 사용할 수만 있다면 커스터마이징이 가능하기 때문에 더 많은 기능을 사용할 수 있을 것이다. 글을 모두 작성했으면 `_posts` 폴더에 마크다운 파일을 업로드 해준다. 또, 마크다운에서 링크한 이미지 파일은 `assets/img` 폴더에 업로드 해준다. 마크다운에서 이미지를 링크할 때, 해당 경로에 업로드 할 것을 상정하고 링크를 설정해줘야 한다. 또, 마크다운 맨 위에는 yml 문법을 통해 해당 블로그 글의 메타데이터를 입력해준다. 또한 다음과 같은 규칙을 지켜서 파일을 생성해야 한다.

```yml
---
title: AI 프로젝트를 위한 WSL2 개발 환경 세팅 가이드
date: 2023-11-20 00:06:11 +09:00
categories: [WSL2, AI]
tags: [WSL2, Linux, git]
image: wsl_easy_vs_hard.png
img_path: /assets/img/images_231120/
---
```

- 형식 : `yyyy-mm-dd-제목.md`
- 년 4자리, 월 2자리, 일 2자리와 제목을 넣어준다.
- 확장자는 `.md` 또는 `.markdown`으로 한다.
- 중간에 공백을 넣지 않는다. 공백이 필요하면 `-`로 바꾼다.

이제 `jekyll serve`를 최종적으로 실행해 다시 한 번 검증하고, `git push`를 통해 원격 레포지토리에 업로드한다.

<img src='/images/images_231126/obsidian_githubaction.png'>

여기서 수정하면 Jekyll configure가 생길텐데, 누른 후 별도의 수정없이 커밋을 눌러준다. 이후 `.github/workflow` 디렉토리에 기존 배포 방식에서 사용했던 파일을 삭제해준다. `pages-deploy.yml.hook`이 바로 그 파일이다. 원격 레포지토리에 `jekyll.yml`을 생성했으므로 로컬에서 다시 pull을 통해 해당 파일을 받아 동기화를 수행해준다. 또, `.gitignore` 내 `assets/js/dist` 디렉토리 내 파일들의 Push가 무시되도록하는 설정을 주석처리 해야한다.

이제 정말 마지막으로 `jeykll serve`를 수행해주고 다시 원격 레포지토리에 push해주면 모든 세팅이 완료된다. `github action`이 자동으로 `github page`를 배포해준다. 정말 좋은 세상이다...

## 마무리하는 글

옵시디언으로 마크다운을 작성하고, Github Action을 이용해서 Github Page를 배포하는 글을 작성해보았다. 다음 글에는 옵시디언 git을 이용해서 이미지와 .md 파일을 더 쉽게 동기화할 수 있도록 로직을 짜보도록 한다. 혹시 다른 오류가 발생할 수 있으니 아래 레퍼런스를 참고해서 트러블 슈팅에 꼭 성공하길 바란다.

## Reference

- [깃허브 페이지 제작 팁(1) - Jekyll 관련 에러 해결 방법](https://synoti21.github.io/blog%20dev/There-are-no-gemspecs-at-~~-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-(%EA%B9%83%ED%97%99-%ED%8E%98%EC%9D%B4%EC%A7%80-%EA%B2%8C%EC%8B%9C%ED%95%A0-%EB%95%8C)/)
- [# Jekyll Chirpy(v6.0.1) 테마를 활용한 Github 블로그 만들기(2023.6 기준)](https://jjikin.com/posts/Jekyll-Chirpy-%ED%85%8C%EB%A7%88%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-Github-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0(2023-6%EC%9B%94-%EA%B8%B0%EC%A4%80)/)
- [# Jekyll Chirpy 테마 사용하여 블로그 만들기](https://www.irgroup.org/posts/jekyll-chirpy/)
- [# Github Blog 만들기-2](https://velog.io/@hashnsalt/Github-Blog-%EB%A7%8C%EB%93%A4%EA%B8%B0-2)
- [# [개발자 블로그] Jekyll의 Chirpy테마로 깃허브 블로그 만들기](https://j1mmyson.github.io/posts/StartingBlog/)
- [Chirpy Thema](https://github.com/cotes2020/jekyll-theme-chirpy)
- [Ruby 공식 설치 사이트](https://rubyinstaller.org/downloads/)
- [jekyll 공식 사이트](https://jekyllrb.com/)
- [jekyll 공식 설치 가이드, For Windows](https://jekyllrb.com/docs/installation/windows/)
