# 使用队列模块

在 Python 中堆叠和排队

> 原文:[https://www . geesforgeks . org/stack-queue-python-using-module-queue/](https://www.geeksforgeeks.org/stack-queue-python-using-module-queue/)

一个简单的 python 列表也可以充当队列和堆栈。队列机制在日常生活中被广泛使用并有许多用途。队列遵循先进先出规则，在编程中用于排序和许多其他事情。Python 提供类队列作为一个模块，通常必须用 C/C++和 Java 等语言创建。

**1。创建先进先出队列**

```
// Initialize queue
Syntax: queue.Queue(maxsize)

// Insert Element
Syntax: Queue.put(data)

// Get And remove the element
Syntax: Queue.get()

```

将变量初始化为最大大小 maxsize。最大大小为零“0”意味着无限队列。该队列遵循先进先出规则。这个模块还有一个后进先出队列，基本上是一个堆栈。使用 put()和 end 将数据插入队列。get()从队列的前面取出数据。请注意，put()和 get()都需要另外两个参数，可选标志、阻塞和超时。

```
import queue

# From class queue, Queue is
# created as an object Now L
# is Queue of a maximum 
# capacity of 20
L = queue.Queue(maxsize=20)

# Data is inserted into Queue
# using put() Data is inserted
# at the end
L.put(5)
L.put(9)
L.put(1)
L.put(7)

# get() takes data out from
# the Queue from the head 
# of the Queue
print(L.get())
print(L.get())
print(L.get())
print(L.get())
```

输出:

```
5
9
1
7

```

**2。下溢和上溢**
当我们试图将数据添加到 maxsize 以上的队列中时，它被称为上溢(Queue Full)，当我们试图从空队列中移除元素时，它被称为下溢。put()和 get()在上溢和下溢时不会产生错误，而是进入无限循环。

```
import queue

L = queue.Queue(maxsize=6)

# qsize() give the maxsize
# of the Queue
print(L.qsize())

L.put(5)
L.put(9)
L.put(1)
L.put(7)

# Return Boolean for Full
# Queue
print("Full: ", L.full())

L.put(9)
L.put(10)
print("Full: ", L.full())

print(L.get())
print(L.get())
print(L.get())

# Return Boolean for Empty
# Queue
print("Empty: ", L.empty())

print(L.get())
print(L.get())
print(L.get())

print("Empty: ", L.empty())
print("Full: ", L.full())

# This would result into Infinite
# Loop as the Queue is empty.
# print(L.get())
```

输出:

```
0
Full:  False
Full:  True
5
9
1
Empty:  False
7
9
10
Empty:  True
Full:  False

```

**3。堆栈**
这个模块队列还提供了后进先出队列，从技术上来说，这是一个堆栈。

```
import queue

L = queue.LifoQueue(maxsize=6)

# qsize() give the maxsize of
# the Queue
print(L.qsize())

# Data Inserted as 5->9->1->7, 
# same as Queue
L.put(5)
L.put(9)
L.put(1)
L.put(7)
L.put(9)
L.put(10)
print("Full: ", L.full())
print("Size: ", L.qsize())

# Data will be accessed in the
# reverse order Reverse of that
# of Queue
print(L.get())
print(L.get())
print(L.get())
print(L.get())
print(L.get())
print("Empty: ", L.empty())
```

输出:

```
0
Full:  True
Size: 6
10
9
7
1
9
Empty:  False

```

**参考:**T2[https://docs.python.org/3/library/asyncio-queue.html](https://docs.python.org/3/library/asyncio-queue.html)