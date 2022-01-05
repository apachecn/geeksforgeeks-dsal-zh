# 插入排序时间复杂度问题

> 原文:[https://www . geeksforgeeks . org/insertion-sort-time-complexity-question/](https://www.geeksforgeeks.org/insertion-sort-time-complexity-question/)

**问题:**需要多长时间[插入排序](https://www.geeksforgeeks.org/insertion-sort/)才能对下面表格中 n 大小的数组进行排序？

arr[] = 2，1，4，3，6，5，…。我，我-1，…..n，n-1

**回答:**乍一看，似乎插入排序需要 O(n)<sup>2</sup>时间，但实际上需要 O(n)时间

怎么做？让我们仔细看看下面的代码。

```
/* Function to sort an array using insertion sort*/
void insertionSort(int arr[], int n)
{
   for (int i = 1; i = 0 && arr[j] > key)
       {
           arr[j+1] = arr[j];
           j = j-1;
       }
       arr[j+1] = key;
   }
}

```

如果我们仔细分析输入，我们会发现每个元素离它在排序数组中的位置只有一个位置。外部 for 循环将运行到“n ”,内部 while 循环将采取 1 次交换和 2 次比较的“恒定”步骤。因为，虽然循环需要恒定的时间，并且对于“n”个元素的循环运行，所以整体复杂性是 O(n)

**备选答案:**另一种看待这个问题的方式是，[插入排序所花费的时间与数组中的反转次数](https://www.geeksforgeeks.org/time-complexity-insertion-sort-inversions/)成正比。在上面的示例类型中，反转的数量是 n/2，因此总的时间复杂度是 O(n)

本文由 **Uddalak Bhaduri** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。