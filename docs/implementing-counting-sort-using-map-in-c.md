# 在 C++中使用映射实现计数排序

> 原文:[https://www . geesforgeks . org/implementing-counting-sort-using-map-in-c/](https://www.geeksforgeeks.org/implementing-counting-sort-using-map-in-c/)

[计数排序](https://www.geeksforgeeks.org/counting-sort/)是可以在 O(n)时间复杂度下排序的最佳排序算法之一，但是计数排序的缺点是空间复杂度，对于一个很小的值集合，也需要大量的未使用空间。

因此，我们需要两件事来克服这一点:

1.  一种数据结构，只占用输入元素的空间，不占用除输入以外的所有元素的空间。
2.  存储的元素必须按顺序排序，因为如果没有排序，那么存储它们就没有用了。

所以 C++中的[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)同时满足这两个条件。因此，我们可以通过地图来实现这一点。

**示例:**

> **输入:** arr[] = {1，4，3，5，1}
> **输出:** 1 1 3 4 5
> 
> **输入:** arr[] = {1，-1，-3，8，-3}
> 输出: -3 -3 -1 1 8

下面是 C++中使用映射进行计数排序的实现:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to sort the array using counting sort
void countingSort(vector<int> arr, int n)
{

    // Map to store the frequency
    // of the array elements
    map<int, int> freqMap;
    for (auto i = arr.begin(); i != arr.end(); i++) {
        freqMap[*i]++;
    }

    int i = 0;

    // For every element of the map
    for (auto it : freqMap) {

        // Value of the element
        int val = it.first;

        // Its frequency
        int freq = it.second;
        for (int j = 0; j < freq; j++)
            arr[i++] = val;
    }

    // Print the sorted array
    for (auto i = arr.begin(); i != arr.end(); i++) {
        cout << *i << " ";
    }
}

// Driver code
int main()
{
    vector<int> arr = { 1, 4, 3, 5, 1 };
    int n = arr.size();

    countingSort(arr, n);

    return 0;
}
```

**Output:**

```
1 1 3 4 5

```