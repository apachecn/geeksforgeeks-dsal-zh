# 使用双链表

实现双端队列

[双端队列或双端队列](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)是[队列数据结构](https://www.geeksforgeeks.org/queue-set-1introduction-and-array-implementation/)的通用版本，允许在两端插入和删除。 在[的先前文章](https://www.geeksforgeeks.org/implementation-deque-using-circular-array/)中，已经讨论了使用圆形数组实现Deque的方法。 现在，在这篇文章中，我们将了解如何使用[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)实现Deque。

#### 计票操作；

主要对队列执行以下四个基本操作：

```
insertFront() : Adds an item at the front of Deque.
insertRear()  : Adds an item at the rear of Deque.
deleteFront() : Deletes an item from front of Deque.
deleteRear()  : Deletes an item from rear of Deque.
```

除上述操作外，还支持以下操作：

```
getFront() : Gets the front item from queue.
getRear()  : Gets the last item from queue.
isEmpty()  : Checks whether Deque is empty or not.
size()     : Gets number of elements in Deque.
erase()    : Deletes all the elements from Deque.
```

![](img/4210693cb20e75e33f593bcd98f67900.png)

**双端队列的双联列表表示形式：**
为了实现双端队列，我们​​需要跟踪两个指针，即**前**和**后置**。 我们将**从队列的后端或前端放入（推送）**，将**从后端和前端从队列中弹出（弹出）**。

**工作：**
声明类型为**节点**的两个指针**前**和**后**，其中**节点**代表结构 双链表的节点的名称。 用值NULL初始化它们两个。

**插入前端：**

```
1\. Allocate space for a newNode of doubly linked list.
2\. IF newNode == NULL, then
3\.     print "Overflow"
4\. ELSE
5\.     IF front == NULL, then
6\.         rear = front = newNode
7\.     ELSE
8\.         newNode->next = front
9\.       front->prev = newNode
10\.        front = newNode 

```

**插入后端：**

```
1\. Allocate space for a newNode of doubly linked list.
2\. IF newNode == NULL, then
3\.     print "Overflow"
4\. ELSE
5\.     IF rear == NULL, then
6\.         front = rear = newNode
7\.     ELSE
8\.         newNode->prev = rear
9\.       rear->next = newNode
10\.        rear = newNode 

```

**从前端删除：**

```
1\. IF front == NULL
2\.     print "Underflow"
3\. ELSE
4\.     Initialize temp = front
5\.     front = front->next
6\.     IF front == NULL
7\.         rear = NULL
8\.     ELSE
9\.         front->prev = NULL
10     Deallocate space for temp

```

**从后端删除：**

```
1\. IF front == NULL
2\.     print "Underflow"
3\. ELSE
4\.     Initialize temp = rear
5\.     rear = rear->prev
6\.     IF rear == NULL
7\.         front = NULL
8\.     ELSE
9\.         rear->next = NULL
10     Deallocate space for temp

```

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of Deque using``// doubly linked list``#include <bits/stdc++.h>``using` `namespace` `std;``// Node of a doubly linked list``struct` `Node ``{``int` `data;``Node *prev, *next;``// Function to get a new node``static` `Node* getnode(``int` `data)``{``Node* newNode = (Node*)``malloc``(``sizeof``(Node));``newNode->data = data;``newNode->prev = newNode->next = NULL;``return` `newNode;``}``};``// A structure to represent a deque``class` `Deque ``{``Node* front;``Node* rear;``int` `Size;``public``:``Deque()``{``front = rear = NULL;``Size = 0;``}``// Operations on Deque``void` `insertFront(``int` `data);``void` `insertRear(``int` `data);``void` `deleteFront();``void` `deleteRear();``int` `getFront();``int` `getRear();``int` `size();``bool` `isEmpty();``void` `erase();``};``// Function to check whether deque``// is empty or not``bool` `Deque::isEmpty()``{``return` `(front == NULL);``}``// Function to return the number of``// elements in the deque``int` `Deque::size()``{``return` `Size;``}``// Function to insert an element``// at the front end``void` `Deque::insertFront(``int` `data)``{``Node* newNode = Node::getnode(data);``// If true then new element cannot be added``// and it is an 'Overflow' condition``if` `(newNode == NULL)``cout <<` `"OverFlow\n"``;``else` `{``// If deque is empty``if` `(front == NULL)``rear = front = newNode;``// Inserts node at the front end``else` `{``newNode->next = front;``front->prev = newNode;``front = newNode;``}``// Increments count of elements by 1``Size++;``}``}``// Function to insert an element``// at the rear end``void` `Deque::insertRear(``int` `data)``{``Node* newNode = Node::getnode(data);``// If true then new element cannot be added``// and it is an 'Overflow' condition``if` `(newNode == NULL)``cout <<` `"OverFlow\n"``;``else` `{``// If deque is empty``if` `(rear == NULL)``front = rear = newNode;``// Inserts node at the rear end``else` `{``newNode->prev = rear;``rear->next = newNode;``rear = newNode;``}``Size++;``}``}``// Function to delete the element``// from the front end``void` `Deque::deleteFront()``{``// If deque is empty then``// 'Underflow' condition``if` `(isEmpty())``cout <<` `"UnderFlow\n"``;``// Deletes the node from the front end and makes``// the adjustment in the links``else` `{``Node* temp = front;``front = front->next;``// If only one element was present``if` `(front == NULL)``rear = NULL;``else``front->prev = NULL;``free``(temp);``// Decrements count of elements by 1``Size--;``}``}``// Function to delete the element``// from the rear end``void` `Deque::deleteRear()``{``// If deque is empty then``// 'Underflow' condition``if` `(isEmpty())``cout <<` `"UnderFlow\n"``;``// Deletes the node from the rear end and makes``// the adjustment in the links``else` `{``Node* temp = rear;``rear = rear->prev;``// If only one element was present``if` `(rear == NULL)``front = NULL;``else``rear->next = NULL;``free``(temp);``// Decrements count of elements by 1``Size--;``}``}``// Function to return the element``// at the front end``int` `Deque::getFront()``{``// If deque is empty, then returns``// garbage value``if` `(isEmpty())``return` `-1;``return` `front->data;``}``// Function to return the element``// at the rear end``int` `Deque::getRear()``{``// If deque is empty, then returns``// garbage value``if` `(isEmpty())``return` `-1;``return` `rear->data;``}``// Function to delete all the elements``// from Deque``void` `Deque::erase()``{``rear = NULL;``while` `(front != NULL) ``{``Node* temp = front;``front = front->next;``free``(temp);``}``Size = 0;``}``// Driver program to test above``int` `main()``{``Deque dq;``cout <<` `"Insert element '5' at rear end\n"``;``dq.insertRear(5);``cout <<` `"Insert element '10' at rear end\n"``;``dq.insertRear(10);``cout <<` `"Rear end element: "``<< dq.getRear() << endl;``dq.deleteRear();``cout <<` `"After deleting rear element new rear"``<<` `" is: "` `<< dq.getRear() << endl;``cout <<` `"Inserting element '15' at front end \n"``;``dq.insertFront(15);``cout <<` `"Front end element: "``<< dq.getFront() << endl;``cout <<` `"Number of elements in Deque: "``<< dq.size() << endl;``dq.deleteFront();``cout <<` `"After deleting front element new "``<<` `"front is: "` `<< dq.getFront() << endl;``return` `0;``}` |

*chevron_right**filter_none*

输出：

```
Insert element '5' at rear end
Insert element '10' at rear end
Rear end element: 10
After deleting rear element new rear is: 5
Inserting element '15' at front end
Front end element: 15
Number of elements in Deque: 2
After deleting front element new front is: 5

```

时间复杂度：诸如insertFront（），insertRear（），deleteFront（），deleteRear（）之类的操作的时间复杂度为O（1）。 Ease（）的时间复杂度为O（n）。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。