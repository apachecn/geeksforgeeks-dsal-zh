# 将数组转换为简化形式|集合 2(使用向量对)

> 原文:[https://www . geesforgeks . org/convert-array-reduced-form-set-2-use-vector-pairs/](https://www.geeksforgeeks.org/convert-array-reduced-form-set-2-using-vector-pairs/)

给定一个有 n 个不同元素的数组，将给定的数组转换成所有元素都在 0 到 n-1 范围内的形式。元素的顺序相同，即 0 代表最小的元素，1 代表第二小的元素，……n-1 代表最大的元素。

```
Input:  arr[] = {10, 40, 20}
Output: arr[] = {0, 2, 1}

Input:  arr[] = {5, 10, 40, 30, 20}
Output: arr[] = {0, 1, 4, 3, 2}

```

我们已经讨论了简单的和基于散列的解决方案。

在这篇文章中，讨论了一个新的解决方案。这个想法是创建一个向量对。每对元素都包含元素和索引。我们按数组值对向量进行排序。排序后，我们将索引复制到原始数组。

```
// C++ program to convert an array in reduced
// form
#include <bits/stdc++.h>
using namespace std;

// Converts arr[0..n-1] to reduced form.
void convert(int arr[], int n)
{
    // A vector of pairs. Every element of
    // pair contains array element and its
    // index
    vector <pair<int, int> > v;

    // Put all elements and their index in
    // the vector
    for (int i = 0; i < n; i++)
        v.push_back(make_pair(arr[i], i));

    // Sort the vector by array values
    sort(v.begin(), v.end());

    // Put indexes of modified vector in arr[]
    for (int i=0; i<n; i++)
        arr[v[i].second] = i;
}

// Utility function to print an array.
void printArr(int arr[], int n)
{
    for (int i=0; i<n; i++)
        cout << arr[i] << " ";
}

// Driver program to test above method
int main()
{
    int arr[] = {10, 20, 15, 12, 11, 50};
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << "Given Array is \n";
    printArr(arr, n);

    convert(arr , n);

    cout << "\n\nConverted Array is \n";
    printArr(arr, n);

    return 0;
}
```

输出:

```
Given Array is 
10 20 15 12 11 50 

Converted Array is 
0 4 3 2 1 5 

```

时间复杂度:O(n Log n)
辅助空间:O(n)

本文由**阿比特古普塔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论