# 循环链接列表| 第 1 组（简介和应用）

我们在以下帖子中讨论了单链和双链列表。

[链表简介](http://quiz.geeksforgeeks.org/linked-list-set-1-introduction/) & [插入](http://quiz.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)
*[双链表简介和插入](http://quiz.geeksforgeeks.org/doubly-linked-list/ "Permanent link to Doubly Linked List  | Set 1 (Introduction and Insertion)")*

 ****圆形链表**是链表，其中所有节点都连接在一起形成一个圆。 最后没有 NULL。 循环链表可以是单循环链表或双循环链表。*

![](img/ff7f30aebf5dc865587c7829dcf4233c.png "cll")

**循环链表的优点：**
**1）**任何节点都可以作为起点。 我们可以从任何点开始遍历整个列表。 当第一个访问的节点再次被访问时，我们只需要停止即可。

**2）**对执行队列有用。 与[此](http://quiz.geeksforgeeks.org/queue-set-2-linked-list-implementation/)实现不同，如果我们使用循环链表，则不需要在前后都保留两个指针。 我们可以维护一个指向最后插入的节点的指针，并且始终可以将前一个作为倒数第二个。

**3）**循环列表在应用程序中反复遍历列表很有用。 例如，当一台 PC 上运行多个应用程序时，操作系统通常会将正在运行的应用程序放在列表中，然后在它们之间循环，给它们每个执行时间，然后让它们等待 而将 CPU 分配给另一个应用程序。 操作系统使用循环列表很方便，这样，当循环列表到达列表末尾时，它可以循环到列表的开头。

**4）**循环双链表用于实现高级数据结构，例如[斐波那契堆](http://en.wikipedia.org/wiki/Fibonacci_heap)。

**下一篇文章：**
**[通报链表| 第 2 组（遍历）](https://www.geeksforgeeks.org/circular-linked-list-set-2-traversal/)**
**[循环单链接列表| 插入](https://www.geeksforgeeks.org/circular-singly-linked-list-insertion/)**

如果您发现上述代码/算法中的任何错误，或找到其他解决相同问题的方法，请发表评论

