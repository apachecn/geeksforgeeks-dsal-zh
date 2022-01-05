# 在 C++中使用 deque 对数组进行循环旋转

> 原文:[https://www . geeksforgeeks . org/循环旋转阵列-使用-deque-in-c/](https://www.geeksforgeeks.org/circular-rotation-of-an-array-using-deque-in-c/)

给定一个整数数组 **arr[]** 和另一个整数 **D** ，任务是在数组上执行 **D** 圆周旋转并打印修改后的数组。

**示例:**

> **输入:** Arr[] = {1，2，3，4，5，6}，D = 2
> T3】输出: 5 6 1 2 3 4
> 
> **输入:** Arr[] = {1，2，3}，D = 2
> T3】输出: 2 3 1

**方法:**
使用 C++中的 [deque](https://www.geeksforgeeks.org/deque-set-1-introduction-applications) ，可以执行旋转，从 Deque 中删除最后一个元素，并将其插入到同一个 Deque 的开头。

同样，可以执行所有需要的旋转，然后打印修改后的 deque 的内容，以获得所需的旋转数组。

如果旋转的次数超过了德格的大小，那么就用 **N** 取 mod，这样， **D = D%N** 。
其中 **D** 为转数，N 为德格大小。

下面是上述方法的实现:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to circular rotate
// the array by d elements
void rotate(deque<int> deq,
            int d, int n)
{
    // Push first d elements
    // from last to the beginning
    for (int i = 0; i < d; i++) {
        int val = deq.back();
        deq.pop_back();
        deq.push_front(val);
    }

    // Print the rotated array
    for (int i = 0; i < n; i++) {
        cout << deq[i] << " ";
    }
    cout << endl;
}

// Driver code
int main()
{
    deque<int> v = { 1, 2, 3, 4, 5, 6, 7 };
    int n = v.size();
    int d = 5;

    rotate(v, d % n, n);
}
```

**Output:**

```
3 4 5 6 7 1 2

```