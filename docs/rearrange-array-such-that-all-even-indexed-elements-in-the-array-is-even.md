# 重新排列数组，使数组中所有偶数索引的元素都是偶数

> 原文:[https://www . geesforgeks . org/rearray-array-so-all-even-indexed-array-in-elements-is-even/](https://www.geeksforgeeks.org/rearrange-array-such-that-all-even-indexed-elements-in-the-array-is-even/)

给定一个数组 **arr[]** ，任务是检查是否有可能重新排列数组，使得每个偶数索引(*基于 1 的索引*)包含一个偶数。如果这样的重新安排是不可能的，打印“否”。否则，打印“是”并打印一个可能的排列

**示例:**

> **输入:** arr[] = {2，4，8，3，1}
> **输出:**
> 是
> 3 4 8 2 1
> **输入:** arr[] = {3，3，11，8}
> **输出:**否
> **说明:**由于数组只包含一个偶数元素，所有偶数索引都不能用一个偶数元素填充。

**方法:**
按照以下步骤解决问题:

*   计算给定数组中**偶数**元素的总数。如果计数超过给定数组中偶数索引的总数，则打印“否”。
*   否则，打印“是”。现在，使用两个指针遍历数组，分别指向偶数和奇数索引。
*   对于包含奇数元素的第 I<sup>个索引，使用 **j** 迭代奇数索引，直到遇到偶数元素。</sup>
*   互换**a【I】**和**a【j】**
*   重复以上步骤，直到所有偶数索引都用偶数元素填充。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it the
// array can be rearranged such
// such that every even indices
// contains an even element
void checkPossible(int a[], int n)
{
    // Stores the count of even elements
    int even_no_count = 0;

    // Traverse array to count even numbers
    for (int i = 0; i < n; i++)
    {
        if (a[i] % 2 == 0)
            even_no_count++;
    }

    // If even_no_count exceeds
    // count of even indices
    if (n / 2 > even_no_count)
    {
        cout << "No" << endl;
        return;
    }

    cout << "Yes" << endl;
    int j = 0;
    for (int i = 1; i < n; i += 2)
    {
        if (a[i] % 2 == 0)
            continue;
        else
        {
            while (j < n && a[j] % 2 != 0)
                j += 2;

            a[i] += a[j];
            a[j] = a[i] - a[j];
            a[i] -= a[j];
        }
    }

    for (int i = 0; i < n; i++)
    {
        cout << a[i] << " ";
    }
}

// Driver Code
int main()
{

    int arr[] = { 2, 3, 4, 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    checkPossible(arr, n);
    return 0;
}

// This code is contributed by gauravrajput1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to check if it the
    // array can be rearranged such
    // such that every even indices
    // contains an even element
    static void checkPossible(int a[])
    {
        // Stores the count of even elements
        int even_no_count = 0;

        // Traverse array to count even numbers
        for (int i = 0; i < a.length; i++) {

            if (a[i] % 2 == 0)
                even_no_count++;
        }

        // If even_no_count exceeds
        // count of even indices
        if (a.length / 2 > even_no_count) {
            System.out.println("No");
            return;
        }

        System.out.println("Yes");
        int j = 0;
        for (int i = 1; i < a.length; i += 2) {
            if (a[i] % 2 == 0)
                continue;
            else {
                while (j < a.length && a[j] % 2 != 0)
                    j += 2;

                a[i] += a[j];
                a[j] = a[i] - a[j];
                a[i] -= a[j];
            }
        }

        for (int i = 0; i < a.length; i++) {
            System.out.print(a[i] + " ");
        }
    }

    // Driver Code
    public static void main(String args[])
    {

        int arr[] = { 2, 3, 4, 5, 6, 7 };

        checkPossible(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if it the
# array can be rearranged such
# such that every even indices
# contains an even element
def checkPossible(a, n):

    # Stores the count of even elements
    even_no_count = 0

    # Traverse array to count even numbers
    for i in range(n):
        if (a[i] % 2 == 0):
            even_no_count += 1

    # If even_no_count exceeds
    # count of even indices
    if (n // 2 > even_no_count):
        print("No")
        return

    print("Yes")
    j = 0

    for i in range(1, n, 2):
        if (a[i] % 2 == 0):
            continue

        else:
            while (j < n and a[j] % 2 != 0):
                j += 2

            a[i] += a[j]
            a[j] = a[i] - a[j]
            a[i] -= a[j]

    for i in range(n):
        print(a[i], end = " ")

# Driver Code
arr = [ 2, 3, 4, 5, 6, 7 ]
n = len(arr)

checkPossible(arr, n)

# This code is contributed by code_hunt
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

  // Function to check if it the
  // array can be rearranged such
  // such that every even indices
  // contains an even element
  static void checkPossible(int []a)
  {
    // Stores the count of even elements
    int even_no_count = 0;

    // Traverse array to count even numbers
    for (int i = 0; i < a.Length; i++)
    {
      if (a[i] % 2 == 0)
        even_no_count++;
    }

    // If even_no_count exceeds
    // count of even indices
    if (a.Length / 2 > even_no_count)
    {
      Console.WriteLine("No");
      return;
    }

    Console.WriteLine("Yes");
    int j = 0;
    for (int i = 1; i < a.Length; i += 2)
    {
      if (a[i] % 2 == 0)
        continue;
      else
      {
        while (j < a.Length && a[j] % 2 != 0)
          j += 2;

        a[i] += a[j];
        a[j] = a[i] - a[j];
        a[i] -= a[j];
      }
    }

    for (int i = 0; i < a.Length; i++)
    {
      Console.Write(a[i] + " ");
    }
  }

  // Driver Code
  public static void Main(String []args)
  {
    int []arr = { 2, 3, 4, 5, 6, 7 };

    checkPossible(arr);
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Java Script Program to implement
// the above approach

    // Function to check if it the
    // array can be rearranged such
    // such that every even indices
    // contains an even element
    function checkPossible(a)
    {
        // Stores the count of even elements
        let even_no_count = 0;

        // Traverse array to count even numbers
        for (let i = 0; i < a.length; i++) {

            if (a[i] % 2 == 0)
                even_no_count++;
        }

        // If even_no_count exceeds
        // count of even indices
        if (a.length / 2 > even_no_count) {
            document.write("No<br>");
            return;
        }

        document.write("Yes<br>");
        let j = 0;
        for (let i = 1; i < a.length; i += 2) {
            if (a[i] % 2 == 0)
                continue;
            else {
                while (j < a.length && a[j] % 2 != 0)
                    j += 2;

                a[i] += a[j];
                a[j] = a[i] - a[j];
                a[i] -= a[j];
            }
        }

        for (let i = 0; i < a.length; i++) {
            document.write(a[i] + " ");
        }
    }

    // Driver Code

        let arr = [ 2, 3, 4, 5, 6, 7 ];

        checkPossible(arr);

// This code is contributed by sravan kumar Gottumukkala
</script>
```

**Output:** 

```
Yes
3 2 5 4 7 6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)