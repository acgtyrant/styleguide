## 库

Numpy 里，[尽量避免会导致复制的函数](http://ipython-books.github.io/featured-01/)：对新变量赋运算结果的值（可以用 inplace 运算代替）；`T`；`flattern`（可以用 `ravel` 代替），fancy indexing（用 array view 或 `take` 或 `compress` 代替）。

用 `subprocess.call` 代替 `os.system` 执行外部命令。

[用 `pathlib` 解析 Path](http://tech.acgtyrant.com/御用-Path-规范/), 除非要用 `os.path` 解析 str 对象。

用 `typing` 来提供高级的 type hints, 比如 Tuple 和 Mapping 等。

[用 `logging` 代替 print 调试](http://victorlin.me/posts/2012/08/26/good-logging-practice-in-python)。

靠 `json.dumps(data, indent=2)` 来得到可读性好的 json.

可以用 `funtools.total_ordering` 简化编写所有比较魔法方法的工作，除非变成瓶颈。

可以用 `functools.partial` 特化函数，以塞进函数接口。

[加入马戏团，刷魔术方法](http://www.rafekettler.com/magicmethods.html)

## 2to3

`range`, `map`, `filter`, `reduce` 在 Python 3 里均是生成器返回的 iterator, 必要时要转换为 list; Python 2 里则是 list.

Python 2 enconding: `# coding=utf-8`

Python 2 必须同时定义 `__eq__` 和 `__ne__` 方法，Python 3 则只定义其中一个即可。

## 其他

不用 `==` 比较不同类型的值，但 `is` 可以。

比起 `import foo.bar as bar`, 优先用 `from foo import bar`, 毕竟前者不能导入非 package 或 module, 后者还少几个字，按奥卡母剃刀，优先选后者。


始终要对字符串是否包含换行符而胸有成竹。凡 identifier 是 `line`, 就必有回车符；分拆 line 或打印或 log 时，就要 `rstrip('\n')`; 同理，用 `format` 构造 `line` 时，就要在尾部显示加上回车符，除非最有一个参数是 `line`.

TODO: 有待规范 Python 中异常与 option 之间的关系。

当在 if 表达式判断两个对象是否相等，用 `if _1 == _2` 即可；当判断两个对象是否同一个，用 `if _1 is _2`. 当判断对象 `_` 是否为 None 时，不要用 `if not _`, 而是 `if _ is None`.

[Python天坑系列（一）：while 1比while True更快？](http://www.pythoner.com/356.html)简而言之，用 Python 3 啦！

TODO: http://nvie.com/posts/writing-a-cli-in-python-in-under-60-seconds/ 有待吸纳自动化工具。

[如同蛇一般地赋值](http://blog.windrunner.info/python/assignment.html#python-中的赋值) ：交换变量：`a, b = b, a`.可以用 `_` 用来接收我们不需要关心的变量，当然禁止产生赋值之外的任何行为；其实同一条赋值语句可以反复还使用 `_`: `_, _ = 1, 2`. 再配合星号 unpacking, 用 `*_` 一口气抛弃掉其他多余的返回值： `a, *_ = some_str.split()`（黑魔法施展状

直接链式比较 `0 < a < 2`，不再分拆成多个子比较表达式。

可以通过切片来删除序列的一部分。

若要在 `except` 语句捕获众多异常，把它们括号起来成 tuple.

小心 lambda 的 late binding 行为。

要么改用 Python 标准库，要么写名字与前者不冲突的新模块。

[传入模块名用 `fullename`](https://laike9m.com/blog/useful-hacklazy-module-attribute,68/).

有必要时可以用 try/else 代替 with; [try 可以包含 return 语句，finally 照样会在之后被执行](http://stackoverflow.com/questions/7442133/try-else-with-return-in-try-block/7442252#7442252)。

善用 [all/any]*(http://treyhunner.com/2016/11/check-whether-all-items-match-a-condition-in-python/).

[有待贯彻 Python 3.6 新语法糖]*(https://medium.com/the-python-corner/syntax-sugar-in-python-3-6-776178ce51f4#.mgeqydith)

可以使用官方都提倡的命名缩写，比如 `import matplotlib.pyplot as plt`, `import numpy as np` 等。

shebang 里的 python 必须有明确的版本后缀，除非真打算同时支持 Python 2/3.

## 内存优化

[如果有大量类对象，其 attributes 又少。可以考虑用 `__slots__` 来构造 attributes, 其访问速度快 30%, 又避免了类 dict 耗费大量内存空间的弊端。

考虑用 namedtupls 代替类，其特点自然是 immutable 且无方法。](https://oded.ninja/2016/11/30/__slots__-and-namedtuples/)

## [用 __all__ 暴露接口](https://python-china.org/t/725)

## [Python: The Dictionary Playbook](http://blog.amir.rachum.com/blog/2013/01/02/python-the-dictionary-playbook/)

#### The "Are You There?"

Bad:

```python
dct.has_key(key)
```

Good:

```python
key in dict
```

#### The "Yoda Test"

Bad:

```
not key in dict
```

Good:

```python
key not in dict
```

#### The "Get The Value Anyway"

Bad:

```python
if key not in dct:
    dct[key] = 0
dct[key] = dct[key] + 1

Good:

```python
dct[key] = dct.get(key, 0) + 1
```

#### The "Make it Happen"

`collection.defaultdict` 可以接收 list, 一次性生成有默认 value 为 list 的 dict.

## Effective Python

#### 第一条

休闲开发不用 Python 2, 即只用 Arch Linux 上最新的 Python 3; 默认实现用 CPython, 与 C/C++ 交互时考虑用 Cython, 高性能实现考虑用 PyPy; 也许可以用 docker 管理虚拟环境。

#### 第二条

遵循 PEP 8. Google Python Style 无关紧要，除非为 Google 效力。

TODO: 有待总结 PEP 8.

#### 第三条

[Python-语法、进程和文件之间的编码关系](http://tech.acgtyrant.com/Python-语法、进程和文件之间的编码关系/)

#### 第四条

多用辅助函数代替复杂的表达式；if/else 语句比 or/and 表达式更清晰。

#### 第五条

切片时，当 start 为 0 或 end 为序列长度时，省略。

#### 第六条

切片时，stride 尽量只用正数；**不要同时用上 start, end 和 stride. 可以分拆成两个赋值语句，一个范围切割另一个步进切割。**

#### 第七条

用列表推导代替需要额外 lambda 的 `map`. 用支持 if 语句的列表推导代替 `map` 与 `filter.`; 不光列表推导，我们也可以习惯于集合推导和字典推导；不过[ map 有时比 list comprehension 好](http://tech.acgtyrant.com/什么情况下-map-比-list-comprehension-好？/)

#### 第八条

不要在列表推导的同一级循环用多重 if 表达式，而是用 and 合并为一个 if 表达式；**不要在列表推导用两个以上循环。**

#### 第九条

习惯用生成器表达式代替一切，除非需要用到全局的 iterable.

#### 第十条

`enumerate` 函数可以返回迭代器的生成器，且后者每次迭代时返回索引值和对应的值。于是用它代替将 `range` 与下标访问相结合的序列遍历代码，即 `range(len(iterable))`; 此外 `enumerate` 的第二个参数可以指定最初索引值。

#### 第十一条

**用 `zip` 平行地迭代两个列表**；Python 2 用 `itertools.izip` 作为生成器表达式；确保两个迭代起长度相等！

#### 第十二条

不要在循环语句后用 else 语句。

#### 第十三条

**无论 try 语句是否发生异常，都可以在 finally 语句执行清理工作，相应地 `open` 之类的函数就要放在 try 之外；把 try 块中不会抛异常的语句挪到 else 块；顺序按 try/except/else/finally.**

#### 第十四条

当调用者违背了函数调用的约定。要么采用人造的 option type 手法，我们只能如此返回一个二元组，第一个元素标识操作是否成功，第二个元素则是运算结果值，此外也可以用利用 Python 3.5 的 type hints; 要么干脆扔回异常。后者的措辞更为激烈。

#### 第十五条

尽量不要在闭包修改外部作用域的变量，否则就用 `nonlocal` 声明，或是封装成更好的类；同理，在函数内部用 `global` 声明模块作用域的变量。别痴心妄想地在闭包或函数修改模块全局作用域甚至内置作用域的变量；Python 2 不支持 `nonlocal`, 可以用列表封装所要修改的变量。

#### 第十六条

迭代时，能用生成器表达式就用。

#### 第十七条

**若只迭代一遍，可以直接用生成器表达式的迭代器；否则就用类的 `__iter__()` 函数封装生成器表达式成容器；可以通过调用两次 `iter()` 来判断对象是迭代器或容器。**

#### 第十八条

用 `args` 声明代表数量可变的位置参数；实际传的 `*args` 应较少；如果函数接收 `*args` 参数，就不要随便添加位置参数。

#### 第十九条

**位置参数必须出现在关键字参数之前；每个参数只能指定一次；可以在函数的形参或实参用关键字参数，来增强可读性；可以靠有默认值的关键字参数来安全地添加形参。**

#### 第二十条

若要设置关键字参数为动态的默认值，则先指定默认值为 `None`, 然后再在函数内部动态地赋新值，必要时再在文档字符串说明其行为；不要在形参用 `[]` 或 `{}` 之类的默认值。

#### 第二十一条

若要强制调用者用关键字参数形式声明实参，可以通过 Python 3 的 `*` 语法或 Python 2 的 `**kwargs` 并手工抛 TypeError 手法实现。

#### 第三十六条

比起 popen, popen2, os.exec*, 优先用 subprocess 模块管理子进程和其 IO; 可以给 communicate 方法传入 timeout 参数以定 deadline.

#### 第三十七条

老生常谈的 GIL 之咒；所以多线程只适合加速 IO 密集计算。

#### 第三十八条

#### 第四十一条

平行计算方案优先级递减：concurrent.future.ProcessPoolExecutor > concurrent.future.ThreadPoolExecutor > multiprocess > c module.

#### 第四十二条

为了在修饰函数后保留原函数的某些标准 Python 属性，可以再用 `functools.wraps()` 来修饰。

#### 第四十三条

可以用 `contextlib` 模块编写类的 `__enter__` 或 `__exit__` 函数来提供对 `with` 语句的支持，不过还可以用 `contextlib.contextmanager` 来直接装饰，它能通过 `yield` 语句向 `with` 语句返回一个由 `as` 关键字所接收的值；用 `with` 管理文件，包括打开并读取。

#### 第四十四条

`pickle` 模块只能在受信任的程序之间通讯用；#TODO 

#### 第四十五条

可以通过 `time.strftime(format)` 来快速得到当地时间；通过 `datetime` 和 `pytz` 模块来在不同时区转换时间；在转换时间前，先统一转换到 UTC 格式。

#### 第四十六条

`collections.namedtuple` 可以构造 named tuple 对象；`collections.defaultdict` 可以构造默认值为类的字典，比如 `collections.defaultdict(list)`; 用 collections.deque 当双端队列，不要用 list; dict 是无序的，用 `collections.OrderedDict` 当有序字典；用 `heapq` 模块实现优先级队列；用  `bisect.bisect_left` 二分查找；妙用 `itertools` 模块，**详阅正文，此处略**。

#### 第四十七条

用 `decimal` 或 `fractions` 来高精度计算。前者的精度有限，后者无限。

#### 第四十八条

御用包管理器首先是 Arch Linux 的包管理器 pacman, 其次才是 PyPI 官方的 pip.

#### 第四十九条

精华篇幅不小，请**详阅正文，此处略**。

#### 第五十条

#### 第五十一条

#### 第五十三条

必要时，用 pyenv 隔离软件包的开发环境；靠 `pip freeze` 保存依赖关系到 `requirements.txt`; 

### 第八章

#### 第五十四条

可以直接在模块作用域编写常规 Python 语句，来根据不同的部署环境来定制本模块的行为，可以利用 `sys` 和 `os` 模块。

#### 第五十五条

用 `print()` 默认打印对象的 `__str__` 属性，后者重在可读。且也可以调用 `__repr__` 属性作为代替，其重在准确；可以用 `eval()` 还原 repr 字符串为初始的值；格式化字符串中可以分别用 `%s`/`%r` 来产生 str/repr 相近的字符串；被调用者可以在类内自定义 `__repr__` 来提供调试信息，调用者也可以反过来用 `__dict__` 观察。

#### 第五十六条

靠单元测试和集成测试来保证 Python 程序的正常运行，弥补动态语言的缺陷；靠 `unittest` 模块和 `unittest.TestCase` 对象。

#### 第五十七条

靠 IPython 和 pdb 来断点测试。

#### 第五十八条

靠 `cProfile` 模块来 profile.
