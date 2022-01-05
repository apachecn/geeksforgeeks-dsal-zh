# 用前 K 个和后 K 个元素的平均值替换给定数组的所有元素

> 原文:[https://www . geeksforgeeks . org/将给定数组的所有元素替换为前 k 个和后 k 个元素的平均值/](https://www.geeksforgeeks.org/replace-all-elements-of-given-array-with-average-of-previous-k-and-next-k-elements/)

给定一个包含 **N** 正整数和一个整数**K**的数组 **arr[]** ，任务是用前一个 **K** 和后一个 **K** 元素的平均值替换每个数组元素。此外，如果 **K** 元素不存在，则调整使用前后可用元素的最大数量。

**示例:**

> **输入:** arr[] = {9，7，3，9，1，8，11}，K=2
> **输出:**5 7 6 4 7 7 4
> T6】解释:对于 i = 0，平均值= (7 + 3)/2 = 5
> 对于 i = 1，平均值= (9 + 3 + 9)/3 = 7
> 对于 i = 2，平均值= (9 + 7 + 9 + 1)/4 = 6
> 对于 i = 3， 平均值= (7 + 3 + 1 + 8)/4 = 4
> 对于 i = 4，平均值= (3 + 9 + 8 + 11)/4 = 7
> 对于 i = 5，平均值= (9 + 1 + 11)/3 = 7
> 对于 i = 6，平均值= (1 + 8)/2 = 4
> 
> **输入:** arr[] = {13，26，35，41，23，18，38}，K=3
> **输出:** 34 28 24 25 31 34 27

**天真方法:**最简单的方法是使用嵌套循环。外环将从左到右遍历数组，即从 **i = 0** 到 **i < N** ，内环将从索引**I–K**到索引 **i + K** 除了 **i** 之外的所有子数组，并计算它们的平均值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to replace all array elements
// with the average of previous and 
// next K elements
void findAverage(int arr[], int N, int K)
{
    int start, end;
    for (int i = 0; i < N; i++) {
        int sum = 0;

        // Start limit is max(i-K, 0)
        start = max(i - K, 0);

        // End limit in min(i+K, N-1)
        end = min(i + K, N - 1);
        int cnt = end - start;
        for (int j = start; j <= end; j++) {

            // Skipping the current element
            if (j == i) {
                continue;
            }
            sum += arr[j];
        }
        cout << sum / cnt << ' ';
    }
}

// Driver Code
int main()
{
    int arr[] = { 9, 7, 3, 9, 1, 8, 11 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 2;
    findAverage(arr, N, K);
    return 0;
}
```

**Output**

```
5 7 6 4 7 7 4 
```

***时间复杂度:***O(N<sup>2</sup>)
***辅助空间:*** O(1)

**高效方法:**该方法采用 [**滑动窗口**](https://www.geeksforgeeks.org/window-sliding-technique/) 的方法。遵循下面提到的步骤来实现这个概念:

*   考虑每个元素都有 **K** 个下一个和上一个元素，取一个大小为 2*K + 1 的窗口来覆盖整个范围。
*   现在初步求第一(K+1)个元素的和。
*   t 遍历数组时:
    *   通过将总和除以(窗口大小-1)来计算平均值。
    *   在当前窗口最右端后添加下一个元素。
    *   移除当前窗口最左边的元素。这会将窗口向右移动一个位置
*   打印结果数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to replace all array elements
// with the average of previous and 
// next K elements
void findAverage(int arr[], int N, int K)
{
    int i, sum = 0, next, prev, update;
    int cnt = 0;

    // Calculate initial sum of K+1 elements
    for (i = 0; i <= K and i < N; i++) {
        sum += arr[i];
        cnt += 1;
    }

    // Using the sliding window technique
    for (i = 0; i < N; i++) {
        update = sum - arr[i];
        cout << update / (cnt - 1) << " ";
        next = i + K + 1;
        prev = i - K;
        if (next < N) {
            sum += arr[next];
            cnt += 1;
        }
        if (prev >= 0) {
            sum -= arr[prev];
          cnt-=1;
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 9, 7, 3, 9, 1, 8, 11 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 2;
    findAverage(arr, N, K);
    return 0;
}
```

**Output**

```
5 7 6 4 7 7 4 
```

***时间复杂度:*** O(N)
***辅助空间:*** O(1)