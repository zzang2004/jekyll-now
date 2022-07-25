---
layout: post
title: DRF generate automatically UI form pages
comments: true
categories: [django]
tags: [django, drf, form, python]
---

drf(Django RestFramework)로 view(GenericAPIView)를 구성하면 List, Detail을 위한 UI Form이 자동으로 생성된다.

```python
# urls.py
from django.urls import path

from .views import UrlList, UrlDetail, UrlReverseDetail

app_name = 'url_transform'

urlpatterns = [
    path(route="short-links/", view=UrlList.as_view(), name="url_list"),
    path(route="short-links/<str:short_id>/", view=UrlDetail.as_view(), name="url_detail"),
]
```

```python
# views.py
from django.shortcuts import redirect
from rest_framework import generics

from .models import Url
from .serializers import UrlSerializer


class UrlList(generics.ListCreateAPIView):
    model = Url
    serializer_class = UrlSerializer
    queryset = model.objects.all()


class UrlDetail(generics.RetrieveUpdateDestroyAPIView):
    queryset = Url.objects.all()
    serializer_class = UrlSerializer
    lookup_url_kwarg = "short_id"
```

[<img src="{{ site.baseurl }}/images/220725-list_view_form.png" />]({{ site.baseurl }}/)
[<img src="{{ site.baseurl }}/images/220725-detail_view_form.png"/>]({{ site.baseurl }}/)

물론 여기에는 serializer에 입력한 "fields", "only_read_fields" 변수 value에 영향을 받는다.

```python
from rest_framework import serializers

from .models import Url


class UrlSerializer(serializers.ModelSerializer):
    class Meta:
        model = Url
        fields = (
            "shortId",
            "url",
        )
        read_only_fields = (
            "shortId",
        )
```
