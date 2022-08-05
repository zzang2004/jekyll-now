---
layout: post
title: Functional Programming
comments: true
categories: [programming]
tags: [Functional, programming]
---

Functional Programming에 대해서 알아보자.

**Feature**
  1. Variable is not variable: 4:30에서도 설명했듯, 특별한 경우가 아니라면 변수의 값을 변경할 수 없습니다. 원한다면 새로운 변수를 생성해서 계산값을 할당하거나, 계산값 자체를 리턴하여 처리해야 합니다.
  2. Every expression is return value: 이는 5:36의 설명과도 일맥상통하는데, 함수의 내부는 단 한 줄의 Expression으로 구성되며 그것이 곧 그 함수의 리턴값이 됩니다. 그렇기에 필연적으로 Recursive하게 함수를 구성할 수밖에 없습니다. 예를 들어 1~n까지 더한 값을 반환하는 함수의 경우 [ let rec sum n = if n = 1 then n else n + sum (n-1) ]과 같이 구현합니다.
  3. Higher-order function: 5:43에 나와 있듯, 함수인데 입력값과 출력값도 함수인 경우입니다. 예를 들어 어떤 함수든지간에, 그 함수를 두 번 적용하는 함수 makeTwice의 경우 [ let makeTwice f = fun x -> f (f x) ]와 같이 구현합니다. 입력받는 인자 f도 함수이고, 반환하는 값 [ fun x -> f (f x) ] 또한 함수입니다. 물론 f의 정의역과 치역은 동일해야 합니다. 영상에서 잠깐 언급된 Functor의 경우, 클래스를 입력받아 클래스를 반환하는 함수.. 정도로 이해하셔도 무방합니다.
  4. Pattern-matching: 우리가 if-else문을 이용하여 특정 변수 안에 들어있는 값에 따라 프로그램의 분기를 만든다면, 패턴매칭은 해당 변수가 어떤 형태를 띠고 있는지에 따라 프로그램의 분기를 만듭니다. 예를 들어 int 타입 변수라면 항상 정수 하나가 저장되어 있는 상태이므로 형태를 나눌 수 없습니다만,  list의 경우에는 '비어있거나, 적어도 하나라도 차 있거나'로 그 형태를 구분할 수 있습니다. 정수형 리스트에 들어있는 값을 전부 더하는 함수 sumList를 패턴매칭으로 구현하면 [ let rec sumList list = match list with [] -> 0 | hd::tl -> hd + sumList tl ]과 같습니다. 여기서 []은 리스트가 가질 수 있는 형태 중 '비어있음'을 뜻하며, hd::tl에서 hd는 리스트의 원소, tl은 나머지 리스트를 뜻하기에 이는 '리스트에 적어도 하나의 원소가 들어있음'의 형태를 뜻합니다. 즉 list라는 변수를 [] | hd::tl로 패턴매칭한 것이죠. 비단 리스트뿐만 아니라 내가 직접 '여러 형태를 지닌 새로운 타입'을 만들어서 패턴매칭하는 것또한 가능하며, 이 때 Monad의 개념이 등장합니다.
  5. Monad: 단순 정수 하나를 입력받아 저장하기 위해서는 int형 변수를 사용하면 됩니다만... 무언가 불행한 일이 발생하여 아무런 정수도 입력되지 않은 채 프로그램이 진행될지도 모릅니다. 이 때를 대비하여 우리는 새로운 타입, intOrNone을 만들 수 있습니다. [ type intOrNone = Some of int | None ] 이렇게 만들어진 intOrNone은 두 가지 형태를 지니므로 패턴매칭을 이용하여 프로그램 분기가 가능합니다. 만약 정상적으로 입력받았을 경우에는 정수 하나가 저장될 것이고 그렇지 않다면 None이 설정되어 있을테니 그에 맞게 프로그램을 분기하는 것이 가능합니다. 이렇듯 여러 예기치 못한 상황을 대비하거나, 혹은 이 형태를 이용하여 외부로부터 어떤 자료가 저장되어 있는지 철저히 숨기는 데에 모나드가 사용됩니다.

#### Reference
1. https://www.youtube.com/watch?v=4ezXhCuT2mw
2. 