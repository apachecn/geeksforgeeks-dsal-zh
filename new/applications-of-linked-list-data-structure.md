# 链表数据结构的应用

链表是一种线性数据结构，其中的元素未存储在连续的内存位置。 链接列表中的元素使用指针链接，如下图所示：
![](img/d97a233bf3c89e80c46e6a3193e851d6.png)
**链接列表在计算机科学中的应用** –

1.  [堆栈](https://www.geeksforgeeks.org/stack-data-structure/)和[队列](https://www.geeksforgeeks.org/queue-data-structure/)的实现
2.  图的实现：[图的相邻列表表示法](https://www.geeksforgeeks.org/graph-and-its-representations/)最流行，它使用链接列表来存储相邻的顶点。
3.  动态内存分配：我们使用空闲块的链表。
4.  维护名称目录
5.  对长整数执行算术运算
6.  通过将常数存储在链接列表的节点中来处理多项式
7.  代表稀疏矩阵

**链表在现实世界中的应用-**

1.  *图像查看器* –上一个和下一个图像已链接，因此可以通过下一个和上一个按钮进行访问。
2.  *Web浏览器中的上一页和下一页* –我们可以通过按Back和Next按钮访问在Web浏览器中搜索的上一个和下一个URL，因为它们被链接为链接列表。
3.  *音乐播放器* –音乐播放器中的歌曲链接到上一首和下一首歌曲。 您可以从列表的开头或结尾播放歌曲。

**循环链接列表的应用：**

1.  对于实现队列很有用。 与[此](http://quiz.geeksforgeeks.org/queue-set-2-linked-list-implementation/)实现不同，如果我们使用循环链表，则不需要在前后都保留两个指针。 我们可以维护一个指向最后插入的节点的指针，并且始终可以将前一个作为倒数第二个。
2.  循环列表在应用程序中反复遍历列表很有用。 例如，当一台PC上运行多个应用程序时，操作系统通常会将正在运行的应用程序放在列表中，然后在它们之间循环，给它们每个执行时间，然后让它们等待 而将CPU分配给另一个应用程序。 操作系统使用循环列表很方便，这样，当循环列表到达列表末尾时，它可以循环到列表的开头。
3.  循环双链表用于实现高级数据结构，例如[斐波那契堆](http://en.wikipedia.org/wiki/Fibonacci_heap)。

**一个示例问题：**

设计一个数据结构，以有效支持以下操作。

1.  getMin：获取最小值
2.  extractMin：去除最小值
3.  getMax：获取最大值
4.  extractMax：删除最大值
5.  insert：插入一个项目。 可以假定插入的项目始终大于到目前为止的最大值。 例如，有效的插入顺序是10、12、13、20、50。

双链表是这里最好的解决方案。 我们保持头和尾指针，因为插入的项总是最大的，所以我们在尾插入。 可以在O（1）时间内从头部或尾部删除项目。 因此，所有操作都需要O（1）时间。

**[链表](https://www.geeksforgeeks.org/category/linked-list/)** 上的最新文章



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。