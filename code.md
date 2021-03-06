## 面向对象
- 封装
- 继承
- 多态
  * python是多态语言

- 接口
  * 若干抽象方法的集合
  * 接口的作用是限制实现接口的类必须按照接口给定的调用方式实现这些方法
  * 对高层模块隐藏了类的内部实现

### 面向对象设计的SOLID原则
- 开放封闭原则
  * 一个软件实体如类、模块和函数应该对扩展开放，对修改关闭。即软件实体应该在不修改原代码的情况下进行修改
- 里氏替换原则
  * 所有引用父类的地方必须能够透明的使用其子类
  * 子类实现函数的参数和返回值需要与父类一致
- 依赖倒置原则
  * 高层不应该依赖底层模块
  * 二者都应该依赖其抽象
  * 抽象不应该依赖细节
  * 细节应该依赖抽象
  * 要针对接口编程，而不是针对实现编程
- 接口隔离原则
  * 使用多个专门的接口，而不使用单一的总接口
  * 高层的代码不应该依赖那些它不需要的接口
- 单一职责原则
  * 不让存在多于一个导致类变更的原因
  * 即一个类只负责一项职责

## 设计模型分类
- 创建型模式
  * 怎样创建一个对象
  * 隐藏底层模块的逻辑
- 结构型模式
  * 几个类之间的协同工作
- 行为型模式
  * 类，方法的行为

### 创建型模式
