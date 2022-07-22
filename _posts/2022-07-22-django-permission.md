---
layout: post
title: Permission
comments: true
categories: [django]
tags: [django, python]
---

DetailView에서 permission_classes에 has_object_permission을 구현한 permission class를 추가하면, View에 Detail HTTP Methods(GET(retrieve), PATCH, PUT, DELETE)에 
해당하는 Request가 들어올 때 has_object_permission의 Logic을 타면서 Permission을 Customizing 할 수 있다.

```python
# views.py
class CategoryTypeDetail(generics.RetrieveUpdateDestroyAPIView):
    queryset = CategoryType.objects.all()
    serializer_class = CategoryTypeSerializer
    lookup_url_kwarg = "label_id"
    permission_classes = [IsAuthenticated & (IsProjectAdmin | IsProjectStaffAndReadOnly) & IsAuthorOrReadOnly]

```

```python
# permissions.py
from rest_framework import permissions

class IsAuthorOrReadOnly(permission.BasePermission):
    # 1차 인증에 해당
    # ListView, DetailView에서 모두 사용 가능
    # 인증된 User에 한해, GET, POST 허용
    def has_permission(self, request, view):
        return request.user.is_authenticated
    
    # 2차 인증에 해당
    # Detail(object)View에 본 IsAuthorOrReadOnly를 적용하면 GET, PATCH, DELETE Request 마다 has_permission 이후에 호출 됨. 
    # 작성자에 한해, Record에 대한 PATCH, DELETE 허용
    def has_object_permission(self, request, view, obj):
        # 조회 요청(GET, HEAD, OPTIONS)에 대해서는 모두 허용
        if request.method in permission.SAFE_METHODS: # SAFE_METHODS = ('GET', 'HEAD', 'OPTIONS')
            return True
        # PATCH, DELETE 요청에 대해, 작성자일 경우에만 요청 허용
        return obj.author == request.user
```

#### Logic
1. 모든 HTTP Method에 대해서 has_permission()을 수행하여 Authentication 유무를 확인함
2. 1에서 return True라면, POST만 제외한 HTTP Methods(GET, PATCH, DELETE)의 경우에 대해서 has_object_permission()을 수행하여 True를 return할 경우 허용, 그렇지 않을 경우 허용하지 않음
