# 我们可以在小于O（n）的时间内反向链接列表吗？

似乎无法逆转[简单的单链接列表](http://quiz.geeksforgeeks.org/linked-list-set-1-introduction/)。 [简单单链表只能使用递归和迭代方法](https://www.geeksforgeeks.org/write-a-function-to-reverse-the-nodes-of-a-linked-list/) s在O（n）时间内反转。

具有头和尾指针的[内存高效双链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)也可以通过交换头和尾指针在O（1）时间内反转。

具有头和尾指针的[双链表](http://quiz.geeksforgeeks.org/doubly-linked-list/)也可以通过交换头和尾指针在O（1）时间内反转。 但是我们将不得不使用prev指针在正向遍历该列表，而使用下一个指针则在反向遍历该列表，这可能被认为无效。

本文由 **Abhishek** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。