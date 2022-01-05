# 在 C++ STL 中对一个向量进行排序后，跟踪之前的索引

> 原文:[https://www . geesforgeks . org/keep-track-of-previous-indexes-after-sorting-a-vector-in-c-STL/](https://www.geeksforgeeks.org/keep-track-of-previous-indexes-after-sorting-a-vector-in-c-stl/)

**先决条件:** [向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)[向量对排序](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second)

给定一个向量，跟踪对应于每个元素的当前索引，并在使用其先前的相应索引对打印元素进行排序之后。

**示例:**

> **输入:** Arr[] = {2，5，3，7，1}
> **输出:** {1，4} {2，0} {3，2} {5，1} {7，3}
> **说明:**
> 排序前【索引(元素)】:【0(2)，1(5)，2(3)，3(7)，4(1)】
> 排序后【previous_index(元素)】:[4(1)，0(2)，2(3)，1(1)
> 
> **输入:** Arr[] = {4，5，10，8，3，11}
> **输出:** {3，4} {4，0} {5，1} {8，3} {10，2} {11，5}

**方法:**思想是将每个元素及其当前索引存储在一个向量对中，然后对向量的所有元素进行排序，最后打印与其索引相关联的元素。

下面是上述方法的实现:

```
// C++ implementation to keep track
// of previous indexes
// after sorting a vector

#include <bits/stdc++.h>
using namespace std;

void sortArr(int arr[], int n)
{

    // Vector to store element
    // with respective present index
    vector<pair<int, int> > vp;

    // Inserting element in pair vector
    // to keep track of previous indexes
    for (int i = 0; i < n; ++i) {
        vp.push_back(make_pair(arr[i], i));
    }

    // Sorting pair vector
    sort(vp.begin(), vp.end());

    // Displaying sorted element
    // with previous indexes
    // corresponding to each element
    cout << "Element\t"
         << "index" << endl;
    for (int i = 0; i < vp.size(); i++) {
        cout << vp[i].first << "\t"
             << vp[i].second << endl;
    }
}

// Driver code
int main()
{
    int arr[] = { 2, 5, 3, 7, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    sortArr(arr, n);

    return 0;
}
```

**Output:**

```
Element    index
1    4
2    0
3    2
5    1
7    3

```