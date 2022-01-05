# 求每个数组元素每侧 K 个相邻元素的平均值

> 原文:[https://www . geesforgeks . org/find-mean-of-k-相邻元素-在每侧-对于每个数组元素/](https://www.geeksforgeeks.org/find-mean-of-k-adjacent-elements-on-each-sides-for-each-array-element/)

给定一个由 **N** 个数字组成的[圆形数组](https://www.geeksforgeeks.org/circular-array/?ref=gcse) **arr[]** ，以及一个整数 **K** 。任务是打印每个元素的 **2K+1** 数字的平均值(从左数 K，从右数 K，元素自身)。

**示例:**

> **输入:** arr []= { 1，2，3，4，5，6，7，8，9 }，K = 3
> **输出:** {4.85714，4.57143，4.28571，4.0，5.0，6.0，5.71429，5.42857，5.14286}
> ***解释:**每个值的平均值为: **左部:12 &结果:4.28571***
> *为 4–右部:18，左部:6 &结果:4*
> *为 5–右部:21，左部:9 &结果:5*
> *为 6–右部:24，左部:12 &结果:6*
> *为 7–右部:18，*
> 
> **输入:** arr[] = {2，2，2，2，2}，K = 3
> **输出:** {2，2，2，2，2}

**天真方法:**解决问题最简单的方法是遍历数组中每个元素所需的元素数量。遵循以下步骤:

*   遍历数组，对每个元素执行以下操作:
    *   遍历下一个和前一个 K 元素，并计算这些元素的平均值。
*   打印每个元素的答案。

下面是上述方法的实现:

## C++

```
// C++ code to implement the above approach
#include <iostream>
using namespace std;

// Function to calculate average
void average(int arr[], int N, int K)
{
    // Iterate over all elements
    for (int i = 0; i < N; i++) {
        int leftSum = 0;
        int rightSum = 0;
        // find the right sum
        for (int j = 1; j <= K; j++) {
            rightSum += arr[(i + j) % N];
        }
        // Find the leftSum
        for (int j = 1; j <= K; j++) {
            leftSum += arr[(i - j < 0
                                ? i - j + N
                                : i - j)
                           % N];
        }

        // Print mean for each element
        cout << ((leftSum + rightSum + arr[i])
                 * 1.0)
                    / (2 * K + 1)
             << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    int K = 3;
    int N = sizeof(arr) / sizeof(int);

    average(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement the above approach
import java.util.*;
public class GFG{

// Function to calculate average
static void average(int[] arr, int N, int K)
{

    // Iterate over all elements
    for(int i = 0; i < N; i++)
    {
        int leftSum = 0;
        int rightSum = 0;

        // Find the right sum
        for(int j = 1; j <= K; j++)
        {
            rightSum += arr[(i + j) % N];
        }

        // Find the leftSum
        for(int j = 1; j <= K; j++)
        {
            leftSum += arr[(i - j < 0 ? i - j + N : i - j) % N];
        }

        // Print mean for each element
        System.out.print( ((leftSum + rightSum + arr[i]) * 1.0) /
                              (2 * K + 1) + " ");
    }
}

// Driver code
public static void main(String args[])
{
    int[] arr = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    int K = 3;
    int N = arr.length;

    average(arr, N, K);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# code to implement the above approach
using System;

class GFG{

// Function to calculate average
static void average(int[] arr, int N, int K)
{

    // Iterate over all elements
    for(int i = 0; i < N; i++)
    {
        int leftSum = 0;
        int rightSum = 0;

        // Find the right sum
        for(int j = 1; j <= K; j++)
        {
            rightSum += arr[(i + j) % N];
        }

        // Find the leftSum
        for(int j = 1; j <= K; j++)
        {
            leftSum += arr[(i - j < 0 ? i - j + N : i - j) % N];
        }

        // Print mean for each element
        Console.Write( ((leftSum + rightSum + arr[i]) * 1.0) /
                              (2 * K + 1) + " ");
    }
}

// Driver code
public static void Main()
{
    int[] arr = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    int K = 3;
    int N = arr.Length;

    average(arr, N, K);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
  <script>
      // JavaScript code for the above approach

      // Function to calculate average
      function average(arr, N, K)
      {

          // Iterate over all elements
          for (let i = 0; i < N; i++)
          {
              let leftSum = 0;
              let rightSum = 0;

              // find the right sum
              for (let j = 1; j <= K; j++) {
                  rightSum += arr[(i + j) % N];
              }

              // Find the leftSum
              for (let j = 1; j <= K; j++) {
                  leftSum += arr[(i - j < 0
                      ? i - j + N
                      : i - j)
                      % N];
              }

              // Print mean for each element
              document.write((((leftSum + rightSum + arr[i])
                  * 1.0)
                  / (2 * K + 1)).toPrecision(6)
                  + " ");
          }
      }

      // Driver code

      let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
      let K = 3;
      let N = arr.length;

      average(arr, N, K);

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
4.85714 4.57143 4.28571 4 5 6 5.71429 5.42857 5.14286 
```

***时间复杂度:*** O(N*K)
***辅助空间:*** O(1)

**有效方法:**为了降低时间复杂度，可以使用前缀和的概念，其中前缀和数组(比如说推定[])的计算方式类似于推定[i] = arr[0] +。。。+ arr[i]。使用假定[]数组，可以很容易地计算每个元素的平均值，而无需在每次迭代中遍历(2K + 1)个元素。计算每个元素的前 K 个元素(左总和)和后 K 个元素(右总和)之和的条件如下:

> **右侧 K 元素之和的计算:**
> 
> *   如果右侧存在 K 元素:
>     right sum = ProteCt[I+K]–ProteCt[I]；
> *   如果没有正确的元素:
>     rightSum =放肆[k–1]；
> *   如果有些元素在右边，有些需要循环遍历:
>     eleInRight = n–I–1；
>     rightSum =假定[n–1]–假定[i] +假定[k–eleInRight–1]；
> 
> **左侧 K 元素之和的计算:**
> 
> *   如果左侧存在多于 K 个元素:
>     leftSum =假定[I–1]–假定[I–K–1]；
> *   如果左边只有 k 个元素:
>     left sum = PleN[I–1]；
> *   如果左边没有元素:
>     left sum = PleN[n–1]–PleN[n–1–k]；
> *   如果有些元素在左边，有些需要循环遍历:
>     eleInLeft = i
>     leftSum =放肆[I–1]+放肆[n–1]–放肆[n–1 –( k–eleInLeft)]；

按照下面提到的步骤来实现它:

*   迭代数组创建前缀和数组。
*   对于每个元素，获取观察中显示的左右总和，并计算平均值。

下面是上述方法的实现:

## C++

```
// C++ code to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the average
void average(int arr[], int N, int K)
{
    int presum[N];
    presum[0] = arr[0];
    for (int i = 1; i < N; i++) {
        presum[i] = presum[i - 1] + arr[i];
    }

    for (int i = 0; i < N; i++) {

        // Right part
        int rightSum = 0;

        // When all k-elements are
        // in right
        if (i + K < N)
            rightSum = presum[i + K]
                       - presum[i];
        else {
            int eleInRight = N - i - 1;

            // When some are in right and
            // some needs circular traversal
            if (eleInRight > 0) {
                rightSum = presum[N - 1]
                           - presum[i]
                           + presum[K - eleInRight - 1];
            }
            else {
                rightSum = presum[K - eleInRight - 1];
            }
        }

        // Left part
        int leftSum = 0;

        // When more than k-elements
        // are in left
        if (i - K > 0)
            leftSum = presum[i - 1]
                      - presum[i - K - 1];

        // When exact k-elements are in left
        else if (i - K == 0) {
            leftSum = presum[i - 1];
        }

        // When some are in left some
        // needs circular traversal
        else {
            int eleInLeft = i;
            if (eleInLeft > 0) {
                leftSum = presum[i - 1]
                          + presum[N - 1]
                          - presum[N - 1 - (K - eleInLeft)];
            }
            else {
                leftSum = presum[N - 1]
                          - presum[N - 1 - K];
            }
        }
        cout << ((arr[i] + leftSum + rightSum)
                 * 1.0)
                    / (2 * K + 1)
             << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    int K = 3;
    int N = sizeof(arr) / sizeof(int);

    average(arr, N, K);
    return 0;
}
```

## java 描述语言

```
<script>
    // JavaScript code to implement the above approach

    // Function to calculate the average
    const average = (arr, N, K) => {
        let presum = new Array(N).fill(0);
        presum[0] = arr[0];
        for (let i = 1; i < N; i++) {
            presum[i] = presum[i - 1] + arr[i];
        }

        for (let i = 0; i < N; i++) {

            // Right part
            let rightSum = 0;

            // When all k-elements are
            // in right
            if (i + K < N)
                rightSum = presum[i + K]
                    - presum[i];
            else {
                let eleInRight = N - i - 1;

                // When some are in right and
                // some needs circular traversal
                if (eleInRight > 0) {
                    rightSum = presum[N - 1]
                        - presum[i]
                        + presum[K - eleInRight - 1];
                }
                else {
                    rightSum = presum[K - eleInRight - 1];
                }
            }

            // Left part
            let leftSum = 0;

            // When more than k-elements
            // are in left
            if (i - K > 0)
                leftSum = presum[i - 1]
                    - presum[i - K - 1];

            // When exact k-elements are in left
            else if (i - K == 0) {
                leftSum = presum[i - 1];
            }

            // When some are in left some
            // needs circular traversal
            else {
                let eleInLeft = i;
                if (eleInLeft > 0) {
                    leftSum = presum[i - 1]
                        + presum[N - 1]
                        - presum[N - 1 - (K - eleInLeft)];
                }
                else {
                    leftSum = presum[N - 1]
                        - presum[N - 1 - K];
                }
            }
            document.write(`${((arr[i] + leftSum + rightSum)
                * 1.0)
                / (2 * K + 1)} `);
        }
    }

    // Driver code
    let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
    let K = 3;
    let N = arr.length;

    average(arr, N, K);

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
4.85714 4.57143 4.28571 4 5 6 5.71429 5.42857 5.14286 
```

***时间复杂度:*** O(N)
***辅助空间:*** O(N)