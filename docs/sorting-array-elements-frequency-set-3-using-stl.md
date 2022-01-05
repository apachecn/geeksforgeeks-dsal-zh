# 按频率排序数组元素|集合 3(使用 STL)

> 原文:[https://www . geesforgeks . org/sorting-array-elements-frequency-set-3-using-STL/](https://www.geeksforgeeks.org/sorting-array-elements-frequency-set-3-using-stl/)

给定一个整数数组，根据元素的频率对数组进行排序。如果两个元素的频率相同，则按递增顺序打印。

示例:

```
Input : arr[] = {2, 3, 2, 4, 5, 12, 2, 3, 3, 3, 12}
Output : 3 3 3 3 2 2 2 12 12 4 5
Explanation :
No. Freq
2  : 3
3  : 4
4  : 1
5  : 1
12 : 2

```

我们在下面的帖子中讨论了不同的方法:
[按频率排序元素|集合 1](https://www.geeksforgeeks.org/sort-elements-by-frequency/)
[按频率排序元素|集合 2](https://www.geeksforgeeks.org/sort-elements-by-frequency-set-2/)

我们可以使用[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)和[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)来解决这个问题。最初，我们创建一个映射，使得 map[element] = freq。一旦我们完成了地图的构建，我们就创建了一个配对数组。存储元素及其相应频率的一对将用于排序。我们编写了一个自定义比较函数，它首先根据 freq 比较两对，如果有，则根据值进行比较。
下面是它的 c++实现:

```
// C++ program to sort elements by frequency using
// STL
#include <bits/stdc++.h>
using namespace std;

// function to compare two pairs for inbuilt sort
bool compare(pair<int,int> &p1,
             pair<int, int> &p2)
{
    // If frequencies are same, compare
    // values
    if (p1.second == p2.second)
        return p1.first < p2.first;
    return p1.second > p2.second;
}

// function to print elements sorted by freq
void printSorted(int arr[], int n)
{
    // Store items and their frequencies
    map<int, int> m;
    for (int i = 0; i < n; i++)
        m[arr[i]]++;

    // no of distinct values in the array
    // is equal to size of map.
    int s = m.size();

    // an array of pairs
    pair<int, int> p[s];

    // Fill (val, freq) pairs in an array
    // of pairs.
    int i = 0;
    for (auto it = m.begin(); it != m.end(); ++it)
        p[i++] = make_pair(it->first, it->second);

    // sort the array of pairs using above
    // compare function.
    sort(p, p + s, compare);

    cout << "Elements sorted by frequency are: ";
    for (int i = 0; i < s; i++)
    {
        int freq = p[i].second;
        while (freq--)
            cout << p[i].first << " ";
    }
}

// driver program
int main()
{
    int arr[] = {2, 3, 2, 4, 5, 12, 2, 3,
                 3, 3, 12};
    int n = sizeof(arr)/ sizeof(arr[0]);
    printSorted(arr, n);
    return 0;
}
```

输出:

```
Elements sorted by frequency are:
 3 3 3 3 2 2 2 12 12 4 5

```

时间复杂度:0(对数 n)

本文由**阿迪提·夏尔马**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。