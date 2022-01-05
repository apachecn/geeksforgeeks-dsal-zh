# 在 STL

中使用对根据另一个数组对一个数组进行排序

> 原文:[https://www . geesforgeks . org/sorting-array-根据另一个-array-使用-pair-stl/](https://www.geeksforgeeks.org/sorting-array-according-another-array-using-pair-stl/)

给我们两个数组。我们需要根据一个数组对另一个数组进行排序。

示例:

```
Input : 2 1 5 4 9 3 6 7 10 8
        A B C D E F G H I J

Output : 1 2 3 4 5 6 7 8 9 10 
         B A F D C G H J E I 
Here we are sorting second array
(a character array) according to 
the first array (an integer array).

```

我们在下面的帖子中讨论了不同的方法。
[根据另一个数组定义的顺序对一个数组进行排序](https://www.geeksforgeeks.org/sort-array-according-order-defined-another-array/)

在这篇文章中，我们将重点放在使用 C++的 STL 中的[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)容器上。

为了完成我们的任务，我们将从这两个数组中分别创建元素对。然后简单地使用排序函数。需要注意的重要一点是，对中的第一个元素应该来自要执行排序的数组。

```
// Sort an array according to 
// other using pair in STL.
#include <bits/stdc++.h>
using namespace std;

// Function to sort character array b[]
// according to the order defined by a[]
void pairsort(int a[], char b[], int n)
{
    pair<int, char> pairt[n];

    // Storing the respective array
    // elements in pairs.
    for (int i = 0; i < n; i++) 
    {
        pairt[i].first = a[i];
        pairt[i].second = b[i];
    }

    // Sorting the pair array.
    sort(pairt, pairt + n);

    // Modifying original arrays
    for (int i = 0; i < n; i++) 
    {
        a[i] = pairt[i].first;
        b[i] = pairt[i].second;
    }
}

// Driver function
int main()
{
    int a[] = {2, 1, 5, 4, 9, 3, 6, 7, 10, 8};
    char b[] = {'A', 'B', 'C', 'D', 'E', 'F', 
                         'G', 'H', 'I', 'J'};

    int n = sizeof(a) / sizeof(a[0]);

    // Function calling
    pairsort(a, b, n);

    for (int i = 0; i < n; i++)
        cout << a[i] << " ";
    cout << endl;

    for (int i = 0; i < n; i++)
        cout << b[i] << " ";

    return 0;
}
```

输出:

```
1 2 3 4 5 6 7 8 9 10 
B A F D C G H J E I 

```

本文由 [**维奈乔希**](https://auth.geeksforgeeks.org/profile.php?user=Vineet Joshi) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。