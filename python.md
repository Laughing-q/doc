- `CfgNode`使字典可以通过对象的方式访问属性
```python
from yacs.config import CfgNode
```

- `unique`枚举避免重复属性
```python
from enum import unique
@unique
class A:
  a = 1
  b = 2
  c = 2  # 会出错
```

- `IntEnum`枚举必须为整数
```python
from enum import IntEnum
@unique
class A(IntEnum):
  a = 1
  b = 2
```
- `staticmethod`和`classmethod`
  - 静态变量，或者静态方法，也叫类变量、类方法，与一般的实例变量区别在于，它是类共有的，可以通过类名直接访问，并且永远保持着最新修改的值
  - 而成员变量则是类实例特有的一个副本，通过类的实例进行访问，当前类实例修改了成员变量的值只会对本实例有用，并不会影响其他类实例所持有的变量的值
  - 如果使用`@staticmethod`来装饰一个方法，则不需要传递self，**外部访问时可以直接通过类名进行访问**
  - 如果使用`@classmethod`来装饰一个方法，不需要传递self，但需要传递一个cls来代表自身类，**外部访问时可以直接通过类名进行访问**
  ```python
  class demo(object):
   
      __c = 10; # 定义一个private的变量
   
      def get_c(self):
          print self.__c
          return self.__c
   
      def add(self,a):
          """
          这个是普通方法，我们改变了一次__c的值，但这只对当前的类实例有效
          :param a:
          :return:
          """
          self.__c = 11
          return self.__c + a
   
      @staticmethod
      def add2(a):
          """
          这是一个静态方法，我们改变了一次__c的值，这个改变对所有类实例都有效
          :param a:
          :return:
          """
          demo.__c = 12 # 改变了__c的值
          return demo.__c + a
   
      @classmethod
      def add3(cls,a):
          """
          这是一个类方法，我们改变了一次__c的值，这个改变对所有类实例都有效
          :param a:
          :return:
          """
          cls.__c = 13 # 改变了__c的值
          return cls.__c + a
  ```

## Numpy
- `np.roll(x, shift, axis=None)`
  * 滚动数组
  * `shift`为滚动偏移
  * `axis`为轴，0则垂直滚动，1则水平滚动，默认None则先将数组扁平化再滚动再还原

## Torch
- `torch.where(condition)` 与`torch.nonzero(condition, as_tuple=True)`等价, 找到非0元素的索引.

