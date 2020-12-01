# 链表的所有子集的总和

> 原文：[https://www.geeksforgeeks.org/sum-of-all-subset-sums-of-a-linked-list/](https://www.geeksforgeeks.org/sum-of-all-subset-sums-of-a-linked-list/)

给定一个链表，任务是找到链表所有子集的总和。

**示例**：

> **输入**：`2 -> 3 -> NULL`
>
> **输出**：10
>
> **说明**：
>
> 所有非空子集是`{2}, {3}`和`{2, 3}`
>
> 总和为`2 + 3 + (2 + 3) = 10`
> 
> **输入**：`2-> 1 -> 5-> 6-> NULL`
>
> **输出**：112

**方法**：考虑所有可能的子集，我们可以观察到每个节点出现`2 ^ (N - 1)`次。 因此，所有节点与`2 ^ (N - 1)`之和的乘积给出了最终答案。

下面是上述方法的实现：

**输出**：

```
112

```

**时间复杂度**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。