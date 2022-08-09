---
layout: post
title: Serializer's read_only_fields
comments: true
categories: [django]
tags: [django, python]
---
Serializer Class의 Meta Class의 fields에 포함되는 속성 중, read_only_fields에 넣지 않은 속성은 Create, Update 시에 입력으로 받겠다는 의미이다.
즉, 넣지 않은 속성, 즉 입력받고자 하는 속성을 Request에 담지 않으면 Bad Request Error가 발생한다.

```python
class ExampleStateSerializer(serializers.ModelSerializer):
    class Meta:
        model = ExampleState
        fields = ("id", "example", "confirmed_by", "confirmed_at")
        read_only_fields = ("id", "example", "confirmed_by", "confirmed_at")
        
        # example에 해당하는 Value를 Request's data에 실어 보내지 않으면 Bad Request: /v1/projects/41/examples/1290/states
        # read_only_fields = ("id", "confirmed_by", "confirmed_at")

```
