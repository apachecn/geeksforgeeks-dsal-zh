# 给定数组中可被所有数字整除的最小 K 位数

> 原文:[https://www . geesforgeks . org/最小 k 位数可被给定数组中的所有数字整除/](https://www.geeksforgeeks.org/smallest-k-digit-number-divisible-by-all-numbers-in-given-array/)

给定数组 **arr[]** 。任务是创建最小的 **K** 数字，可被**arr【】**的所有数字整除。

**示例:**

> **输入:** arr[] = {2，3，5}，N = 3
> **输出:** 120
> **说明:** 120 可被 2，3，5 整除
> 
> **输入:** arr[] = {2，6，7，4，5}，N = 5
> T3】输出: 10080

**进场:**这个问题可以用[最低公倍数](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/)解决。按照以下步骤解决给定的问题。

*   [求**arr【】**所有阵元](https://www.geeksforgeeks.org/lcm-of-given-array-elements/)的 LCM。
*   找到具有 **K** 位数的 **LCM** 的倍数。
*   第一个有 **K** 位的数字将是最终答案。
*   最后，返回答案。

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive implementation
int findLCM(vector<int> arr, int idx)
{
    // lcm(a,b) = (a*b/gcd(a,b))
    if (idx == arr.size() - 1) {
        return arr[idx];
    }
    int a = arr[idx];
    int b = findLCM(arr, idx + 1);

    return (a * b / __gcd(a, b));
}

// Finding smallest number with given conditions
int findNum(vector<int>& arr, int N)
{
    int lcm = findLCM(arr, 0);
    int ans = pow(10, N - 1) / lcm;
    ans = (ans + 1) * lcm;
    return ans;
}

// Driver Code
int main()
{
      // Array arr[]
    vector<int> arr = { 2, 3, 5 };
    int N = 3;

      // Function call
    cout << findNum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG {

  static int __gcd(int a, int b) {

    // Everything divides 0
    if (b == 0) {
      return a;
    }

    return __gcd(b, a % b);
  }

  // Recursive implementation
  static int findLCM(int[] arr, int idx)
  {

    // lcm(a,b) = (a*b/gcd(a,b))
    if (idx == arr.length - 1) {
      return arr[idx];
    }
    int a = arr[idx];
    int b = findLCM(arr, idx + 1);

    return (a * b / __gcd(a, b));
  }

  // Finding smallest number with given conditions
  static int findNum(int[] arr, int N) {
    int lcm = findLCM(arr, 0);
    int ans = (int) Math.pow(10, N - 1) / lcm;
    ans = (ans + 1) * lcm;
    return ans;
  }

  // Driver Code
  public static void main(String args[])
  {

    // Array arr[]
    int[] arr = { 2, 3, 5 };
    int N = 3;

    // Function call
    System.out.println(findNum(arr, N));

  }
}

// This code is contributed b saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python 3 program for above approach
import math
# Recursive implementation
def findLCM(arr, idx):

    # lcm(a,b) = (a*b/gcd(a,b))
    if (idx == len(arr) - 1):
        return arr[idx]

    a = arr[idx]
    b = findLCM(arr, idx + 1)

    return (a * b // math.gcd(a, b))

# Finding smallest number with given conditions

def findNum(arr, N):

    lcm = findLCM(arr, 0)
    ans = pow(10, N - 1) // lcm
    ans = (ans + 1) * lcm
    return ans

# Driver Code
if __name__ == "__main__":

    # Array arr[]
    arr = [2, 3, 5]
    N = 3

    # Function call
    print(findNum(arr, N))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for above approach
using System;
class GFG {

  static int __gcd(int a, int b) {

    // Everything divides 0
    if (b == 0) {
      return a;
    }

    return __gcd(b, a % b);
  }

  // Recursive implementation
  static int findLCM(int[] arr, int idx)
  {

    // lcm(a,b) = (a*b/gcd(a,b))
    if (idx == arr.Length - 1) {
      return arr[idx];
    }
    int a = arr[idx];
    int b = findLCM(arr, idx + 1);

    return (a * b / __gcd(a, b));
  }

  // Finding smallest number with given conditions
  static int findNum(int[] arr, int N) {
    int lcm = findLCM(arr, 0);
    int ans = (int) Math.Pow(10, N - 1) / lcm;
    ans = (ans + 1) * lcm;
    return ans;
  }

  // Driver Code
  public static void Main(string []args)
  {

    // Array arr[]
    int[] arr = { 2, 3, 5 };
    int N = 3;

    // Function call
    Console.WriteLine(findNum(arr, N));

  }
}

// This code is contributed by gaurav01.
```

## java 描述语言

```
<script>
        // JavaScript code for the above approach
        function __gcd(a, b) {

            // Everything divides 0
            if (b == 0) {
                return a;
            }

            return __gcd(b, a % b);
        }

        // Recursive implementation
        function findLCM(arr, idx)
        {

            // lcm(a,b) = (a*b/gcd(a,b))
            if (idx == arr.length - 1) {
                return arr[idx];
            }
            let a = arr[idx];
            let b = findLCM(arr, idx + 1);

            return (a * b / __gcd(a, b));
        }

        // Finding smallest number with given conditions
        function findNum(arr, N) {
            let lcm = findLCM(arr, 0);
            let ans = Math.floor(Math.pow(10, N - 1) / lcm);
            ans = (ans + 1) * lcm;
            return ans;
        }

        // Driver Code

        // Array arr[]
        let arr = [2, 3, 5];
        let N = 3;

        // Function call
        document.write(findNum(arr, N));

  // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
120
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)