---
title: Python/Decorator
alias:
  - 装饰器
public: true
tags:
date: 2024-10-05
updated: 2024-10-05
toc: true
mathjax: true
---

最终返回嵌套函数的引用

  + 覆盖 `__name__` 和 `__code__`

不修改原函数，不修改调用方法。通过标记，^^增强函数功能^^

  + 为已经存在的对象(函数和类)添加额外的功能

  + 函数修饰器在导入模块时立即执行，被装饰函数只在明确调用时运行。

`@` 装饰器[[语法糖]]

  + 等价于 add = timer(add)

```python
def timer(func):
  def wrapper(*arg, **kw):
    ### code
    return func(*arg, **kw)
  return wrapper

@timer
def add(arg):
  pass
```

标准库中的装饰器

  + `lru_cache` 把耗时的函数结果保存起来

    + 字典存储结果，键是传入的定位参数和关键字参数

  + 单分派泛函数 `functools.singledispatch` PEP 443

    + Python 不支持重载方法或函数

    + 使用这个装饰器后根据第一个参数的类型执行对应的函数。

    + `@singledispatch` 标记基函数

    + `@base_function.register(type)`装饰专门的函数

      + type 使用抽象基类

  + `@staticmathod`

  + `@classmethod`

  + `@property`

叠放装饰器，按叠放顺序执行

```python
@a
@b
@c
def f ():
```

  + 等价于 `f = a(b(c(f)))`

参数化装饰器

  + 
