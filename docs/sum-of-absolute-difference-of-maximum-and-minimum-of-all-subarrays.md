# 所有子阵列的最大值和最小值的绝对差之和

> 原文:[https://www . geeksforgeeks . org/所有子阵列的最大和最小绝对差之和/](https://www.geeksforgeeks.org/sum-of-absolute-difference-of-maximum-and-minimum-of-all-subarrays/)

给定一个包含 N 个整数的数组 arr，任务是找到所有子数组的最大值和最小值的绝对差之和。

示例:

> **输入:** arr[] = {1，4，3}
> **输出:** 7
> **说明:**以下为六个子阵:
> 【1】:最大–最小值= 1–1 = 0
> 【4】:最大–最小值= 4–4 = 0
> 【3】:最大–最小值= 3–3 = 0
> 【1，4】:最大值–最小值= 4–1 = 3
> 【4， 3]:最大–最小= 4–3 = 1
> 【1，4，3】:最大–最小= 4–1 = 3
> 因此，总和为:0 + 0 + 0 + 3 + 1 + 3 = 7
> 
> **输入:** arr[] = {1，6，3 }
> T3】输出: 13

**方法:**方法是找到所有可能的子阵，并保持它们的最大值和最小值，然后用它们来计算和。现在，按照下面的步骤来解决这个问题:

1.  创建一个变量**和**来存储最终答案并将其初始化为 0。
2.  运行从 **i=0** 到 **i < N** 的循环，在每次迭代中:
    *   创建两个变量 **mx** 和 **mn** 分别存储子阵列的最大值和最小值。
    *   将 **mx** 和 **mn** 初始化为**arr【I】**。
    *   现在，运行从 **j=i** 到 **j < N** 的另一个循环:
        *   该循环的每次迭代用于计算从 **i** 到 **j** 的子阵的最大值和最小值。
        *   因此，将 **mx** 更改为最大输出 **mx** 和**arr【j】**。
        *   并将 **mn** 更改为最小 **mn** 和**arr【j】**。
        *   现在，将 **(mx-mn)** 加到**和**中。
3.  返回 sum 作为这个问题的最终答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum
// of the absolute difference
// of maximum and minimum of all subarrays
int sumOfDiff(vector<int>& arr)
{

    int sum = 0;
    int n = arr.size();

    for (int i = 0; i < n; i++) {
        int mn = arr[i];
        int mx = arr[i];

        for (int j = i; j < n; j++) {
            mx = max(mx, arr[j]);
            mn = min(mn, arr[j]);
            sum += (mx - mn);
        }
    }

    return sum;
}

// Driver Code
int main()
{

    vector<int> arr = { 1, 6, 3 };
    cout << sumOfDiff(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

  // Function to find the sum
  // of the absolute difference
  // of maximum and minimum of all subarrays
  static int sumOfDiff(int []arr)
  {

    int sum = 0;
    int n = arr.length;

    for (int i = 0; i < n; i++) {
      int mn = arr[i];
      int mx = arr[i];

      for (int j = i; j < n; j++) {
        mx = Math.max(mx, arr[j]);
        mn = Math.min(mn, arr[j]);
        sum += (mx - mn);
      }
    }

    return sum;
  }

  // Driver Code
  public static void main(String args[])
  {

    int []arr = { 1, 6, 3 };
    System.out.println(sumOfDiff(arr));
  }
}

// This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the sum of the absolute
// difference of maximum and minimum of all
// subarrays
static int sumOfDiff(int []arr)
{
    int sum = 0;
    int n = arr.Length;

    for(int i = 0; i < n; i++)
    {
        int mn = arr[i];
        int mx = arr[i];

        for(int j = i; j < n; j++)
        {
            mx = Math.Max(mx, arr[j]);
            mn = Math.Min(mn, arr[j]);
            sum += (mx - mn);
        }
    }
    return sum;
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 6, 3 };

    Console.Write(sumOfDiff(arr));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to find the sum
      // of the absolute difference
      // of maximum and minimum of all subarrays
      function sumOfDiff(arr) {

          let sum = 0;
          let n = arr.length;

          for (let i = 0; i < n; i++) {
              let mn = arr[i];
              let mx = arr[i];

              for (let j = i; j < n; j++) {
                  mx = Math.max(mx, arr[j]);
                  mn = Math.min(mn, arr[j]);
                  sum += (mx - mn);
              }
          }

          return sum;
      }

      // Driver Code
      let arr = [1, 6, 3];
      document.write(sumOfDiff(arr));

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
13
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(1)