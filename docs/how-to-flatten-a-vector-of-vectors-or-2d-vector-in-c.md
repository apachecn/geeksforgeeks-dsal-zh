# 如何在 C++中展平矢量或 2D 矢量

> 原文:[https://www . geeksforgeeks . org/如何展平矢量中的矢量或矢量中的二维矢量/](https://www.geeksforgeeks.org/how-to-flatten-a-vector-of-vectors-or-2d-vector-in-c/)

给定向量的[向量(2D 向量)](https://www.geeksforgeeks.org/vector-of-vectors-in-c-stl-with-examples/)，任务是展平这个二维向量。

**示例:**

> **输入:**向量= [[1，2，3，4]，[5，6]，[7，8]]
> **输出:** 1 2 3 4 5 6 7 8
> 
> **输入:**向量= [[1，2]，[3]，[4，5，6，8]]
> **输出:** 1 2 3 4 5 6 8

**算法:**

1.  [2D 向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/)可以使用[迭代器](https://www.geeksforgeeks.org/iterators-c-stl/)进行展平。
2.  在两个数组中分别存储每个向量的开始和结束迭代器。
3.  创建一个 **hasNext()方法**来检查它是否有向量有下一个元素。
4.  如果 hasNext()得出 true，则打印当前元素

下面是上述方法的实现:

```
// C++ program to flatten a
// Vector of Vectors or 2D Vector

#include <bits/stdc++.h>
using namespace std;

// Class to flatten the 2d vector
class FlattenVector {

public:
    int n;

    vector<vector<int>::iterator> iStart;
    vector<vector<int>::iterator> iEnd;
    int currIndex;

    // Store ending and starting iterators.
    FlattenVector(vector<vector<int> >& v)
    {

        // Get the number
        // of rows in 2d vector
        n = v.size();
        currIndex = 0;
        iStart.resize(n);
        iEnd.resize(n);

        for (int i = 0; i < n; i++) {
            iStart[i] = v[i].begin();
            iEnd[i] = v[i].end();
        }
    }

    // Returns true if any element is left.
    bool hasNext()
    {
        for (int i = 0; i < n; i++) {
            if (iStart[i] != iEnd[i])
                return true;
        }
        return false;
    }

    int next()
    {
        // Vector at currIndex is printed,
        // increment currIndex.
        if (iStart[currIndex]
            == iEnd[currIndex]) {
            currIndex++;
            return next();
        }

        // Increment iterator
        // and return the value.
        else
            return *iStart[currIndex]++;
    }
};

// Driver code
int main()
{
    vector<vector<int> >
        v{ { 1, 2 },
           { 3 },
           { 4, 5, 6 },
           { 7, 8, 9, 10 } };
    FlattenVector iter(v);

    while (iter.hasNext())
        cout << iter.next() << " ";

    return 0;
}
```

**Output:**

```
1 2 3 4 5 6 7 8 9 10

```