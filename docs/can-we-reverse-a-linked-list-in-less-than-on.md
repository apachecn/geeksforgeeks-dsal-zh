# 我们可以在小于`O(n)`的时间内反向链表吗？

> 原文：[https://www.geeksforgeeks.org/can-we-reverse-a-linked-list-in-less-than-on/](https://www.geeksforgeeks.org/can-we-reverse-a-linked-list-in-less-than-on/)

似乎无法逆转[简单的单链表](http://quiz.geeksforgeeks.org/linked-list-set-1-introduction/)。 [简单单链表只能使用递归和迭代方法在`O(n)`时间内反转](https://www.geeksforgeeks.org/write-a-function-to-reverse-the-nodes-of-a-linked-list/)。

具有头和尾指针的[内存高效双链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)也可以通过交换头和尾指针在`O(1)`时间内反转。

具有头和尾指针的[双链表](http://quiz.geeksforgeeks.org/doubly-linked-list/)也可以通过交换头和尾指针在`O(1)`时间内反转。 但是我们将不得不使用`prev`指针在正向遍历该列表，而使用下一个指针则在反向遍历该列表，这可能被认为无效。

本文由 **Abhishek** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

