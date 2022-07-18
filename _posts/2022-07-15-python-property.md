---
layout: post
title: Property
comments: true
categories: [python]
tags: [python]
---

```python
class Person:
    def __init__(self, first_name, last_name, age):
        self.first_name = first_name
        self.last_name = last_name
        self.age = age

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, age):
        if age < 0:
            raise ValueError("age must >= than 0.")
        else:
            self._age = age

    @property
    def full_name(self):
        return f"{self.first_name} {self.last_name}"


jdkim = Person("JeonDo", "KIM", 31)

# jdkim.age = -1 # ValueError: age must >= than 0.
jdkim.age += 1

print(jdkim.age) # 32
print(jdkim.full_name) # JeonDo KIM

```

## Use
1. setter, getter 용도로 이용하며, \_\_init\_\_ 시점에서 self.age가 정의될 때도 setter가 수행된다.
(코드를 보면 self._age만 정의되는 것으로 볼 수 있지만, 디버깅 해보면 self.age와 Protected Attributes에 self._age까지 같이 정의된다.
즉, 둘 다 사용할 수 있다.)
2. 기존 변수를 이용한 파생 변수(full_name)를 만들 때 주로 사용하며, \_\_init\_\_ 시점에서 생성에 필요한 기존 변수가 정의되면 생성된다. 
django의 Model에서도 사용된다.
