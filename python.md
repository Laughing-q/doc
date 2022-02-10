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

