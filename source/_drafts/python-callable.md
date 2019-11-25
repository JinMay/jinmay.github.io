---
title: python-callable
categories:
  - python
---

# 파이썬의 __call__ 함수

더블 언더스코어(__)로 시작하는 매직메소드를 통해 클래스가 특별한 동작을 수행할 수 있도록 만들 수 있다. 함수를 호출하는 것처럼 클래스의 객체도 호출할 수 있게 만들수 있는데 이때 필요한 매직메소드가 **__call__**이다.  

리스트에서 랜덤하게 번호를 추출하는 기능을 인스턴스 메소드와 객체 호출 두 가지 방법으로 구현하면서 __call__ 함수에 대해서 정리하자.

## 인스턴스 메소드로 구현하기

~~~python
import random

class RandomPick:

  def __init__(self):
    self._numbers = [n for n in range(1, 101)]
  
  def pick(self):
    random.shuffle(self._numbers)
    return sorted([random.choice(self._numbers) for _ in range(10)])    

obj = RandomPick()
print(obj.pick())
~~~

## 객체 호출로 구현하기

~~~python
def __call__(self):
  return self.pick()

a = RandomPick()
a() # [7, 9, 10, 11, 36, 37, 52, 71, 80, 100]
a.pick() # [4, 18, 31, 36, 46, 50, 52, 70, 93, 94]
~~~

위의 __call__ 함수를 추가해주면된다.  

## 객체가 호출가능한지 판단하기

callable 함수를 써서 해당 객체가 호출 가능한지 판단할 수 있다.

~~~python
class A:
  def __call__(self):
    return 'haha'

class B:
  pass

a = A()
b = B()

callable(a) # True
callable(b) # False
~~~


