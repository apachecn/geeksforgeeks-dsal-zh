# Python 中使用`OrderedDict`的 LRU 缓存

> 原文：[https://www.geeksforgeeks.org/lru-cache-in-python-using-ordereddict/](https://www.geeksforgeeks.org/lru-cache-in-python-using-ordereddict/)

[LRU（最久未使用）缓存](https://www.geeksforgeeks.org/lru-cache-implementation/)首先丢弃最近最少使用的项目。 此算法需要跟踪何时使用了什么，如果要确保算法始终丢弃最近最少使用的商品，这将非常昂贵。 此技术的一般实现要求保留高速缓存行的“年龄位”，并根据年龄位跟踪“最近最少使用”的高速缓存行。

我们的问题陈述是为最近最少使用（LRU）缓存设计和实现数据结构。

它应支持以下操作：获取和放置。

* `get(key)`：如果密钥存在于缓存中，则获取密钥的值（始终为正），否则返回 -1。

* `put(key, value)`：如果密钥不存在，则设置或插入该值。 当缓存达到其容量时，它应在插入新项目之前使最近最少使用的项目无效。

缓存始终以正容量初始化。

**示例**：

```
Input/Output : 
LRUCache cache = new LRUCache( 2 /* capacity */ );

cache.put(1, 1);                                    
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.put(4, 4);    // evicts key 1
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4

```

我们的解决方案是使用来自`collections`模块的[`OrderedDict`](https://www.geeksforgeeks.org/ordereddict-in-python/)的功能来保持键插入的顺序，并且如果需要，我们可以更改该顺序。 最好的部分是所有操作的时间复杂度为`O(1)`。

我们以这样的方式维护`OrderedDict`：顺序显示了最近使用它们的方式。 首先，我们将使用最少的东西，最后使用最近的东西。

如果对某个键进行任何更新或查询，它将移至末尾（最近使用）。 如果添加了任何内容，则将其添加到末尾（最近使用/添加的）

对于`get(key)`：我们返回在`O(1)`中查询的键的值，如果不返回，则返回-1。 找不到输入字典/缓存中的密钥。 并将密钥移到末尾以表明它最近被使用过。

对于`put(key, value)`：首先，我们通过常规方法添加/更新密钥。 并将密钥移到末尾以表明它最近被使用过。 但是在这里，我们还将检查订购字典的长度是否超过了我们的能力，如果是，我们将删除第一把键（最近最少使用的键）

## Python3

```py

from collections import OrderedDict

class LRUCache:

    # initialising capacity
    def __init__(self, capacity: int):
        self.cache = OrderedDict()
        self.capacity = capacity

    # we return the value of the key
    # that is queried in O(1) and return -1 if we
    # don't find the key in out dict / cache.
    # And also move the key to the end
    # to show that it was recently used.
    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1
        else:
            self.cache.move_to_end(key)
            return self.cache[key]

    # first, we add / update the key by conventional methods.
    # And also move the key to the end to show that it was recently used.
    # But here we will also check whether the length of our
    # ordered dictionary has exceeded our capacity,
    # If so we remove the first key (least recently used)
    def put(self, key: int, value: int) -> None:
        self.cache[key] = value
        self.cache.move_to_end(key)
        if len(self.cache) > self.capacity:
            self.cache.popitem(last = False)

# RUNNER
# initializing our cache with the capacity of 2
cache = LRUCache(2) 

cache.put(1, 1)
print(cache.cache)
cache.put(2, 2)
print(cache.cache)
cache.get(1)
print(cache.cache)
cache.put(3, 3)
print(cache.cache)
cache.get(2)
print(cache.cache)
cache.put(4, 4)
print(cache.cache)
cache.get(1)
print(cache.cache)
cache.get(3)
print(cache.cache)
cache.get(4)
print(cache.cache)

#This code was contributed by Sachin Negi

```

**Output:** 

```
OrderedDict([(1, 1)])
OrderedDict([(1, 1), (2, 2)])
OrderedDict([(2, 2), (1, 1)])
OrderedDict([(1, 1), (3, 3)])
OrderedDict([(1, 1), (3, 3)])
OrderedDict([(3, 3), (4, 4)])
OrderedDict([(3, 3), (4, 4)])
OrderedDict([(4, 4), (3, 3)])
OrderedDict([(3, 3), (4, 4)])

```

时间复杂度：`O(1)`

[LRU](https://www.geeksforgeeks.org/lru-cache-implementation/)

的其他实现



* * *

* * *



