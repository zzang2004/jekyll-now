---
layout: post
title: Micro Service Architecture
comments: true
categories: [architecture]
tags: [msa, architecture]
---

### 정의
Software Architecture의 하나로, Application이 여러 개의 작고 독립적인 형태의 서비스로 구성되어 있는 것.(From Gartner)

### 배경
기존의 Monolithic Architecture는 Application이 한 Project에 통합되어 있는 형태이기 때문에, 
1. 부분 장애가 전체 서비스의 장애로 확대될 수 있다
2. 부분적인 Scale-out이 어렵다.
3. 서비스의 변경이 어렵고, 장애의 파악이 어렵다
   - 여러 컴포넌트가 하나의 서비스에 강하게 결합되어 있을 수 있기 때문에 수정에 대한 영향 파악이 어렵다
4. 배포가 어렵다
   - 하나의 모듈을 수정해도 모듈이 독립적이지 않아 프로젝트 전체를 테스트 해야 하기 때문에 많은 비용이 발생한다
5. Framework와 언어에 종속적이다

Monolithic Architecture가 가지는 이러한 단점들로 인해 MSA가 등장하게 되었다.

### MSA's Feature
1. 부분 장애가 전체 서비스의 장애로 확장될 가능성이 적다
2. Load balancing을 통해 Service별 Computing Resource를 효율적으로 사용할 수 있다.
3. 서비스의 변경이 쉽고 장애 파악이 쉽다
4. 서비스별 배포가 가능하므로 테스트 비용이 낮다
5. 서비스별 I/O가 정해져있으므로 언어에 비교적 덜 종속적이다.



#### Reference
1. https://blog.lgcns.com/1278
2. https://prodo-developer.tistory.com/137