---
layout: post
title: Declarative vs Imperative
comments: true
categories: [programming]
tags: [Declarative, Imperative, programming]
---

Declarative Programming(이하 선언형)과 Imperative Programming(이하 명령형)은 무슨 차이가 있을까?

선언형은 내가 하고자 하는 것을 선언하는 것이고 명령형은 내가 하고자 하는 것을 절차적으로 명령하는 것이다.

따라서 선언형은 본질적인 핵심(What)에 집중할 수 있고 명령형은 과정을 모두 명시 해야 한다.(How)

아래 예시를 살펴보자.

1. Restaurant: 한 가족이 식당에 도착하여 앉을 자리를 위해 요청한다.
   - 선언형: 네 명 앉을 자리 부탁해요.
   - 명령형: 4번 테이블이 비어있습니다. 우리 네 명은 저 자리로 걸어가 앉을 것입니다.<br><br>

2. 집에 돌아가는 법: 택배 기사가 자신의 위치에서 우리집을 어떻게 와야 하는지 질문하여 이에 대답한다.
   - 선언형: 내 주소는 98 West Immutable Alley, Eden, Utah 84310입니다.
   - 명령형: 주차장 북쪽 출구를 나와 왼쪽으로 가세요. 12번가 출구에 도착할 때까지 15번 북쪽 도로를 타세요. 이케아를 끼고 우회전하세요. 직진하여 첫 번째 신호등에서 우회전 하세요. 다음 신호등을 지나 좌회전을 하세요. 우리 집은 #298입니다.<br><br>

코드 예시를 살펴보자. 
문자열의 공백을 "-"로 치환하고자 한다.

```python
string_object = "Hello, World!"


# 선언형
declarative_object = string_object.replace(" ", "-")

# 명령형
imperative_object = ""
for char in string_object:
    if char == "":
        imperative_object += "-"
    else:
        imperative_object += char
```


#### Reference
1. https://ui.dev/imperative-vs-declarative-programming
2. https://www.youtube.com/watch?v=7aEQLvvnQIY
3. https://boxfoxs.tistory.com/430