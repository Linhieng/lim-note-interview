这里只记录和算法相关的 py 语法。

## 🍕 其他

在做题过程中，涉及奇偶数，下标，中点时。牢记下面四种情况：
- `n//2`
    ```
       偶数(n=2)      奇数(n=3)
        0  1          0  1  2
           ↑             ↑
    ```
- `n//2 - 1`
    ```
       偶数(n=2)      奇数(n=3)
        0  1          0  1  2
        ↑             ↑
    ```
- `(n+1)//2`
    ```
       偶数(n=2)      奇数(n=3)
        0  1          0  1  2
           ↑                ↑
    ```
- `(n-1)//2`
    ```
       偶数(n=2)      奇数(n=3)
        0  1          0  1  2
        ↑                ↑
    ```

## 🍕 常见的对象及其方法和属性（实现数据结构）。

- 全局函数
    - `len(..)`
    - `map(func, ...)`
    - `list(Iterable)`
    - `input()` 读取一行输入
    - `max(..)`, `min(..)`, `sum(..)`
    - `sorted(.., key=lambda x: 0-x[0])` 降序
    - `round(..)`, `enumerate(..)`, `reversed(..)`
    - `ord(string)`, `chr(number)` 字符和 ASCII 互换
    - `bin(num)` 将数字转换为二进制，格式是字符串
    - 没怎么用到，但感觉不错的
        - `abs(number)`
        - `bin(number)` 返回数字的二进制形式
        - `hex(number)` 返回数字的十六进制形式
        - `divmod(x, y)` 返回 `(x//y, x%y)`
- 字符串
    - `upper()`
    - `lower()`
    - `join(Iterable[str])`
    - `split(sep)` 做算法时，不传入 sep 更好，因为这样会自动丢弃空字符串。
    - `strip()`
    - `replace(old, new)` 返回替换后的字符串
    - `ljust(width, fillchar)`, `rjust()` 填充字符到指定长度。
- `list` 列表
    - `append(object)` 从尾部添加
    - `insert(index, object)` 从指定位置添加
    - `pop(index)` 弹出指定位置元素
    - `reverse()` 反转（可用 `[::-1]` 代替）
    - `index(val)` 找不到时会报错，想要判断是否存在，应该用 `in` 关键字
    - `remove(val)` 删除
- `{}` dict
    - `pop(key)`
    - `keys()`
    - `values()`
    - `get(key, default_value)`

- `from queue import Queue`
    - 完全可以用 `list` 代替
    - `put(val)`
    - `get()`
    - `empty()`
    - 不支持 `len()`
- `from queue import PriorityQueue`
    - `put(val)`
    - `get()` 取出最小值
    - `empty()`
    - 比较对象时，需要对象有提供比较方法（`__lt__`）
- `set`
    - `add(ele)`
    - `pop(ele)`
    - `remove(ele)` 不返回
- `import heapq`
    - `heapify(iterableObj)` 原地修改可迭代对象为小根堆
    - `heappush(iterableObj, val)` 插入新元素, 确保该元素处于正确的位置
    - `heappop(iterableObj)` 弹出最小元素, 同时维持堆
    - `heappushpop(iterableObj, val)` 插入然后返回最小元素
    - `heapreplace(iterableObj, val)` 弹出最小元素然后插入

## 🍕 操作符

- `0 <= x < LEN` py 支持这种写法！

- `//` 运算符
    - 整数除法, 向下取整, 等同于 `int(a / b)`

- `**` 阶乘
    - `a ** 0.5` 求根号很方便

- `[::-1]` 反转列表/数组/字符串
    - 比如 `a[::-1]` 将会返回一个反转后的a
    - 比如 `a[x:] = a[x:][::-1]`
    - 比如 `a[x:y] = a[x:y][::-1]`

- `[0] * num`
    - 创建数组, 注意如果元素是对象, 则不能使用乘号, 得使用推导式
