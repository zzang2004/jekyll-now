---
layout: post
title: Server-Sent Events
comments: true
categories: [web]
tags: [server-sent events, server, web]
---

Server 개발을 하다보면 Client의 Request 없이도 Server에서 Client로 Data를 보내 주어야 할 때가 있는데, 이럴 때 사용할 수 있는 것이 SSE이다.

SSE는 Client에서 Subscribe를 위한 Request를 한 번 보내고 나면, 이후에는 서버에서 비동기적으로 데이터를 전송할 수 있다.

Process는 다음과 같다.
1. Client에서 SSE Request를 보낸다.
2. Server에서는 해당 특정 Client와 매핑되는 SSE 통신 객체를 만든다.
3. Server에서 Event가 발생하면 해당 객체를 통해 Client로 Data를 보낸다.

#### Reference
1. Spring에서 Server-Sent-Events 구현하기, https://tecoble.techcourse.co.kr/post/2022-10-11-server-sent-events/
