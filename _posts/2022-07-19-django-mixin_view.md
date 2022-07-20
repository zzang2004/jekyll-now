---
layout: post
title: Mixin view
comments: true
categories: [django]
tags: [django, python]
---


```python
from rest_framework import generics
```
DRF generics의 ListCreateAPIView, RetrieveUpdateDestroyAPIView 등의 View는 CRUD에 해당하는 POST, GET, PUT, PATCH, DELETE 
Method Request를 받으면 상속 받은 Mixin Class의 함수를 호출하여 Method에 적합한 내부 Logic을 타게 된다.

P.S: URI에 담긴 Parameter Value는 kwargs에 담기게 된다.(http://localhost:8000/v1/**projects/7**/examples)
```python
# urls.py
urlpatterns = [
    path(route="projects/<int:project_id>", view=ProjectDetail.as_view(), name="project_detail"),
    # ...
]

# mixins.py
class CreateModelMixin:
    """
    Create a model instance.
    """
    def create(self, request, *args, **kwargs):
        # kwargs = {'project_id': 7}
        serializer = self.get_serializer(data=request.data)
        # ...
```

#### ListCreateAPIView
- POST: create
- GET: list

#### RetrieveUpdateDestroyAPIView
- GET: retrieve
- PUT: update
- PATCH: partial_update
- DELETE: destroy

#### create
ListCreateAPIView에서, perform_create()를 통해 record 생성 시 필요한 별도 조작을 처리한다.

```python
class CreateModelMixin:
    """
    Create a model instance.
    """
    def create(self, request, *args, **kwargs):
        serializer = self.get_serializer(data=request.data)
        serializer.is_valid(raise_exception=True)
        self.perform_create(serializer)
        headers = self.get_success_headers(serializer.data)
        return Response(serializer.data, status=status.HTTP_201_CREATED, headers=headers)

    def perform_create(self, serializer):
        serializer.save()

    def get_success_headers(self, data):
        try:
            return {'Location': str(data[api_settings.URL_FIELD_NAME])}
        except (TypeError, KeyError):
            return {}
```


#### list
ListCreateAPIView에서, get_queryset()을 통해 record list를 control한다.

```python
class ListModelMixin:
    """
    List a queryset.
    """
    def list(self, request, *args, **kwargs):
        queryset = self.filter_queryset(self.get_queryset())

        page = self.paginate_queryset(queryset)
        if page is not None:
            serializer = self.get_serializer(page, many=True)
            return self.get_paginated_response(serializer.data)

        serializer = self.get_serializer(queryset, many=True)
        return Response(serializer.data)
```

#### retrieve
RetrieveUpdateDestroyAPIView에서, queryset, lookup_url_kwarg Variables를 통해 single record를 조회한다.
```python
class RetrieveModelMixin:
    """
    Retrieve a model instance.
    """
    def retrieve(self, request, *args, **kwargs):
        instance = self.get_object()
        serializer = self.get_serializer(instance)
        return Response(serializer.data)
```

#### update, partial_update
```python
class UpdateModelMixin:
    """
    Update a model instance.
    """
    def update(self, request, *args, **kwargs):
        partial = kwargs.pop('partial', False)
        instance = self.get_object()
        serializer = self.get_serializer(instance, data=request.data, partial=partial)
        serializer.is_valid(raise_exception=True)
        self.perform_update(serializer)

        if getattr(instance, '_prefetched_objects_cache', None):
            # If 'prefetch_related' has been applied to a queryset, we need to
            # forcibly invalidate the prefetch cache on the instance.
            instance._prefetched_objects_cache = {}

        return Response(serializer.data)

    def perform_update(self, serializer):
        serializer.save()

    def partial_update(self, request, *args, **kwargs):
        kwargs['partial'] = True
        return self.update(request, *args, **kwargs)
```


#### destroy
```python
class DestroyModelMixin:
    """
    Destroy a model instance.
    """
    def destroy(self, request, *args, **kwargs):
        instance = self.get_object()
        self.perform_destroy(instance)
        return Response(status=status.HTTP_204_NO_CONTENT)

    def perform_destroy(self, instance):
        instance.delete()
```