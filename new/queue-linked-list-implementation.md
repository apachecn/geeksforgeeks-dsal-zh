# 队列–链表实现

> 原文：[https://www.geeksforgeeks.org/queue-linked-list-implementation/](https://www.geeksforgeeks.org/queue-linked-list-implementation/)

在[之前的文章](http://quiz.geeksforgeeks.org/queue-set-1introduction-and-array-implementation/)中，我们介绍了 Queue 并讨论了数组实现。 在这篇文章中，讨论了链表的实现。 必须有效执行以下两个主要操作。

在[队列数据结构](https://www.geeksforgeeks.org/queue-data-structure/)中，我们维护两个指针，即*前*和*后*。 *前*指向队列的第一项，*后*指向最后的队列。

**enQueue（）**此操作在*后*后添加一个新节点，并将*后*后移到下一个节点。

**deQueue（）**此操作删除前节点，并将*前*移动到下一个节点。

## C++

```cpp

#include <bits/stdc++.h> 
using namespace std; 

struct QNode { 
    int data; 
    QNode* next; 
    QNode(int d) 
    { 
        data = d; 
        next = NULL; 
    } 
}; 

struct Queue { 
    QNode *front, *rear; 
    Queue() 
    { 
        front = rear = NULL; 
    } 

    void enQueue(int x) 
    { 

        // Create a new LL node 
        QNode* temp = new QNode(x); 

        // If queue is empty, then 
        // new node is front and rear both 
        if (rear == NULL) { 
            front = rear = temp; 
            return; 
        } 

        // Add the new node at 
        // the end of queue and change rear 
        rear->next = temp; 
        rear = temp; 
    } 

    // Function to remove 
    // a key from given queue q 
    void deQueue() 
    { 
        // If queue is empty, return NULL. 
        if (front == NULL) 
            return; 

        // Store previous front and 
        // move front one node ahead 
        QNode* temp = front; 
        front = front->next; 

        // If front becomes NULL, then 
        // change rear also as NULL 
        if (front == NULL) 
            rear = NULL; 

        delete (temp); 
    } 
}; 

// Driven Program 
int main() 
{ 

    Queue q; 
    q.enQueue(10); 
    q.enQueue(20); 
    q.deQueue(); 
    q.deQueue(); 
    q.enQueue(30); 
    q.enQueue(40); 
    q.enQueue(50); 
    q.deQueue(); 
    cout << "Queue Front : " << (q.front)->data << endl; 
    cout << "Queue Rear : " << (q.rear)->data; 
} 
// This code is contributed by rathbhupendra 

```

## C

```c

// A C program to demonstrate linked list based implementation of queue 
#include <stdio.h> 
#include <stdlib.h> 

// A linked list (LL) node to store a queue entry 
struct QNode { 
    int key; 
    struct QNode* next; 
}; 

// The queue, front stores the front node of LL and rear stores the 
// last node of LL 
struct Queue { 
    struct QNode *front, *rear; 
}; 

// A utility function to create a new linked list node. 
struct QNode* newNode(int k) 
{ 
    struct QNode* temp = (struct QNode*)malloc(sizeof(struct QNode)); 
    temp->key = k; 
    temp->next = NULL; 
    return temp; 
} 

// A utility function to create an empty queue 
struct Queue* createQueue() 
{ 
    struct Queue* q = (struct Queue*)malloc(sizeof(struct Queue)); 
    q->front = q->rear = NULL; 
    return q; 
} 

// The function to add a key k to q 
void enQueue(struct Queue* q, int k) 
{ 
    // Create a new LL node 
    struct QNode* temp = newNode(k); 

    // If queue is empty, then new node is front and rear both 
    if (q->rear == NULL) { 
        q->front = q->rear = temp; 
        return; 
    } 

    // Add the new node at the end of queue and change rear 
    q->rear->next = temp; 
    q->rear = temp; 
} 

// Function to remove a key from given queue q 
void deQueue(struct Queue* q) 
{ 
    // If queue is empty, return NULL. 
    if (q->front == NULL) 
        return; 

    // Store previous front and move front one node ahead 
    struct QNode* temp = q->front; 

    q->front = q->front->next; 

    // If front becomes NULL, then change rear also as NULL 
    if (q->front == NULL) 
        q->rear = NULL; 

    free(temp); 
} 

// Driver Program to test anove functions 
int main() 
{ 
    struct Queue* q = createQueue(); 
    enQueue(q, 10); 
    enQueue(q, 20); 
    deQueue(q); 
    deQueue(q); 
    enQueue(q, 30); 
    enQueue(q, 40); 
    enQueue(q, 50); 
    deQueue(q); 
    printf("Queue Front : %d \n", q->front->key); 
    printf("Queue Rear : %d", q->rear->key); 
    return 0; 
} 

```

## Java

```java

// Java program for linked-list implementation of queue 

// A linked list (LL) node to store a queue entry 
class QNode { 
    int key; 
    QNode next; 

    // constructor to create a new linked list node 
    public QNode(int key) 
    { 
        this.key = key; 
        this.next = null; 
    } 
} 

// A class to represent a queue 
// The queue, front stores the front node of LL and rear stores the 
// last node of LL 
class Queue { 
    QNode front, rear; 

    public Queue() 
    { 
        this.front = this.rear = null; 
    } 

    // Method to add an key to the queue. 
    void enqueue(int key) 
    { 

        // Create a new LL node 
        QNode temp = new QNode(key); 

        // If queue is empty, then new node is front and rear both 
        if (this.rear == null) { 
            this.front = this.rear = temp; 
            return; 
        } 

        // Add the new node at the end of queue and change rear 
        this.rear.next = temp; 
        this.rear = temp; 
    } 

    // Method to remove an key from queue. 
    void dequeue() 
    { 
        // If queue is empty, return NULL. 
        if (this.front == null) 
            return; 

        // Store previous front and move front one node ahead 
        QNode temp = this.front; 
        this.front = this.front.next; 

        // If front becomes NULL, then change rear also as NULL 
        if (this.front == null) 
            this.rear = null; 
    } 
} 

// Driver class 
public class Test { 
    public static void main(String[] args) 
    { 
        Queue q = new Queue(); 
        q.enqueue(10); 
        q.enqueue(20); 
        q.dequeue(); 
        q.dequeue(); 
        q.enqueue(30); 
        q.enqueue(40); 
        q.enqueue(50); 
        q.dequeue(); 
        System.out.println("Queue Front : " + q.front.key); 
        System.out.println("Queue Rear : " + q.rear.key); 
    } 
} 
// This code is contributed by Gaurav Miglani 

```

## Python3

```py

# Python3 program to demonstrate linked list 
# based implementation of queue 

# A linked list (LL) node 
# to store a queue entry 
class Node: 

    def __init__(self, data): 
        self.data = data 
        self.next = None

# A class to represent a queue 

# The queue, front stores the front node 
# of LL and rear stores the last node of LL 
class Queue: 

    def __init__(self): 
        self.front = self.rear = None

    def isEmpty(self): 
        return self.front == None

    # Method to add an item to the queue 
    def EnQueue(self, item): 
        temp = Node(item) 

        if self.rear == None: 
            self.front = self.rear = temp 
            return
        self.rear.next = temp 
        self.rear = temp 

    # Method to remove an item from queue 
    def DeQueue(self): 

        if self.isEmpty(): 
            return
        temp = self.front 
        self.front = temp.next

        if(self.front == None): 
            self.rear = None

# Driver Code 
if __name__== '__main__': 
    q = Queue() 
    q.EnQueue(10) 
    q.EnQueue(20) 
    q.DeQueue() 
    q.DeQueue() 
    q.EnQueue(30) 
    q.EnQueue(40) 
    q.EnQueue(50)  
    q.DeQueue()    
    print("Queue Front " + str(q.front.data)) 
    print("Queue Rear " + str(q.rear.data)) 

```

## C#

```cs

// C# program for linked-list 
// implementation of queue 
using System; 

// A linked list (LL) node to 
// store a queue entry 
class QNode { 
    public int key; 
    public QNode next; 

    // constructor to create 
    // a new linked list node 
    public QNode(int key) 
    { 
        this.key = key; 
        this.next = null; 
    } 
} 

// A class to represent a queue The queue, 
// front stores the front node of LL and 
// rear stores the last node of LL 
class Queue { 
    QNode front, rear; 

    public Queue() 
    { 
        this.front = this.rear = null; 
    } 

    // Method to add an key to the queue. 
    public void enqueue(int key) 
    { 

        // Create a new LL node 
        QNode temp = new QNode(key); 

        // If queue is empty, then new 
        // node is front and rear both 
        if (this.rear == null) { 
            this.front = this.rear = temp; 
            return; 
        } 

        // Add the new node at the 
        // end of queue and change rear 
        this.rear.next = temp; 
        this.rear = temp; 
    } 

    // Method to remove an key from queue. 
    public void dequeue() 
    { 
        // If queue is empty, return NULL. 
        if (this.front == null) 
            return; 

        // Store previous front and 
        // move front one node ahead 
        QNode temp = this.front; 
        this.front = this.front.next; 

        // If front becomes NULL, 
        // then change rear also as NULL 
        if (this.front == null) 
            this.rear = null; 
    } 
} 

// Driver code 
public class Test { 
    public static void Main(String[] args) 
    { 
        Queue q = new Queue(); 
        q.enqueue(10); 
        q.enqueue(20); 
        q.dequeue(); 
        q.dequeue(); 
        q.enqueue(30); 
        q.enqueue(40); 
        q.enqueue(50); 
        q.dequeue(); 
        Console.WriteLine("Queue Front : " + q.front.key); 
        Console.WriteLine("Queue Rear : " + q.rear.key); 
    } 
} 

// This code has been contributed by Rajput-Ji 

```

**输出**：

```
Queue Front : 40
Queue Rear : 50

```

**时间复杂度**：两个操作 enqueue（）和 dequeue（）的时间复杂度均为`O(1)`，因为我们在两个操作中仅更改了几个指针。 任何操作都没有循环。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

