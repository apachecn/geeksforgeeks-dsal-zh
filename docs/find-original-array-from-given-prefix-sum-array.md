# 从给定的前缀和数组中找到原始数组

> 原文:[https://www . geesforgeks . org/find-origin-array-from-给定前缀-sum-array/](https://www.geeksforgeeks.org/find-original-array-from-given-prefix-sum-array/)

给定 [**前缀和数组**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) **推定[]** 的一个数组。任务是找到前缀和为**的原始数组。**

**示例:**

> **输入:**假定[] = {5，7，10，11，18}
> **输出:**【5，2，3，1，7】
> **解释:**原数组{5，2，3，1，7}
> 前缀和数组= {5，5+2，5+2+3+1，5+2+3+1+7} = {5，7，10，11，18 }
> 
> **输入:**假定[] = {45，57，63，78，89，97}
> **输出:**【45，12，6，15，11，8】

**进场:**这个问题可以根据下面的观察来解决。

> 给定前缀和数组**假定[]** ，假设原始数组为 **arr[]** ，大小为 **N** 。
> **假定[]** 数组计算如下:
> 
> *   S7-1200 可编程控制器
> *   假设[i] = arr[0] + arr[1] +。。。范围内所有**I****【1，N-1】**的+arr【I】
> 
> 所以，**假定[i]** = **arr[0] + arr[i] +。。。+ arr[i-1] + arr[i]**
> = **假定[i-1] + arr[i]**
> 因此， **arr[i] =假定[I]–假定[i-1]。**对于范围**【1，N-1】**和
> **中的所有**I**=假定【0】**

按照下面提到的步骤解决问题:

1.  从数组的开头开始遍历**假定[]** 数组。
2.  如果索引 **(i) = 0** ，那么**arr【I】=假定【I】**。
3.  Else， **arr[i] = presum[i] – presume[i-1]** 。

下面是上述实现的代码:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Finds and prints the elements of
// the original array
void DecodeOriginalArray(int presum[], int N)
{
    // Calculating elements of original array
    for (int i = N - 1; i > 0; i--)
        presum[i] = presum[i] - presum[i - 1];

    // Displaying elements of original array
    for (int i = 0; i < N; i++)
        cout << presum[i] << " ";
}

// Driver program to test above
int main()
{
    int presum[] = { 45, 57, 63, 78, 89, 97 };
    int N = sizeof(presum) / sizeof(presum[0]);

    // Function Call
    DecodeOriginalArray(presum, N);
    return 0;
}
```

**Output**

```
45 12 6 15 11 8 
```

***时间复杂度:*** O(N)
***辅助空间:*** O(1)