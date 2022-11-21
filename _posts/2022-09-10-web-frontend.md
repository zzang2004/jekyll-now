---
layout: post
title: Frontend basic
comments: true
categories: [web]
tags: [html, css, javascript, web]
---

Browser를 통해 Naver를 방문할 때, 어떤 작업들이 수행될까?

Browser는 www.naver.com로부터 Html File을 수신하고, 해당 File을 통해서 js, gif, png 등의 Resource 를 수신하는 것이다.

#### Html File의 구성
Html 단일 File 안에 CSS, JS를 포함하는 경우와, 별도 CSS, JS File로 분리하는 경우가 있지만 대부분 후자의 경우로 한다. 
왜냐하면, HTML 응답 Body 크기를 줄일 수 있고, Browser Caching 기능을 통해 CSS, JS File을 서버로부터 다시 읽어들이지 않을 수 있고,
웹페이지 응답성을 높일 수 있기 때문이다.

#### Client
HTTP Request를 보낼 수 있는 어떠한 프로그램이든 Client가 될 수 있음.
1. Browser
2. Browser for CLI
3. Android/IOS App

#### 하나의 HTTP Request, 하나의 Response
Process about Request to Response
1. HTTP Request From Browser
2. HTTP Request에 대한 처리 From Server's View
3. View에서 Return 해야만 비로소 HTTP 응답이 시작 됨. 즉 응답을 하기 전까지는 Client에서 하얀 화면만 보여짐.
4. Response가 HTML인 경우, Browser는 HTML 문자열을 1줄씩 해석하여 그래픽적으로 표현함.(외부 Resource는 해당 Resource가 로딩 완료/실행 될 때까지 대기함.)

#### HTML UI 응답성을 낮추는 경우
1. 과도한 JS 로딩 및 계산
2. 과도한 CSS 레이아웃 로딩 및 계산
3. 잦은 시각적 객체 업데이트

#### Reference
1. Inflearn, 파이썬/장고 웹서비스 개발 완벽 가이드 with 리액트, 이진석
