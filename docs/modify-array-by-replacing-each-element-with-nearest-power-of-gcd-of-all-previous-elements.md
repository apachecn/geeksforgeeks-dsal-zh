# 通过将每个元素替换为所有先前元素的 GCD 的最近幂来修改数组

> 原文:[https://www . geeksforgeeks . org/通过用所有先前元素的 gcd 的最近幂替换每个元素来修改数组/](https://www.geeksforgeeks.org/modify-array-by-replacing-each-element-with-nearest-power-of-gcd-of-all-previous-elements/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是用所有前面数组元素的 [**GCD**](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 的最近幂替换每个数组元素。如果存在多个可能的答案，则打印其中任何一个。

**示例:**

> **输入:** arr[] = {4，2，8，2}
> **输出:** 4 1 8 2
> **解释:**
> 对于元素 arr[0]，元素保持不变。
> 对于元素 arr[1]，前面元素的 GCD 为 4。最接近 2 的 4 的幂是 1。
> 对于元素 arr[2]，前面元素的 GCD 为 2。最接近 8 的 2 的幂是 8。
> 对于元素 arr[3]，前面元素的 GCD 为 2。最接近 2 的 2 的幂是 2。
> 因此，修改后的数组变为{4，1，8，2}。
> 
> **输入:** arr[] = {3，6，9，2}
> **输出:** 3 9 9 3

**方法:**给定的问题可以通过计算[前缀 GCD](https://www.geeksforgeeks.org/gcds-of-a-given-index-ranges-in-an-array/) 来解决，然后为每个数组元素找到最接近当前元素的 GCD 的最近幂。以下是一些观察结果:

*   对于最接近 **Y** 的 **X** 的幂的计算，思路是得到 **K** 的值，使得**X<sup>K</sup>T9】和 **Y** 的绝对差最小。**
*   求 **K** 的值，求**原木 <sub>x</sub> (Y)** 的地板值。
*   因此， **K** 和 **(K + 1)** 将是两个整数，对于这两个整数，最近的幂可以是一个可能的值。

按照以下步骤解决问题:

*   初始化一个变量，用**arr【0】**表示**前缀 GCD** ，将**前缀 GCD** 存储到数组的每个索引。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 在索引范围**【1，N】**内，并执行以下步骤:
    *   找到**log<sub>prefixGCD</sub>(arr【I】)**的地板值，说 **K** 。
    *   找到 **(arr[i] <sup>K</sup> )** 和 **(arr[i] <sup>K + 1</sup> )** 的值，检查哪个最接近 **arr[i]** ，并将该值赋给数组的当前索引。
    *   将**前缀**更新为**前缀**和**arr【I】**的 GCD。
*   完成上述步骤后，打印修改后的数组。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the float
// value of log function
int log1(int x, int base)
{
  return int(log(x) / log(base));
}

// Function for finding the nearest
// power of X with respect to Y
int getNP(int x, int y)
{

  // Base Case
  if (y == 1)
    return 1;

  // Find the value of K
  int k = int(log1(x, y));

  // Nearest power of GCD closest to Y
  if (abs(pow(y, k) - x) < abs(pow(y, (k + 1)) - x))
    return pow(y, k);
  return pow(y, (k + 1));

}

// Function to modify the given array
// such that each array element is the
// nearest power of X with respect to Y
vector<int> modifyEle(vector<int> arr)
{
  int prevGCD = arr[0];

  // Traverse the array
  for (int i = 1; i < arr.size(); i++)
  {

    // Find the current number
    int NP = getNP(arr[i], prevGCD);

    // Update the GCD
    prevGCD = __gcd(arr[i], prevGCD);

    // Update the array at the
    // current index
    arr[i] = NP;
  }

  // Return the updated GCD array
  return arr;

}

// Driver Code
int main()
{
  vector<int>arr{4, 2, 8, 2};

  // Function Call
  vector<int> ans = modifyEle(arr);
  cout<<"[";
  for(int i = 0; i < ans.size(); i++)
    if(i < ans.size() - 1)
      cout << ans[i] << ", ";
  else
    cout << ans[i];
  cout << "]";
}

// This code is contributed by SURENDRA_GANGWAR.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

    // gcd
    static int gcd(int x, int y)
    {
        if (x == 0)
            return y;
        return gcd(y % x, x);
    }

    // Function to find the float
    // value of log function
    static int log1(int x, int b)
    {
        return (int)(Math.log(x) / Math.log(b));
    }

    // Function for finding the nearest
    // power of X with respect to Y
    static int getNP(int x, int y)
    {

        // Base Case
        if (y == 1)
            return 1;

        // Find the value of K
        int k = (int)(log1(x, y));

        // Nearest power of GCD closest to Y
        if (Math.abs(Math.pow(y, k) - x)
            < Math.abs(Math.pow(y, (k + 1)) - x))
            return (int)(Math.pow(y, k));
        return (int)(Math.pow(y, (k + 1)));
    }

    // Function to modify the given array
    // such that each array element is the
    // nearest power of X with respect to Y
    static ArrayList<Integer> modifyEle(ArrayList<Integer> arr)
    {
        int prevGCD = arr.get(0);

        // Traverse the array
        for (int i = 1; i < arr.size(); i++) {

            // Find the current number
            int NP = getNP(arr.get(i), prevGCD);

            // Update the GCD
            prevGCD = gcd(arr.get(i), prevGCD);

            // Update the array at the
            // current index
            arr.set(i, NP);
        }

        // Return the updated GCD array
        return arr;
    }

// Driver Code
public static void main(String[] args)
{
    ArrayList<Integer> arr = new ArrayList<Integer>() ;
    arr.add(4);
    arr.add(2);
    arr.add(8);
    arr.add(2);

        // Function Call
        ArrayList<Integer> ans = new ArrayList<Integer>();
        ans = modifyEle(arr);
        System.out.print("[");
        for (int i = 0; i < ans.size(); i++)
            if (i < ans.size() - 1)
                System.out.print(ans.get(i) + ", ");
            else
                System.out.print(ans.get(i));
       System.out.print("]");
}
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python program for the above approach

import math

# Function to find the float
# value of log function
def LOG(x, base):
    return int(math.log(x)/math.log(base))

# Function for finding the nearest
# power of X with respect to Y
def getNP(x, y):

    # Base Case
    if y == 1:
        return 1

    # Find the value of K
    k = int(math.log(x, y))

    # Nearest power of GCD closest to Y
    if abs(y**k - x) < abs(y**(k + 1) - x):
        return y**k

    return y**(k + 1)

# Function to find the GCD of a and b
def GCD(a, b):

      # Base Case
    if b == 0:
        return a

    # Recursively calculate GCD
    return GCD(b, a % b)

# Function to modify the given array
# such that each array element is the
# nearest power of X with respect to Y
def modifyEle(arr):

      # Stores the prefix GCD
    prevGCD = arr[0]

    # Traverse the array
    for i in range(1, len(arr)):

          # Find the current number
        NP = getNP(arr[i], prevGCD)

        # Update the GCD
        prevGCD = GCD(arr[i], prevGCD)

        # Update the array at the
        # current index
        arr[i] = NP

    # Return the updated GCD array
    return arr

# Driver Code
arr = [4, 2, 8, 2]

# Function Call
print(modifyEle(arr))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

    // gcd
    static int gcd(int x, int y)
    {
        if (x == 0)
            return y;
        return gcd(y % x, x);
    }

    // Function to find the float
    // value of log function
    static int log1(int x, int b)
    {
        return (int)(Math.Log(x) / Math.Log(b));
    }

    // Function for finding the nearest
    // power of X with respect to Y
    static int getNP(int x, int y)
    {

        // Base Case
        if (y == 1)
            return 1;

        // Find the value of K
        int k = (int)(log1(x, y));

        // Nearest power of GCD closest to Y
        if (Math.Abs(Math.Pow(y, k) - x)
            < Math.Abs(Math.Pow(y, (k + 1)) - x))
            return (int)(Math.Pow(y, k));
        return (int)(Math.Pow(y, (k + 1)));
    }

    // Function to modify the given array
    // such that each array element is the
    // nearest power of X with respect to Y
    static List<int> modifyEle(List<int> arr)
    {
        int prevGCD = arr[0];

        // Traverse the array
        for (int i = 1; i < arr.Count; i++) {

            // Find the current number
            int NP = getNP(arr[i], prevGCD);

            // Update the GCD
            prevGCD = gcd(arr[i], prevGCD);

            // Update the array at the
            // current index
            arr[i] = NP;
        }

        // Return the updated GCD array
        return arr;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        List<int> arr = new List<int>() { 4, 2, 8, 2 };

        // Function Call
        List<int> ans = new List<int>();
        ans = modifyEle(arr);
        Console.Write("[");
        for (int i = 0; i < ans.Count; i++)
            if (i < ans.Count - 1)
                Console.Write(ans[i] + ", ");
            else
                Console.Write(ans[i]);
        Console.Write("]");
    }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // gcd
      function gcd(x, y) {
        if (x === 0)
            return y;
        return gcd(y % x, x);
      }

      // Function to find the float
      // value of log function
      function log1(x, b) {
        return parseInt(Math.log(x) / Math.log(b));
      }

      // Function for finding the nearest
      // power of X with respect to Y
      function getNP(x, y) {
        // Base Case
        if (y === 1) return 1;

        // Find the value of K
        var k = parseInt(log1(x, y));

        // Nearest power of GCD closest to Y
        if (Math.abs(Math.pow(y, k) - x) <
            Math.abs(Math.pow(y, k + 1) - x))
            return parseInt(Math.pow(y, k));
        return parseInt(Math.pow(y, k + 1));
      }

      // Function to modify the given array
      // such that each array element is the
      // nearest power of X with respect to Y
      function modifyEle(arr) {
          var prevGCD = arr[0];

        // Traverse the array
        for (var i = 1; i < arr.length; i++) {
          // Find the current number
          var NP = getNP(arr[i], prevGCD);

          // Update the GCD
          prevGCD = gcd(arr[i], prevGCD);

          // Update the array at the
          // current index
          arr[i] = NP;
        }

        // Return the updated GCD array
        return arr;
      }

      // Driver Code
      var arr = [4, 2, 8, 2];

      // Function Call
      var ans = [];
      ans = modifyEle(arr);
      document.write("[");
      for (var i = 0; i < ans.length; i++)
          if (i < ans.length - 1)
            document.write(ans[i] + ", ");
        else
            document.write(ans[i]);
      document.write("]");
</script>
```

**Output:** 

```
[4, 1, 8, 2]
```

***时间复杂度:** O(N*log(M))，其中 **M** 是* [*阵的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(1)*