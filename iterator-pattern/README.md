---
title: "迭代器模式"
---

## 1. 什么是迭代器模式？

> 迭代器模式是指提供一种方法顺序访问一个集合对象的各个元素，使用者不需要了解集合对象的底层实现。

## 2. 内部迭代器和外部迭代器

内部迭代器：封装的方法完全接手迭代过程，外部只需要一次调用。

外部迭代器：用户必须显式地请求迭代下一元素。熟悉C++的朋友，可以类比C++内置对象的迭代器的 `end()`、`next()`等方法。

## 3. 代码实现

### 3.1 ES6 实现

这里实现的是一个外部迭代器。需要实现边界判断函数、元素获取函数和更新索引函数。

```javascript
const Iterator = obj => {
  let current = 0;
  let next = () => current += 1;
  let end = () => current >= obj.length;
  let get = () => obj[current];

  return {
    next,
    end,
    get
  }
}

let myIter = Iterator([1, 2, 3]);
while(!myIter.end()) {
  console.log(myIter.get())
  myIter.next();
}
```

### 3.2 python3 实现

python3的迭代器可以用作`for()`循环和`next()`方法的对象。同时，在实现迭代器的时候，可以在借助生成器`yield`。python会生成传给`yeild`的值。

```python
def my_iter():
  yield 0, "first"
  yield 1, "second"
  yield 2, "third"

if __name__ == "__main__":
  # 方法1: Iterator可以用for循环
  for (index, item) in my_iter():
    print("At", index , "is", item)
  
  # 方法2: Iterator可以用next()来计算
  # 需要借助 StopIteration 来终止循环
  _iter = iter(my_iter())
  while True:
    try:
      index,item = next(_iter)
      print("At", index , "is", item)
    except StopIteration:
      break
```

## 4. 参考资料

- [python迭代器](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/00143178254193589df9c612d2449618ea460e7a672a366000)

- 《JavaScript 设计模式和开发实践》