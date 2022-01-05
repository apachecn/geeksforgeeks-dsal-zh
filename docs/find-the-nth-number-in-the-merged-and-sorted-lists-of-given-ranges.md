# 在给定范围的合并排序列表中找到第 n 个数字

> 原文:[https://www . geeksforgeeks . org/在给定范围的合并和排序列表中查找第 n 个数字/](https://www.geeksforgeeks.org/find-the-nth-number-in-the-merged-and-sorted-lists-of-given-ranges/)

给定两个整数[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **L** 和 **R** 以及一个整数 **N** 。给定数组中的每个范围表示范围 **[L[i]，R[i]]** 中的每个数字都存在。当给定范围内的数字按其**排序的**顺序排列时，任务是计算第 N 个**(基于 0 的索引)元素。**

****示例**:**

> ****输入** : L = {1，5}，R = {3，7}，N = 4
> **输出** : 6
> **说明**:呈现的数字为{1，2，3，5， **6** ，7}。因此，第 4 个元素(0 索引)是 6。**
> 
> ****输入** : L = {1，3}，R = {4，5}，N = 3
> **输出** : 3
> **解释**:呈现的数字为{1，2，3，4，3，4，5}，它们的排序顺序为{1，2，3， **3** ，4，4，5}。因此第三个元素(0 索引)是 3。**

****接近**:通过答案上方的[二分搜索法](https://www.geeksforgeeks.org/binary-search/)可以解决任务。
按照以下步骤解决问题:**

*   **计算两个变量 **min** 和 **max** ，它们存储来自 **L** 数组的**最小**元素和来自 **R** 数组的**最大元素。****
*   **二分搜索法的范围是**【最小值，最大值】**。**
*   **对于每个 **mid = (min + max) / 2** 计算当前元素的**位置**。**
*   **要计算位置，迭代所有范围，使变量 t = 0 来存储**位置**。如果 **L【我】> =中**，检查以下两个条件

    *   如果**中间< = R[i]** ，更新 t +=中间–L[I]+1。
    *   否则 t+= R[I]–L[I]+1** 
*   **二分搜索法范围可以更新为

    *   if(t > n)max =**mid–1。**
    *   else min = **mid + 1** 。** 
*   **最终答案将存储在变量 **min** 中。**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;
int nthElement(vector<int> L, vector<int> R, int n)
{
    // Store the size of the ranges
    int K = L.size();

    // Calculate the max and min values
    long long min = 2000000000, max = -2000000000;
    for (int i = 0; i < K; i++) {
        if (L[i] < min)
            min = L[i];
        if (R[i] > max)
            max = R[i];
    }

    // Do a binary search over answer
    while (min <= max) {
        long long mid = (min + max) / 2;
        long long t = 0;

        for (int i = 0; i < K; i++) {
            if (mid >= L[i]) {
                if (mid <= R[i]) {
                    t += mid - L[i] + 1;
                }
                else {
                    t += R[i] - L[i] + 1;
                }
            }
        }

        // Update the binary Search range.
        if (t > n) {
            max = mid - 1;
        }
        else {
            min = mid + 1;
        }
    }
    return min;
}

// Driver Code
int main()
{
    vector<int> L = { 1, 5 }, R = { 3, 7 };
    int N = 4;
    cout << nthElement(L, R, N);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation for the above approach

class GFG {

    public static long nthElement(int[] L, int[] R, int n) {
        // Store the size of the ranges
        int K = L.length;

        // Calculate the max and min values
        long min = 2000000000, max = -2000000000;
        for (int i = 0; i < K; i++) {
            if (L[i] < min)
                min = L[i];
            if (R[i] > max)
                max = R[i];
        }

        // Do a binary search over answer
        while (min <= max) {
            long mid = (min + max) / 2;
            long t = 0;

            for (int i = 0; i < K; i++) {
                if (mid >= L[i]) {
                    if (mid <= R[i]) {
                        t += mid - L[i] + 1;
                    } else {
                        t += R[i] - L[i] + 1;
                    }
                }
            }

            // Update the binary Search range.
            if (t > n) {
                max = mid - 1;
            } else {
                min = mid + 1;
            }
        }
        return min;
    }

    // Driver Code
    public static void main(String args[]) {
        int[] L = { 1, 5 }, R = { 3, 7 };
        int N = 4;
        System.out.println(nthElement(L, R, N));
    }

}

// This code is contributed by gfgking
```

## **蟒蛇 3**

```
# Python implementation for the above approach

def nthElement(L, R, n):
  # Store the size of the ranges
  K = len(L)

  # Calculate the max and min values
  min = 2000000000
  max = -2000000000;
  for i in range(K):
    if (L[i] < min):
      min = L[i]
    if (R[i] > max):
      max = R[i];

  # Do a binary search over answer
  while (min <= max):
    mid = (min + max) // 2;
    t = 0;

    for i in range(K):
      if (mid >= L[i]):
        if (mid <= R[i]):
          t += mid - L[i] + 1;
        else:
          t += R[i] - L[i] + 1;

    # Update the binary Search range.
    if (t > n):
      max = mid - 1;
    else:
      min = mid + 1;

  return min;

# Driver Code

L = [1, 5]
R = [3, 7];
N = 4;
print(nthElement(L, R, N));

# This code is contributed by gfgking
```

## **C#**

```
// C# implementation for the above approach

using System;
class GFG {

    public static long nthElement(int[] L, int[] R, int n)
    {

        // Store the size of the ranges
        int K = L.Length;

        // Calculate the max and min values
        long min = 2000000000, max = -2000000000;
        for (int i = 0; i < K; i++) {
            if (L[i] < min)
                min = L[i];
            if (R[i] > max)
                max = R[i];
        }

        // Do a binary search over answer
        while (min <= max) {
            long mid = (min + max) / 2;
            long t = 0;

            for (int i = 0; i < K; i++) {
                if (mid >= L[i]) {
                    if (mid <= R[i]) {
                        t += mid - L[i] + 1;
                    } else {
                        t += R[i] - L[i] + 1;
                    }
                }
            }

            // Update the binary Search range.
            if (t > n) {
                max = mid - 1;
            } else {
                min = mid + 1;
            }
        }
        return min;
    }

    // Driver Code
    public static void Main() {
        int[] L = { 1, 5 }, R = { 3, 7 };
        int N = 4;
        Console.Write(nthElement(L, R, N));
    }

}

// This code is contributed by gfgking
```

## **java 描述语言**

```
<script>
// Javascript implementation for the above approach

function nthElement(L, R, n) {
  // Store the size of the ranges
  let K = L.length;

  // Calculate the max and min values
  let min = 2000000000, max = -2000000000;
  for (let i = 0; i < K; i++) {
    if (L[i] < min)
      min = L[i];
    if (R[i] > max)
      max = R[i];
  }

  // Do a binary search over answer
  while (min <= max) {
    let mid = Math.floor((min + max) / 2);
    let t = 0;

    for (let i = 0; i < K; i++) {
      if (mid >= L[i]) {
        if (mid <= R[i]) {
          t += mid - L[i] + 1;
        }
        else {
          t += R[i] - L[i] + 1;
        }
      }
    }

    // Update the binary Search range.
    if (t > n) {
      max = mid - 1;
    }
    else {
      min = mid + 1;
    }
  }
  return min;
}

// Driver Code

let L = [1, 5]
let R = [3, 7];
let N = 4;
document.write(nthElement(L, R, N));

// This code is contributed by gfgking

</script>
```

****Output**

```
6
```** 

*****时间复杂度***:O(N * log(max–min))
***辅助空间*** **:** O(N)**