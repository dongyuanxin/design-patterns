---
title: "策略模式"
---

## 1. 什么是策略模式？

> 策略模式定义：就是能够把一系列“可互换的”算法封装起来，并根据用户需求来选择其中一种。

策略模式**实现的核心**就是：将算法的使用和算法的实现分离。
  - 算法的实现交给策略类。
  - 算法的使用交给环境类，环境类会根据不同的情况选择合适的算法。

## 2. 策略模式优缺点

在使用策略模式的时候，需要了解所有的“策略”（strategy）之间的异同点，才能选择合适的“策略”进行调用。

## 3. 代码实现

### 3.1 ES6 实现

```javascript
// 策略类
const strategies = {
  A() {
    console.log("This is stragegy A");
  },
  B() {
    console.log("This is stragegy B");
  }
};

// 环境类
const context = name => {
  return strategies[name]();
};

// 调用策略A
context("A");
// 调用策略B
context("B");
```

### 3.2 python3 实现

```python
class Stragegy():
  # 子类必须实现 interface 方法
  def interface(self):
    raise NotImplementedError()

# 策略A
class StragegyA():
  def interface(self):
    print("This is stragegy A")

# 策略B
class StragegyB():
  def interface(self):
    print("This is stragegy B")

# 环境类：根据用户传来的不同的策略进行实例化，并调用相关算法
class Context():
  def __init__(self, stragegy):
    self.__stragegy = stragegy()
  
  # 更新策略
  def update_stragegy(self, stragegy):
    self.__stragegy = stragegy()
  
  # 调用算法
  def interface(self):
    return self.__stragegy.interface()


if __name__ == "__main__":
  # 使用策略A的算法
  cxt = Context( StragegyA )
  cxt.interface()

  # 使用策略B的算法
  cxt.update_stragegy( StragegyB )
  cxt.interface()
```


## 4. 参考

- [策略模式-Python四种实现方式](https://zhuanlan.zhihu.com/p/30576518)
- [Python设计模式 - 策略模式](http://www.isware.cn/python-design-pattern/03-strategy/)
- 《JavaScript设计模式和开发实践》
