---
title: "[GitHub Blog] 깃허브 블로그 시작하기"
date: 2023-03-09
categories:
  - GitHub
tags:
  - [Github, Blog, MarkDown]
permalink: /Blog/git-hub-blog-01/
toc: true
toc_sticky: true
toc_label: "GITHUB BLOG START"
last_modified_at: 2023-03-09
---

## GitHub Blog 만들기

Jekyll theme의 Minimal Mistakes 로 블로그를 생성해보자

📌 **작성자 개발 환경** <br>
**OS** : Windows 10<br>
{: .notice}

# 기본 환경 세팅

## 루비 설치

[Ruby for Window - 루비 다운로드](https://rubyinstaller.org/downloads/){:target="\_blank"}
DEVKIT이 필요하므로 With DEVKIT에 있는 버전을 다운 받는다.
여기서 중요한 것은 **Jekyll이 32bit**이기 때문에 설치시 반드시 **(x86)**으로 다운 받는다.

![ruby-download](https://user-images.githubusercontent.com/100749520/224908732-2d6380b7-4573-4f30-ae21-c316cfe9a9d6.png)

## Jekyll 설치
  명령 프롬프트 창에서 아래 명령어로 Jekyll을 설치해보자.
   ```
   gem install jekyll bundler
   ```
  터미널을 열고 설치를 완료하면 `ruby -v`와 `jekyll -v`으로 버전 및 설치를 확인 할 수 있다.

## minimal-mistakes 테마
- [minimal-mistakes theme 공식 홈페이지](https://mmistakes.github.io/minimal-mistakes/)
- [minimal-mistakes 가이드](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)
- [minimal-mistakes Github Link](https://github.com/mmistakes/minimal-mistakes)

여러가지 방법으로 시도 했는데 가장 쉬운 방법은 - [minimal-mistakes Github Link](https://github.com/mmistakes/minimal-mistakes) 에서 zip파일을 다운로드 받는 방법이다.

![image](https://user-images.githubusercontent.com/100749520/224916900-b6a892f8-9608-491b-b9fa-01ef4334ab10.png)

