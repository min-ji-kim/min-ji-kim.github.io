---
layout: post
title: .dev redirect 해결하기(Ubuntu)
categories : TIL
tags : 환경설정
---

# .dev redirect 해결하기(Ubuntu)

Chrome 63 버전(2017년 12월)이상 사용 시 도메인이 .dev나 .foo로 끝날 경우 

http 가 https로 redirect되도록 적용됨.

참고 : [URL](https://ma.ttias.be/chrome-force-dev-domains-https-via-preloaded-hsts/)

### 해결방법
> 1. Google Chrome 버전 62 이하ㄴ로 낮추기
> 2. URL 주소 .dev -> .test 등 다른 주소로 변환하기
> 3. SSL 인증서 설치해서 http -> https 로 변환하기



### 1. 크롬 63 이전 Version 설치

*설치 사이트 : [https://www.slimjet.com/chrome/google-chrome-old-version.php](https://www.slimjet.com/chrome/google-chrome-old-version.php)

위 사이트에서 61.0.3163.79 클릭하여 다운로드 폴더에 설치 후 명령어 실행 

~$ cd Downloads
~/Downloads$ sudo dpkg -i chrome64_61.0.3163.79.deb