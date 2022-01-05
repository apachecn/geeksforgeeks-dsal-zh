# 用 C++中的 map 计算向量中每个元素的频率的程序

> 原文:[https://www . geesforgeks . org/program-to-find-frequency-in-a-vector-use-map-in-c/](https://www.geeksforgeeks.org/program-to-find-frequency-of-each-element-in-a-vector-using-map-in-c/)

给定一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **向量**，任务是使用[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)找到**向量**的每个元素的频率。
**举例:**

> 输入:vec = {1，2，2，3，1，4，4，5}
> 输出:
> 1 2
> 2 2
> 3 1
> 4 2
> 5 1
> T7】说明:T9】1 已发生 2 次
> 2 已发生 2 次
> 3 已发生 1 次
> 4 已发生 2 次
> 5 已发生 1 次
> 输入:v1 = {6，7，8，6，4， 1}
> 输出:
> 1 1
> 4 1
> 6 2
> 7 1
> 8 1
> **说明:**
> 1 已发生 1 次
> 4 已发生 1 次
> 6 已发生 2 次
> 7 已发生 1 次
> 8 已发生 1 次

**方法:**
我们可以使用给定的四个步骤高效地找到向量中元素的频率:

1.  遍历给定向量**向量**的元素。
2.  检查当前元素是否存在于地图中。
3.  如果存在，则更新当前元素的频率，否则插入频率为 1 的元素，如下所示:
4.  遍历地图并打印作为映射值存储的每个元素的频率。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
#include <bits/stdc++.h>
using namespace std;

void printFrequency(vector<int> vec)
{
    // Define an map
    map<int, int> M;

    // Traverse vector vec check if
    // current element is present
    // or not
    for (int i = 0; vec[i]; i++) {

        // If the current element
        // is not found then insert
        // current element with
        // frequency 1
        if (M.find(vec[i]) == M.end()) {
            M[vec[i]] = 1;
        }

        // Else update the frequency
        else {
            M[vec[i]]++;
        }
    }

    // Traverse the map to print the
    // frequency
    for (auto& it : M) {
        cout << it.first << ' '
             << it.second << '\n';
    }
}

// Driver Code
int main()
{
    vector<int> vec = { 1, 2, 2, 3, 1, 4, 4, 5 };

    // Function call
    printFrequency(vec);
    return 0;
}
```

**Output:** 

```
1 2
2 2
3 1
4 2
5 1
```

**复杂度分析:**
**时间复杂度:** O(n log n)
对于给定的大小为 n 的向量，我们迭代一次，在地图中搜索元素的时间复杂度为 O(log n)。所以时间复杂度是 O(n log n)
**空间复杂度:** O(n)
对于给定的大小为 n 的向量，我们使用的是一个额外的映射，它最多可以有 n 个键值，所以空间复杂度是 O(n)