---
layout: post
title: Reverse reference
comments: true
categories: [django]
tags: [django, python]
---

```python
class Member(models.Model):
    user = models.ForeignKey(to=User, on_delete=models.CASCADE, related_name="role_mappings")
    project = models.ForeignKey(to=Project, on_delete=models.CASCADE, related_name="role_mappings")
    role = models.ForeignKey(to=Role, on_delete=models.CASCADE)

    # ...

    class Meta:
        unique_together = ("user", "project")
```
Member Model은 User, Project, Role Model(이하, Model 생략)을 FK로 Reference한다. User는 Project를 직접 FK로 Reference하지 않지만, 
Project.objects.filter(role_mappings__user=self.request.user) 코드와 같은 형태로 Reverse Reference가 가능하다. 

Member의 record는 Project, User를 갖기 때문에 User를 통해 User가 할당된 Project를, Project를 통해 user가 할당된 Project를 알 수 있는 것이다.

```python
class ProjectList(generics.ListCreateAPIView):
    serializer_class = ProjectPolymorphicSerializer
    filter_backends = (DjangoFilterBackend, filters.SearchFilter, filters.OrderingFilter)
    search_fields = ("name", "description")

    def get_queryset(self):
        return Project.objects.filter(role_mappings__user=self.request.user)
```
