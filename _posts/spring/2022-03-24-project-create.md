---
title:  "[SPRING] 프로젝트 생성과 라이브러리"

categories:
  - Spring
tags:
  - [Framework, Spring, Java]

toc: true
toc_sticky: true
 
date: 2022-03-24
last_modified_at: 2022-03-24
---

## 🌱 사전 준비
- jdk: Java 11
- IDE: intellij

## 🌱 스프링 프로젝트 생성
아래 스프링 부트 스타터 사이트로 이동
> https://start.spring.io

아래와 같이 설정<br>
- Project: Gradle Project<br>
- Language: Java<br>
- Spring Boot: 괄호가 붙어있지 않은 가장 최신 버전 (22년3월24일 기준: 2.6.4)<br>
- Dependencies: Spring Web, Thymeleaf<br>

## 🌱 intellij에서 오픈
Generate 후 압축을 풀기<br>
intellij에서 build.gradle(압축 푼 폴더 안에 존재) 오픈(open as project)<br>

## 🌱 스프링 부트 라이브러리
- spring-boot-starter-web
> spring-boot-starter-tomcat: 톰캣(웹서버)<br>
> spring-webmvc: 스프링 웹 MVC<br>
- spring-boot-starter-thymeleaf: 타임리프 템플릿 엔진 (View)
- spring-boot-starter(공통): 스프링 부트 + 스프링 코어 + 로깅
> spring-boot<br>
> spring-boot-starter-logging<br>

## 🌱 테스트 라이브러리
- spring-boot-starter-test
> junit<br>
> mockito<br>
> assertj<br>
> spring-test<br>



***
<br>

    💛 개인 공부 기록용 블로그입니다. 👻

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}