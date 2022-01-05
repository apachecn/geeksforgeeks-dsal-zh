# 给定数组中可被所有数字整除的最大 K 位数

> 原文:[https://www . geesforgeks . org/最大 k 位数可被给定数组中的所有数字整除/](https://www.geeksforgeeks.org/largest-k-digit-number-divisible-by-all-numbers-in-given-array/)

给定一个大小为 **N** 的数组 **arr[]** 和一个整数 **K.** 任务是找到可被 arr[]的所有数整除的**最大 K 位数**。

**示例:**

> **输入:** arr[] = {2，3，5}，K = 3
> **输出:** 990
> **说明:** 990 是可被 2，3，5 整除的最大 3 位数。
> 
> **输入:** arr[] = {91，93，95}，K = 3
> **输出:** -1
> **说明:**没有能被 91，93，95 整除的 3 位数。

**方法:**解决方案基于类似于寻找[最大 K 位数可被 X](https://www.geeksforgeeks.org/largest-k-digit-number-divisible-x/) 整除的思路。遵循下面提到的步骤。

*   [找到数组 arr[]](https://www.geeksforgeeks.org/lcm-of-given-array-elements/) 的所有数字的 **LCM**
*   使用以下公式找出具有 K 个数字的 LCM 的最大倍数:

> LCM(arr)*(10<sup>k</sup>1)/LCM(arr))

下面是上述方法的实现。

## C++

```
// C++ code to implement above approach
#include <bits/stdc++.h>
using namespace std;

   int __gcd(int a, int b)
   {

    // Everything divides 0
    if (a == 0)
      return b;
    if (b == 0)
      return a;

    // Base case
    if (a == b)
      return a;

    // a is greater
    if (a > b)
      return __gcd(a - b, b);

    return __gcd(a, b - a);
   }

  // Function to find LCM of the array
  int findLCM(int arr[], int n, int idx)
  {

    // lcm(a, b) = (a*b / gcd(a, b))
    if (idx == n - 1)
    {
      return arr[idx];
    }
    int a = arr[idx];
    int b = findLCM(arr, n, idx + 1);

    double gcd = __gcd(a, b);

    return (a * (int)floor(b / gcd));
  }

  // Function to find the number
  int findNum(int arr[], int n, int K)
  {
    int  lcm = findLCM(arr, n, 0);
    int ans = (int)floor((pow(10, K) - 1) / lcm);
    ans = (ans) * lcm;

    if (ans == 0)
      return -1;

    return ans;
  }

  // Driver code
  int main()
  {
    int arr[] = { 2, 3, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int K = 3;

    cout << findNum(arr, n, K);
  }

// This code is contributed by Samim Hossain Mondal.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
class GFG
{
  static int __gcd(int a, int b)
  {

    // Everything divides 0
    if (a == 0)
      return b;
    if (b == 0)
      return a;

    // Base case
    if (a == b)
      return a;

    // a is greater
    if (a > b)
      return __gcd(a - b, b);

    return __gcd(a, b - a);
  }

  // Function to find LCM of the array
  static int findLCM(int []arr, int idx)
  {

    // lcm(a, b) = (a*b / gcd(a, b))
    if (idx == arr.length - 1)
    {
      return arr[idx];
    }
    int a = arr[idx];
    int b = findLCM(arr, idx + 1);

    double gcd = __gcd(a, b);

    return (a * (int)Math.floor(b / gcd));
  }

  // Function to find the number
  static int findNum(int []arr, int K)
  {
    int  lcm = findLCM(arr, 0);
    int ans = (int)Math.floor((Math.pow(10, K) - 1) / lcm);
    ans = (ans) * lcm;

    if (ans == 0)
      return -1;

    return ans;
  }

  // Driver code
  public static void main(String []args)
  {
    int []arr = { 2, 3, 5 };
    int K = 3;

    System.out.println(findNum(arr, K));
  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python code to implement above approach
import math

# Function to find LCM of the array
def findLCM(arr, idx):

    # lcm(a, b) = (a*b / gcd(a, b))
    if (idx == len(arr) - 1):
        return arr[idx]

    a = arr[idx]
    b = findLCM(arr, idx + 1)
    return (a * b // math.gcd(a, b))

# Function to find the number
def findNum(arr, K):

    lcm = findLCM(arr, 0)
    ans = (pow(10, K) - 1) // lcm
    ans = (ans)*lcm
    if (ans == 0):
        return -1
    return ans

# Driver code
if __name__ == "__main__":

    arr = [2, 3, 5]
    K = 3
    print(findNum(arr, K))

# This code is contributed by rakeshsahni
```

## C#

```
// C# code to implement above approach
using System;
using System.Collections;
class GFG
{
static int __gcd(int a, int b)
{

    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a - b, b);

    return __gcd(a, b - a);
}

// Function to find LCM of the array
static int findLCM(int []arr, int idx)
{

    // lcm(a, b) = (a*b / gcd(a, b))
    if (idx == arr.Length - 1)
    {
        return arr[idx];
    }
    int a = arr[idx];
    int b = findLCM(arr, idx + 1);

    double gcd = __gcd(a, b);

    return (a * (int)Math.Floor(b / gcd));
}

// Function to find the number
static int findNum(int []arr, int K)
{
    int  lcm = findLCM(arr, 0);
    int ans = (int)Math.Floor((Math.Pow(10, K) - 1) / lcm);
    ans = (ans) * lcm;

    if (ans == 0)
        return -1;

    return ans;
}

// Driver code
public static void Main()
{
int []arr = { 2, 3, 5 };
int K = 3;

Console.Write(findNum(arr, K));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

// JavaScript code to implement above approach
function __gcd(a, b)
{

    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a - b, b);

    return __gcd(a, b - a);
}

// Function to find LCM of the array
function findLCM(arr, idx)
{

    // lcm(a, b) = (a*b / gcd(a, b))
    if (idx == arr.length - 1)
    {
        return arr[idx];
    }
    let a = arr[idx];
    let b = findLCM(arr, idx + 1);
    return Math.floor((a * b / __gcd(a, b)));
}

// Function to find the number
function findNum(arr, K)
{
    let lcm = findLCM(arr, 0);
    let ans = Math.floor((Math.pow(10, K) - 1) / lcm);
    ans = (ans) * lcm;

    if (ans == 0)
        return -1;

    return ans;
}

// Driver code
let arr = [ 2, 3, 5 ];
let K = 3;

document.write(findNum(arr, K));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
990
```

**时间复杂度:** O(N*logD)其中 D 是数组的最大元素
T3】辅助空间: O(1)