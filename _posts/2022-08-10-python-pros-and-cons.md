---
layout: post
title: Python pros and cons
comments: true
categories: [python]
tags: [interpret, object, gil, python]
---

### pros
- 쉽다
- 직관적이다

### cons
- Interpreter Language 이기 때문에 Compile Language 보다 느리고 Real-time 이 요구되는 System에는 적합하지 않다.
- GIL(Global Interpreter Lock)로 인해 일반적으로 Multi-threading이 효과가 없다. 
GIL은 한 번에 하나의 바이트 코드만 실행하도록 하는 것을 말한다. 
단 I/O와 관련된 Task 처리의 경우, CPU 사용이 주가 아니기 때문에 유의한 효과를 얻을 수 있다.
- 