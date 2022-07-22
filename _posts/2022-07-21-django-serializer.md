---
layout: post
title: Serializer
comments: true
categories: [django]
tags: [django, python]
---

serializer class의 내부 class Meta의 fields에 입력한 attribute는 Request 시에 입력 받을 수 있고 Response에서 확인할 수 있는 attribute이다.

단, read_only_fields에 입력한 attribute는 Request, Swagger 등에서 입력할 수 없으나 response에는 여전히 확인할 수 있다.

즉, Client에게 직접 입력 받지 않기 위해서 read_only_fields에 입력한 attribute를 입력 및 저장하기 위해서는, 아래와 같이 View 단에서 담아야 한다.

```python
# serializer.py
class ExampleStateSerializer(serializers.ModelSerializer):
    class Meta:
        model = ExampleState
        fields = ("id", "example", "confirmed_by", "confirmed_at")
        read_only_fields = ("id", "confirmed_by", "confirmed_at")

# view.py
class ExampleStateList(generics.ListCreateAPIView):
    serializer_class = ExampleStateSerializer
    permission_classes = [IsAuthenticated & IsProjectMember]
    
    def perform_create(self, serializer):
        serializer.save(confirmed_by=self.request.user)
```
