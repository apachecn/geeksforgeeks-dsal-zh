# 可被 50 整除的最大数字，可由一组仅由 0 和 7s 组成的 N 个数字组成

> 原文:[https://www . geeksforgeeks . org/最大数字可被 50 整除-只能由 0 和 7s 组成的给定 n 位数集合/](https://www.geeksforgeeks.org/largest-number-divisible-by-50-that-can-be-formed-from-a-given-set-of-n-digits-consisting-of-0s-and-7s-only/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**,这些整数或者是 **0** 或者是 **7** ，任务是找到可以使用数组元素形成的最大数，这样它就可以被 **50** 整除。

**示例:**

> **输入:** arr[] = {7，7，7，7，7，7，0，0，0，0，0，0 }
> T3】输出: 777770000000
> 
> **输入:** arr[] = {7，0 }
> T3】输出: 0

**天真方法:**解决这个问题最简单的方法是基于以下观察:

*   想象 **50** 等于 **5 * 10** ，因此插入的任何尾随零将被 **10** 除，作为 **50** 的因子呈现。因此，任务简化为组合 **7** s，使其可被 **5** 整除，对于一个可被 **5** 整除的数，其单位位置应为 **0** 或 **5** 。
    ***时间复杂度:**O(2<sup>N</sup>)*
    ***辅助空间:** O(1)*

**高效方法:**优化上述方法，思路是计算 **7** s 和 **0** s 在数组中出现的频率，生成所需的可被 **50** 整除的数。按照以下步骤解决问题:

1.  计算阵列中出现的 **7** 和 **0** 的数量。
2.  计算 5 的**最近因子与阵列中存在的 **7** 的计数(因为 **35** 是最小因子 **5** ，仅使用 7s 即可获得)**
3.  显示**7**的计算数。
4.  在上面的数字后面附加零。

**要考虑的角案例:**

> *   If the count of 0s in the array is 0 (then, the task is to check whether the count of 7s in the array can be evenly divided by 50.
> *   If the count of 7s is less than 5 and there is no 0 in the array, just print "Impossible".
> *   If the count of 7s is less than 5 and there is 0, simply print' 0'.

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Print the largest number divisible by 50
void printLargestDivisible(int arr[], int N)
{

    int i, count0 = 0, count7 = 0;
    for (i = 0; i < N; i++) {

        // Counting number of 0s and 7s
        if (arr[i] == 0)
            count0++;
        else
            count7++;
    }

    // If count of 7 is divisible by 50
    if (count7 % 50 == 0) {

        while (count7--)
            cout << 7;
        while (count0--)
            cout << 0;
    }

    // If count of 7 is less than 5
    else if (count7 < 5) {

        if (count0 == 0)
            cout << "No";
        else
            cout << "0";
    }

    // If count of 7 is not
    // divisible by 50
    else {

        // Count of groups of 5 in which
        // count of 7s can be grouped
        count7 = count7 - count7 % 5;
        while (count7--)
            cout << 7;
        while (count0--)
            cout << 0;
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 0, 7, 0, 7, 7, 7, 7, 0,
                0, 0, 0, 0, 0, 7, 7, 7 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    printLargestDivisible(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.io.*;
class GFG {

  // Print the largest number divisible by 50
  static void printLargestDivisible(int arr[], int N)
  {

    int i, count0 = 0, count7 = 0;
    for (i = 0; i < N; i++) {

      // Counting number of 0s and 7s
      if (arr[i] == 0)
        count0++;
      else
        count7++;
    }

    // If count of 7 is divisible by 50
    if (count7 % 50 == 0) {

      while (count7 != 0)
      {
        System.out.print(7);
        count7 -= 1;
      }
      while (count0 != 0)
      {
        System.out.print(0);
        count0 -= 1;
      }
    }

    // If count of 7 is less than 5
    else if (count7 < 5) {

      if (count0 == 0)
        System.out.print("No");
      else
        System.out.print( "0");
    }

    // If count of 7 is not
    // divisible by 50
    else {

      // Count of groups of 5 in which
      // count of 7s can be grouped
      count7 = count7 - count7 % 5;
      while (count7 != 0)
      {
        System.out.print(7);
        count7 -= 1;
      }
      while (count0 != 0)
      {
        System.out.print(0);
        count0 -= 1;
      }
    }
  }

  // Driver Code
  public static void main(String[] args)
  {
    // Given array
    int arr[] = { 0, 7, 0, 7, 7, 7, 7, 0,
                 0, 0, 0, 0, 0, 7, 7, 7 };

    // Size of the array
    int N = arr.length;

    printLargestDivisible(arr, N);
  }
}

// This code is contributed by jana_sayantan.
```

## 蟒蛇 3

```
# Python3 Program for the above approach

# Print the largest number divisible by 50
def printLargestDivisible(arr, N) :
    count0 = 0; count7 = 0;
    for i in range(N) :

        # Counting number of 0s and 7s
        if (arr[i] == 0) :
            count0 += 1;
        else :
            count7 += 1;

    # If count of 7 is divisible by 50
    if (count7 % 50 == 0) :
        while (count7) :
            count7 -= 1;
            print(7, end = "");

        while (count0) :
            count0 -= 1;
            print(count0, end = "");

    # If count of 7 is less than 5
    elif (count7 < 5) :

        if (count0 == 0) :
            print("No", end = "");
        else :
            print("0", end = "");

    # If count of 7 is not
    # divisible by 50
    else :

        # Count of groups of 5 in which
        # count of 7s can be grouped
        count7 = count7 - count7 % 5;

        while (count7) :
            count7 -= 1;
            print(7, end = "");

        while (count0) :
            count0 -= 1;
            print(0, end = "");

# Driver Code
if __name__ == "__main__" :

    # Given array
    arr = [ 0, 7, 0, 7, 7, 7, 7, 0, 0, 0, 0, 0, 0, 7, 7, 7 ];

    # Size of the array
    N = len(arr);

    printLargestDivisible(arr, N);

    # This code is contributed by AnkThon
```

## C#

```
// C# program of the above approach
using System;
public class GFG {

  // Print the largest number divisible by 50
  static void printLargestDivisible(int []arr, int N)
  {

    int i, count0 = 0, count7 = 0;
    for (i = 0; i < N; i++)
    {

      // Counting number of 0s and 7s
      if (arr[i] == 0)
        count0++;
      else
        count7++;
    }

    // If count of 7 is divisible by 50
    if (count7 % 50 == 0) {

      while (count7 != 0)
      {
        Console.Write(7);
        count7 -= 1;
      }
      while (count0 != 0)
      {
        Console.Write(0);
        count0 -= 1;
      }
    }

    // If count of 7 is less than 5
    else if (count7 < 5) {

      if (count0 == 0)
        Console.Write("No");
      else
        Console.Write( "0");
    }

    // If count of 7 is not
    // divisible by 50
    else {

      // Count of groups of 5 in which
      // count of 7s can be grouped
      count7 = count7 - count7 % 5;
      while (count7 != 0)
      {
        Console.Write(7);
        count7 -= 1;
      }
      while (count0 != 0)
      {
        Console.Write(0);
        count0 -= 1;
      }
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given array
    int []arr = { 0, 7, 0, 7, 7, 7, 7, 0,
                 0, 0, 0, 0, 0, 7, 7, 7 };

    // Size of the array
    int N = arr.Length;
    printLargestDivisible(arr, N);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript Program for the above approach

// Print the largest number divisible by 50
function printLargestDivisible(arr, N)
{

    var i, count0 = 0, count7 = 0;

    for (i = 0; i < N; i++) {

        // Counting number of 0s and 7s
        if (arr[i] == 0)
            count0++;
        else
            count7++;
    }

    // If count of 7 is divisible by 50
    if (count7 % 50 == 0) {

        while (count7--)
            document.write(7);
        while (count0--)
            document.write(0);
    }

    // If count of 7 is less than 5
    else if (count7 < 5) {

        if (count0 == 0)
            document.write("No");
        else
            document.write("0");
    }

    // If count of 7 is not
    // divisible by 50
    else {

        // Count of groups of 5 in which
        // count of 7s can be grouped
        count7 = count7 - count7 % 5;
        while (count7--)
            document.write(7);
        while (count0--)
            document.write(0);
    }
}

// Driver Code

// Given array
var arr = [ 0, 7, 0, 7, 7, 7, 7, 0,
            0, 0, 0, 0, 0, 7, 7, 7 ];
// Size of the array
var N = arr.length;
printLargestDivisible(arr, N);

</script>
```

**输出:**

```
7777700000000
```

**时间复杂度:** O(N)

**辅助空间:** O(1)