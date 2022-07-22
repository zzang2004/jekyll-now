---
layout: post
title: Authentication
comments: true
categories: [django]
tags: [django, python]
---

#### Authentication Process
1. 매 요청 시마다 APIView의 dispatch(request) 호출(CBV를 구현했다면 항상 dispatch가 호출 됨)
2. APIView의 initial(request) 호출
3. APIView의 perform_authentication(request) 호출
4. request의 user 속성 호출 (rest_framework.request.Request Type)
5. request의 _authenticate() 호출(실제적으로 여기에서 인증 여부를 확인함)

- Session 인증을 할 때는 Login할 때만 인증
- API에서는 Client의 Server로의 요청은 매번 인증을 하여 요청의 유효성을 검사

#### Authentication Type
1. SessionAuthentication: Login을 통한 인증이며 Admin Page 등을 이용하기 위해 활성화 해야함
2. BasicAuthentication: 매 요청 때마다 Request Header에 id, pw를 담아서 보내야함
3. TokenAuthentication: Token의 만료 기한이 없고 User 별로 1개만 할당되어 노출되면 문제가 됨
4. RemoteUserAuthentication

#### DFS's Permission system
1. AllowAny: 인증 여부에 상관없이, View 호출 허용
2. IsAuthenticated: 인증된 요청에 한해서, View 호출 허용
3. IsAdminUser: Staff 인증 요청에 한해서, View 호출 허용
4. IsAuthenticatedOrReadOnly: 비인증 요청에게는 읽기 권한만 허용

#### DFS's user 권한
1. is_active: True여야지만 인증 요청을 할 수 있음
2. is_staff: admin page 접근 권한이 주어지지만 접근만 가능하고 추가적인 권한(django model 관련)이 부여되야 실제적으로 admin page에서 별도 작업을 수행할 수 있음
3. is_superuser: 별도 Permission이 주어지지 않아도 모든 Model에 대한 CRUD가 가능함.

#### Auth App
1. DjangoModelPermissions: 인증된 요청에 한해 View 호출 허용, 추가로 장고의 모델 단위 Permissions 체크
2. DjangoModelPermissionsOrAnonReadOnly
3. DjangoObjectPermissions: 인증된 요청은 Object에 대한 권한 체크

#### P.S
- django permission과 drf permission은 다름.

#### Reference
- 파이썬/장고 웹서비스 개발 완벽 가이드 with 리액트, 이진석