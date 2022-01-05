# Python 中的优先级队列

> 原文:[https://www.geeksforgeeks.org/priority-queue-in-python/](https://www.geeksforgeeks.org/priority-queue-in-python/)

优先级队列是抽象的数据结构，其中队列中的每个数据/值都有特定的优先级。例如，在航空公司，标题为“商务”或“头等舱”的行李比其他行李更早到达。
优先级队列是队列的扩展，具有以下属性。
1)优先级高的元素在优先级低的元素之前出列。
2)如果两个元素具有相同的优先级，则根据它们在队列中的顺序进行服务。
计算机科学中优先级队列的各种**应用**有:
作业调度算法、中央处理器和磁盘调度、管理不同进程间共享的资源等。

**优先级队列和队列的主要区别:**
1)在队列中，最早的元素先出队。而在优先级队列中，基于最高优先级的元素被出列。
2)当元素从优先级队列中弹出时，得到的结果或者按递增顺序排序，或者按递减顺序排序。而当元素从一个简单的队列中弹出时，会在结果中获得数据的先进先出顺序。

下面是**优先级队列的简单实现**。

```
# A simple implementation of Priority Queue
# using Queue.
class PriorityQueue(object):
    def __init__(self):
        self.queue = []

    def __str__(self):
        return ' '.join([str(i) for i in self.queue])

    # for checking if the queue is empty
    def isEmpty(self):
        return len(self.queue) == 0

    # for inserting an element in the queue
    def insert(self, data):
        self.queue.append(data)

    # for popping an element based on Priority
    def delete(self):
        try:
            max = 0
            for i in range(len(self.queue)):
                if self.queue[i] > self.queue[max]:
                    max = i
            item = self.queue[max]
            del self.queue[max]
            return item
        except IndexError:
            print()
            exit()

if __name__ == '__main__':
    myQueue = PriorityQueue()
    myQueue.insert(12)
    myQueue.insert(1)
    myQueue.insert(14)
    myQueue.insert(7)
    print(myQueue)            
    while not myQueue.isEmpty():
        print(myQueue.delete()) 
```

**Output:**

```
12 1 14 7
14
12
7
1

```

注意，在上面的代码中，delete 的时间复杂度是 O(n)。

一个**更好的实现**是使用[二进制堆](https://www.geeksforgeeks.org/binary-heap/)，它通常用于实现优先级队列。注意 Python 在库也提供 **[heapq](https://www.geeksforgeeks.org/heap-queue-or-heapq-in-python/)** 。

```
By using heap datastructure to implement Priority Queues, Time complexity:
Insert Operation: O(log(n))
Delete Operation: O(log(n))

```