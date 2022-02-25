---
title:  "[Git] .gitignore 파일 만들기"
# excerpt: ".gitignore에 대해 알아보자"

categories:
  - Git
tags:
  - [Git]

toc: true
toc_sticky: true
 
date: 2022-02-25
last_modified_at: 2022-02-25
---

## .gitignore 이란?
프로젝트를 개발할 때 필요한 파일 이외의 불필요한 로그 파일들이 생성된다.
.gitignore은 이러한 파일들을 <u>git 관리 대상에서 제외</u>하기 위해(commit에 포함하지 않도록) 규칙들을 저장한 파일이다.
<br>

예를 들어 협업 중 팀원의 프로젝트를 내려받아서 작업할 때, <br>
팀원들의 작업환경이 모두 다르기 때문에(log file, 컴파일된 파일, 운영체제 파일, IDE 설정 파일 등)
충돌을 피하기 위해 해당 파일들을 .gitignore에 추가해서 Git이 위치를 추적하지 못하게 설정한다.
<br>

## 파일 생성하기
프로젝트의 최상위 디렉터리에 `.gitignore` 파일로 저장한다.
<br>

## 파일 내용 작성하기 

> gitignore.io 
>> <https://www.toptal.com/developers/gitignore>

<center><img src="https://user-images.githubusercontent.com/59405576/155642486-8895d34e-1fee-4f93-97b9-679e080e339d.png" width="60%" height="60%"></center>

위 사이트에서 사용할 언어를 검색해 "생성" 버튼을 누른 뒤 해당 코드를 복사해 `.gitignore` 파일에 붙여넣는다.
<br>

## 파일을 레포지토리에 push하기
```
git add .gitignore
git commit -m "커밋 메세지"
git push
```
<br>

## 참고

- [기억의 궁전](https://parkjye.tistory.com/28)


***
<br>

    💛 개인 공부 기록용 블로그입니다. 👻

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}