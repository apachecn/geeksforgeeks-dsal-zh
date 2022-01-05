# 队列|集合 1(介绍和数组实现)

> 原文:[https://www . geeksforgeeks . org/queue-set-1 introduction-and-array-implement/](https://www.geeksforgeeks.org/queue-set-1introduction-and-array-implementation/)

与[堆栈](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)一样，[队列](http://en.wikipedia.org/wiki/Queue_%28data_structure%29)是一种线性结构，它遵循执行操作的特定顺序。顺序是 **F** 第一 **I** n **F** 第一 **O** ut(先进先出)。队列的一个很好的例子是资源的消费者队列，其中先到的消费者先被服务。
栈和队列的区别在于移除。在堆栈中，我们移除最近添加的项目；在队列中，我们移除最近添加最少的项目。
**对队列的操作:**
主要对队列进行以下四个基本操作:
**入队:**向队列中添加一个项目。如果队列已满，则称为溢出情况。
**出列:**从队列中移除一个项目。项目按推送的相同顺序弹出。如果队列为空，则称为下溢状态。
**前置:**从队列中获取前置项。
**后方:**从队列中获取最后一项。

![queue](img/a3f253b1dbe832f1e2665a79f5b25dc9.png)

**队列的应用:**
队列用于当事情不必立即处理，而是必须在 **F** 第一个 **I** n **F** 第一个 **O** 中处理时，就像[广度优先搜索](http://en.wikipedia.org/wiki/Breadth-first_search)一样。队列的这个属性使得它在以下场景中也很有用。
**1)** 当一个资源在多个消费者之间共享时。例子包括中央处理器调度，磁盘调度。
**2)** 当数据在两个进程之间异步传输时(数据接收的速率不一定与发送的速率相同)。例子包括输入输出缓冲区、管道、文件输入输出等。
队列和堆栈的更详细应用见[本](http://introcs.cs.princeton.edu/43stack/)。
**队列的数组实现**
为了实现队列，我们需要跟踪前后两个索引。我们在后面排队一个项目，在前面出列一个项目。如果我们简单地增加前面和后面的索引，那么可能会有问题，前面可能会到达数组的末尾。解决这个问题的办法是以循环的方式增加前后。

## C++

```
// CPP program for array
// implementation of queue
#include <bits/stdc++.h>
using namespace std;

// A structure to represent a queue
class Queue {
public:
    int front, rear, size;
    unsigned capacity;
    int* array;
};

// function to create a queue
// of given capacity.
// It initializes size of queue as 0
Queue* createQueue(unsigned capacity)
{
    Queue* queue = new Queue();
    queue->capacity = capacity;
    queue->front = queue->size = 0;

    // This is important, see the enqueue
    queue->rear = capacity - 1;
    queue->array = new int[queue->capacity];
    return queue;
}

// Queue is full when size
// becomes equal to the capacity
int isFull(Queue* queue)
{
    return (queue->size == queue->capacity);
}

// Queue is empty when size is 0
int isEmpty(Queue* queue)
{
    return (queue->size == 0);
}

// Function to add an item to the queue.
// It changes rear and size
void enqueue(Queue* queue, int item)
{
    if (isFull(queue))
        return;
    queue->rear = (queue->rear + 1)
                  % queue->capacity;
    queue->array[queue->rear] = item;
    queue->size = queue->size + 1;
    cout << item << " enqueued to queue\n";
}

// Function to remove an item from queue.
// It changes front and size
int dequeue(Queue* queue)
{
    if (isEmpty(queue))
        return INT_MIN;
    int item = queue->array[queue->front];
    queue->front = (queue->front + 1)
                   % queue->capacity;
    queue->size = queue->size - 1;
    return item;
}

// Function to get front of queue
int front(Queue* queue)
{
    if (isEmpty(queue))
        return INT_MIN;
    return queue->array[queue->front];
}

// Function to get rear of queue
int rear(Queue* queue)
{
    if (isEmpty(queue))
        return INT_MIN;
    return queue->array[queue->rear];
}

// Driver code
int main()
{
    Queue* queue = createQueue(1000);

    enqueue(queue, 10);
    enqueue(queue, 20);
    enqueue(queue, 30);
    enqueue(queue, 40);

    cout << dequeue(queue)
         << " dequeued from queue\n";

    cout << "Front item is "
         << front(queue) << endl;
    cout << "Rear item is "
         << rear(queue) << endl;

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program for array implementation of queue
#include <limits.h>
#include <stdio.h>
#include <stdlib.h>

// A structure to represent a queue
struct Queue {
    int front, rear, size;
    unsigned capacity;
    int* array;
};

// function to create a queue
// of given capacity.
// It initializes size of queue as 0
struct Queue* createQueue(unsigned capacity)
{
    struct Queue* queue = (struct Queue*)malloc(
        sizeof(struct Queue));
    queue->capacity = capacity;
    queue->front = queue->size = 0;

    // This is important, see the enqueue
    queue->rear = capacity - 1;
    queue->array = (int*)malloc(
        queue->capacity * sizeof(int));
    return queue;
}

// Queue is full when size becomes
// equal to the capacity
int isFull(struct Queue* queue)
{
    return (queue->size == queue->capacity);
}

// Queue is empty when size is 0
int isEmpty(struct Queue* queue)
{
    return (queue->size == 0);
}

// Function to add an item to the queue.
// It changes rear and size
void enqueue(struct Queue* queue, int item)
{
    if (isFull(queue))
        return;
    queue->rear = (queue->rear + 1)
                  % queue->capacity;
    queue->array[queue->rear] = item;
    queue->size = queue->size + 1;
    printf("%d enqueued to queue\n", item);
}

// Function to remove an item from queue.
// It changes front and size
int dequeue(struct Queue* queue)
{
    if (isEmpty(queue))
        return INT_MIN;
    int item = queue->array[queue->front];
    queue->front = (queue->front + 1)
                   % queue->capacity;
    queue->size = queue->size - 1;
    return item;
}

// Function to get front of queue
int front(struct Queue* queue)
{
    if (isEmpty(queue))
        return INT_MIN;
    return queue->array[queue->front];
}

// Function to get rear of queue
int rear(struct Queue* queue)
{
    if (isEmpty(queue))
        return INT_MIN;
    return queue->array[queue->rear];
}

// Driver program to test above functions./
int main()
{
    struct Queue* queue = createQueue(1000);

    enqueue(queue, 10);
    enqueue(queue, 20);
    enqueue(queue, 30);
    enqueue(queue, 40);

    printf("%d dequeued from queue\n\n",
           dequeue(queue));

    printf("Front item is %d\n", front(queue));
    printf("Rear item is %d\n", rear(queue));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for array
// implementation of queue

// A class to represent a queue
class Queue {
    int front, rear, size;
    int capacity;
    int array[];

    public Queue(int capacity)
    {
        this.capacity = capacity;
        front = this.size = 0;
        rear = capacity - 1;
        array = new int[this.capacity];
    }

    // Queue is full when size becomes
    // equal to the capacity
    boolean isFull(Queue queue)
    {
        return (queue.size == queue.capacity);
    }

    // Queue is empty when size is 0
    boolean isEmpty(Queue queue)
    {
        return (queue.size == 0);
    }

    // Method to add an item to the queue.
    // It changes rear and size
    void enqueue(int item)
    {
        if (isFull(this))
            return;
        this.rear = (this.rear + 1)
                    % this.capacity;
        this.array[this.rear] = item;
        this.size = this.size + 1;
        System.out.println(item
                           + " enqueued to queue");
    }

    // Method to remove an item from queue.
    // It changes front and size
    int dequeue()
    {
        if (isEmpty(this))
            return Integer.MIN_VALUE;

        int item = this.array[this.front];
        this.front = (this.front + 1)
                     % this.capacity;
        this.size = this.size - 1;
        return item;
    }

    // Method to get front of queue
    int front()
    {
        if (isEmpty(this))
            return Integer.MIN_VALUE;

        return this.array[this.front];
    }

    // Method to get rear of queue
    int rear()
    {
        if (isEmpty(this))
            return Integer.MIN_VALUE;

        return this.array[this.rear];
    }
}

// Driver class
public class Test {
    public static void main(String[] args)
    {
        Queue queue = new Queue(1000);

        queue.enqueue(10);
        queue.enqueue(20);
        queue.enqueue(30);
        queue.enqueue(40);

        System.out.println(queue.dequeue()
                           + " dequeued from queue\n");

        System.out.println("Front item is "
                           + queue.front());

        System.out.println("Rear item is "
                           + queue.rear());
    }
}

// This code is contributed by Gaurav Miglani
```

## 蟒蛇 3

```
# Python3 program for array implementation of queue

# Class Queue to represent a queue
class Queue:

    # __init__ function
    def __init__(self, capacity):
        self.front = self.size = 0
        self.rear = capacity -1
        self.Q = [None]*capacity
        self.capacity = capacity

    # Queue is full when size becomes
    # equal to the capacity
    def isFull(self):
        return self.size == self.capacity

    # Queue is empty when size is 0
    def isEmpty(self):
        return self.size == 0

    # Function to add an item to the queue.
    # It changes rear and size
    def EnQueue(self, item):
        if self.isFull():
            print("Full")
            return
        self.rear = (self.rear + 1) % (self.capacity)
        self.Q[self.rear] = item
        self.size = self.size + 1
        print("% s enqueued to queue"  % str(item))

    # Function to remove an item from queue.
    # It changes front and size
    def DeQueue(self):
        if self.isEmpty():
            print("Empty")
            return

        print("% s dequeued from queue" % str(self.Q[self.front]))
        self.front = (self.front + 1) % (self.capacity)
        self.size = self.size -1

    # Function to get front of queue
    def que_front(self):
        if self.isEmpty():
            print("Queue is empty")

        print("Front item is", self.Q[self.front])

    # Function to get rear of queue
    def que_rear(self):
        if self.isEmpty():
            print("Queue is empty")
        print("Rear item is",  self.Q[self.rear])

# Driver Code
if __name__ == '__main__':

    queue = Queue(30)
    queue.EnQueue(10)
    queue.EnQueue(20)
    queue.EnQueue(30)
    queue.EnQueue(40)
    queue.DeQueue()
    queue.que_front()
    queue.que_rear()
```

## C#

```
// C# program for array implementation of queue
using System;

namespace GeeksForGeeks {
// A class to represent a linearqueue
class Queue {
    private int[] ele;
    private int front;
    private int rear;
    private int max;

    public Queue(int size)
    {
        ele = new int[size];
        front = 0;
        rear = -1;
        max = size;
    }

    // Function to add an item to the queue.
    // It changes rear and size
    public void enqueue(int item)
    {
        if (rear == max - 1) {
            Console.WriteLine("Queue Overflow");
            return;
        }
        else {
            ele[++rear] = item;
        }
    }

    // Function to remove an item from queue.
    // It changes front and size
    public int dequeue()
    {
        if (front == rear + 1) {
            Console.WriteLine("Queue is Empty");
            return -1;
        }
        else {
            Console.WriteLine(ele[front] + " dequeued from queue");
            int p = ele[front++];
            Console.WriteLine();
            Console.WriteLine("Front item is {0}", ele[front]);
            Console.WriteLine("Rear item is {0} ", ele[rear]);
            return p;
        }
    }

    // Function to print queue.
    public void printQueue()
    {
        if (front == rear + 1) {
            Console.WriteLine("Queue is Empty");
            return;
        }
        else {
            for (int i = front; i <= rear; i++) {
                Console.WriteLine(ele[i] + " enqueued to queue");
            }
        }
    }
}

// Driver code
class Program {
    static void Main()
    {
        Queue Q = new Queue(5);

        Q.enqueue(10);
        Q.enqueue(20);
        Q.enqueue(30);
        Q.enqueue(40);
        Q.printQueue();
        Q.dequeue();
    }
}
}
```

**输出:**

```
10 enqueued to queue
20 enqueued to queue
30 enqueued to queue
40 enqueued to queue
10 dequeued from queue
Front item is 20
Rear item is 40
```

**复杂度分析:**

*   **时间复杂度:**

```
Operations              Complexity
Enque(insertion)           O(1)
Deque(deletion)            O(1)
Front(Get front)           O(1)
Rear(Get Rear)             O(1)              
```

*   **辅助空间:** O(N)。
    N 是存储元素的数组大小。

阵列实施的优势:

1.  易于实施。

阵列实施的缺点:

1.  静态数据结构，固定大小。
2.  如果队列有大量的入队和出队操作，在某个时刻(前后索引线性递增的情况下)，即使队列为空，我们也可能无法在队列中插入元素(通过使用循环队列可以避免这个问题)。

链表实现比较容易，这里讨论: [Queue | Set 2(链表实现)](https://www.geeksforgeeks.org/queue-linked-list-implementation/)
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息。