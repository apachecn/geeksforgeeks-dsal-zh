# 二进制堆的数组表示

> 原文:[https://www . geeksforgeeks . org/array-表示二进制堆/](https://www.geeksforgeeks.org/array-representation-of-binary-heap/)

二进制堆是一个完整的二叉树。二进制堆通常表示为数组。表示如下:

*   根元素将位于 Arr[0]。
*   Below table shows indexes of other nodes for the i<sup>th</sup> node, i.e., Arr[i]:

    | Arr[(i-1)/2] | 返回父节点 |
    | Arr[(2*i)+1] | 返回左边的子节点 |
    | Arr[(2*i)+2] | 返回右边的子节点 |

    用于实现数组表示遍历方法是**级排序**
    ![binary-heap-array-mapping](img/b491df56cefa7c6ca90d2dd480b11c8e.png)
    二进制堆满足**排序属性**。
    排序可以有两种类型:
    **1。最小堆属性:**每个节点的值大于或等于其父节点的值，最小值在根节点。

    示例:
    ![min-heap](img/3fe68e1f4fb92b42bda15ee46d1b9ba1.png)

    **2。最大堆属性:**每个节点的值小于或
    等于其父节点的值，最大值在根节点。

    示例:
    ![max-heap](img/3a68c0b7e894e84fb6348ab61291f532.png)

    要实现基本的堆操作，请遵循以下链接:[https://www.geeksforgeeks.org/binary-heap/](https://www.geeksforgeeks.org/binary-heap/)

    本文由 **Saksham Raj Seth** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

    如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。