# C

中 qsort()的比较器功能

> 原文:[https://www . geesforgeks . org/comparator-of-qsort-in-c/](https://www.geeksforgeeks.org/comparator-function-of-qsort-in-c/)

标准 C 库提供了 [qsort()](http://www.cplusplus.com/reference/cstdlib/qsort/) 可以用来对数组进行排序。顾名思义，该函数使用快速排序算法对给定的数组进行排序。以下是 qsort()的原型

```
void qsort (void* base, size_t num, size_t size, 
            int (*comparator)(const void*,const void*));
```

关于 qsort()的重点是比较器功能*比较器*。比较器函数接受两个参数，并包含逻辑来决定它们在排序输出中的相对顺序。其思想是提供灵活性，以便 qsort()可以用于任何类型(包括用户定义的类型)，并可以用于获得任何所需的顺序(增加、减少或任何其他)。

比较器函数采用两个指针作为参数(都是类型转换为 const void*)，并通过返回(以稳定和可传递的方式)来定义元素的顺序

```
int comparator(const void* p1, const void* p2);
Return value meaning
<0 0 the element pointed by p1 goes before p2 is equivalent to>0 The element pointed by p1 goes after the element pointed by p2

Source: http://www.cplusplus.com/reference/cstdlib/qsort/
0>
```

例如，假设有一组学生，下面是学生的类型。

```
struct Student
{
    int age, marks;
    char name[20];
};
```

假设我们需要按照分数的升序对学生进行排序。比较器功能如下所示:

```
int comparator(const void *p, const void *q) 
{
    int l = ((struct Student *)p)->marks;
    int r = ((struct Student *)q)->marks; 
    return (l - r);
}
```

有关 qsort()的更多示例用法，请参见以下帖子。
[给定一个单词序列，将所有的字谜打印在一起](https://www.geeksforgeeks.org/given-a-sequence-of-words-print-all-anagrams-together-set-2/)
[盒子堆叠问题](https://www.geeksforgeeks.org/dynamic-programming-set-21-box-stacking-problem/)
[最接近的一对点](https://www.geeksforgeeks.org/closest-pair-of-points/)

下面是一个有趣的问题，可以借助 *qsort()* 和比较器功能轻松解决。
**给定一个整数数组，按照奇数先出现，偶数后出现的方式进行排序。奇数应该按降序排列，偶数应该按升序排列。**

简单的方法是首先修改输入数组，使偶数和奇数分开，然后对两个部分(奇数和偶数)分别应用某种排序算法。

然而，有一个有趣的方法，对快速排序的比较器功能稍作修改。这个想法是写一个比较器函数，用两个地址 p 和 q 作为参数。设 l 和 r 为 p 和 q 所指向的数，函数使用以下逻辑:
1)如果(l 和 r)都是奇数，先放两者中的较大者。
2)如果(l 和 r)都是偶数，先放两者中较小的一个。
3)如果其中一个是偶数，另一个是奇数，就把奇数放在第一位。

以下是上述方法的 C 实现。

```
#include <stdio.h>
#include <stdlib.h>

// This function is used in qsort to decide the relative order
// of elements at addresses p and q.
int comparator(const void *p, const void *q)
{
    // Get the values at given addresses
    int l = *(const int *)p;
    int r = *(const int *)q;

    // both odd, put the greater of two first.
    if ((l&1) && (r&1))
        return (r-l);

    // both even, put the smaller of two first
    if ( !(l&1) && !(r&1) )
        return (l-r);

    // l is even, put r first
    if (!(l&1))
        return 1;

    // l is odd, put l first
    return -1;
}

// A utility function to print an array
void printArr(int arr[], int n)
{
    int i;
    for (i = 0; i < n; ++i)
        printf("%d ", arr[i]);
}

// Driver program to test above function
int main()
{
    int arr[] = {1, 6, 5, 2, 3, 9, 4, 7, 8};

    int size = sizeof(arr) / sizeof(arr[0]);
    qsort((void*)arr, size, sizeof(arr[0]), comparator);

    printf("Output array is\n");
    printArr(arr, size);

    return 0;
}
```

输出:

```
Output array is
9 7 5 3 1 2 4 6 8
```

**练习:**
给定一个整数数组，以交替的方式对其进行排序。交替方式意味着偶数索引处的元素被分开排序，奇数索引处的元素被分开排序。

本文由[aashis Barnwal](https://www.facebook.com/barnwal.aashish?fref=ts)编辑。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。