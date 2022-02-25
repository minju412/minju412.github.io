---
title:  "[Git] branch와 merge"
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

# 📝branch

## 새 작업 branch 만들기
```
git checkout -b 1-layout
```
`checkout`: 브랜치를 이동하라는 명령 <br>
`-b`: 브랜치를 생성하라는 옵션. 즉, 새로운 브랜치를 생성하자마자 그리로 이동하라는 의미 <br>
`1-layout`: 생성하려는 브랜치 이름. <strike>(저는 “이슈 번호-이슈 내용” 의 형식으로 적었습니다.) </strike><br>

## 새 작업 branch를 원격 저장소로 push
```
git push --set-upstream origin 1-layout
```
`--set-upstream`: 쉽게 말해 로컬 브랜치와 원격 브랜치를 연결하는 옵션 <br>
`origin`: 원격 저장소 이름<br>

## branch에서 작업을 마친 후 원격 저장소로 push
```
git add .
git commit
git push
```
`git commit` 메시지 입력 후 엔터를 치면 커밋 메시지 창이 나온다. <br>
커밋 메시지 창은 vim과 같은 형태로 `i`를 입력한 뒤에 내용을 작성한다.<br> 
내용 작성 후 `esc`를 누르고 `:wq`를 입력한다. (`#` 주석처리 하지 않은 부분만 읽힘!) <br>
> 커밋 메시지 예시

```
[#1] Layout 변경

- 변경 사항-1

- 변경 사항-2

- 변경 사항-3

Resolves #1

```
이때 `#이슈번호` 형식으로 커밋 메시지에 입력을 하면 github이 이슈 번호를 읽어들이게 된다. <br>
하단에 `Resolves #1`를 붙이면 push 후 자동으로 1번 이슈가 닫힌다.<br>

# 📝merge

## master와 병합하기
```
git checkout master
git merge 1-layout
```
checkout을 통해 현재 master 브랜치인 상태이다. <br>
이때 master에서 1-layout 브랜치를 병합한다. (master로 1-layout을 가져온다.)<br>

## pull request 생성
앞서 `git merge 1-layout` 명령을 통해 pull request(PR)를 생성할 수 있다. <br>
PR을 받은 원본 저장소 관리자<strike>(지금은 나..)</strike>는 코드 변경 내역을 확인하고 Merge 여부를 결정한다. 
원본 저장소에 merge가 완료되면 로컬 코드와 원본 저장소의 코드가 동기화 된다. <br>
이후 작업하던 로컬의 브랜치를 삭제한다.<br>

## branch 삭제
(현재 master인 상태에서 아래 명령어 입력)
> 병합한 브랜치 지우기
```
git branch -d 1-layout
```
> 병합하지 않은 브랜치 지우기
```
git branch -D 1-layout
```

## merge를 했는데 PR이 생성되지 않을 때
(master 브랜치에 해당 브랜치 내용을 <strong>강제</strong>로 덮어씌우기)
```
git checkout 1-layout
git branch master 1-layout -f
git checkout master
git push origin master -f
```

***
<br>

    💛 개인 공부 기록용 블로그입니다. 👻

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}