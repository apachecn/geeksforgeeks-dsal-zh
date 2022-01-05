# 重新排列数组，使每两个连续元素的乘积为 4 的倍数

> 原文:[https://www . geeksforgeeks . org/重排数组，这样每两个连续元素的乘积就是 4 的倍数/](https://www.geeksforgeeks.org/rearrange-an-array-such-that-product-of-every-two-consecutive-elements-is-a-multiple-of-4/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是重新排列数组元素，使得对于每个索引**I**(1<= I<= N–1)，arr[i]和 arr[I–1]的乘积是 4 的倍数。
**例:**

> **输入:** arr[] = {1，10，100}
> **输出:** 1，100，10
> **解释:**
> 1 * 100 可被 4 整除
> 100 * 10 可被 4 整除
> 
> **输入:** arr[] = {2，7，1，8，2，8}
> 输出: 7，8，1，8，2，2

**天真方法:**
解决这个问题最简单的方法是生成数组所有可能的排列，对于每个排列，检查每两个连续元素的乘积是否是 4 的倍数。

***时间复杂度:** O(N^2 * N！)*
***辅助空间:** O(N！)*

**高效方法:**
按照以下步骤优化上述方法:

*   初始化以下三个变量:
    *   **奇数** =奇数元素**的数量**。
    *   **四个** =可被 4 个整除的元素数量**。**
    *   **非四** =不能被 4 整除的**偶数元素数。**
*   考虑以下两种情况:
    *   **情况 1:非四= 0**
        在这种情况下，不存在不能被 4 整除的偶元素。
        *   最优的方式是先将 ***【奇数】*** 元素先放在阵中的交替位置。
        *   用偶数元素填补空缺。

> ***插图***
> *arr[] = {1，1，1，4，4}*
> *第 0 步:四个= 2，奇数= 3*
> *第 1 步:{1 _ 1 _ 1}*
> *第 2 步:{ 1 4 1 4 }*

*   因此，为了使该方法在数学上可行，偶数和奇数元素的计数之差不应超过 1。
*   **情况 2:非四> 0**

在这种情况下，数组中甚至存在不能被 4 整除的元素。

*   遵循与上面描述的完全相同的策略，将可被 4 整除的元素放在交替的位置，然后在空位中放置奇数元素。
*   然后，将所有剩余的偶数元素放在数组的末尾。这是因为两个偶数的乘积总是能被 4 整除。因此，将偶数元素放在数组的末尾可以保证其中连续元素的乘积可以被 4 整除。

> ***图解:***
> *arr[] = {2，7，1，8，2，8}*
> *第一步:四= 2，非 _ 四= 2，奇数= 2*
> 第二步:{_ 8 _ 8}
> *第三步:{1 8 7 8}*
> *第四步:{ 1 8 7 8 2 }*

*   从数学上来说，这是可能的，四> =奇数。

下面是上述方法的实现:

## C++

```
// C++ Program to rearray array
// elements such that the product
// of every two consecutive
// elements is a multiple of 4

#include <bits/stdc++.h>
using namespace std;

// Function to rearrange array
// elements such that the every
// two consecutive elements is
// a multiple of 4
void Permute(vector<int>& arr,
            int n)
{

    int odd = 0, four = 0;
    int non_four = 0;

    vector<int> ODD, FOUR,
        NON_FOUR;

    for (auto x : arr) {

        // If element is odd
        if (x & 1) {
            odd++;
            // Odd
            ODD.push_back(x);
        }

        // If element is divisible
        // by 4
        else if (x % 4 == 0) {
            four++;
            // Divisible by 4
            FOUR.push_back(x);
        }

        // If element is not
        // divisible by 4
        else {
            non_four++;
            // Even but not divisible
            // by 4
            NON_FOUR.push_back(x);
        }
    }

    // Condition for rearrangement
    // to be possible
    if (non_four == 0
        && four >= odd - 1) {

        int x = ODD.size();
        int y = FOUR.size();
        int i;

        // Print ODD[i] and FOUR[i]
        // consecutively
        for (i = 0; i < x; i++) {
            cout << ODD[i] << " ";
            if (i < y)
                cout << FOUR[i] << " ";
        }

        // Print the remaining
        // FOUR[i], if any
        while (i < y)
            cout << FOUR[i] << " ";
        cout << endl;
    }

    // Condition for rearrangement
    // to be possible
    else if (non_four > 0
            and four >= odd) {

        int x = ODD.size();
        int y = FOUR.size();
        int i;

        // Print ODD[i] and FOUR[i]
        // consecutively
        for (i = 0; i < x; i++) {
            cout << ODD[i] << " ";
            if (i < y)
                cout << FOUR[i] << " ";
        }

        // Print the remaining
        // FOUR[i], if any
        while (i < y)
            cout << FOUR[i] << " ";

        // Print the NON_FOUR[i]
        // elements at the end
        for (int j = 0;
            j < (int)NON_FOUR.size();
            j++)
            cout << NON_FOUR[j] << " ";
        cout << endl;
    }
    else

        // No possible configuration
        cout << "Not Possible" << endl;
}

// Driver Code
signed main()
{

    vector<int> arr = { 2, 7, 1,
                        8, 2, 8 };
    int N = sizeof(arr) / sizeof(arr);
    Permute(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rearray array
// elements such that the product
// of every two consecutive
// elements is a multiple of
import java.io.*;
import java.util.*;

class GFG{

// Function to rearrange array
// elements such that the every
// two consecutive elements is
// a multiple of 4
public static void Permute(Vector<Integer> arr, int n)
{
    int odd = 0, four = 0;
    int non_four = 0;

    Vector<Integer> ODD = new Vector<Integer>();
    Vector<Integer> FOUR = new Vector<Integer>(n);
    Vector<Integer> NON_FOUR = new Vector<Integer>(n);

    for(int x : arr)
    {

        // If element is odd
        if (x % 2 != 0)
        {
            odd++;

            // Odd
            ODD.add(x);
        }

        // If element is divisible
        // by 4
        else if (x % 4 == 0)
        {
            four++;

            // Divisible by 4
            FOUR.add(x);
        }

        // If element is not
        // divisible by 4
        else
        {
            non_four++;

            // Even but not divisible
            // by 4
            NON_FOUR.add(x);
        }
    }

    // Condition for rearrangement
    // to be possible
    if (non_four == 0 && four >= odd - 1)
    {
        int x = ODD.size();
        int y = FOUR.size();
        int i;

        // Print ODD.get(i) and FOUR.get(i)
        // consecutively
        for(i = 0; i < x; i++)
        {
            System.out.print(ODD.get(i) + " ");

            if (i < y)
                System.out.print(FOUR.get(i) + " ");
        }

        // Print the remaining
        // FOUR.get(i), if any
        while (i < y)
            System.out.print(FOUR.get(i) + " ");

        System.out.println();
    }

    // Condition for rearrangement
    // to be possible
    else if (non_four > 0 && four >= odd)
    {
        int x = ODD.size();
        int y = FOUR.size();
        int i;

        // Print ODD.get(i) and FOUR.get(i)
        // consecutively
        for(i = 0; i < x; i++)
        {
            System.out.print(ODD.get(i) + " ");

            if (i < y)
                System.out.print(FOUR.get(i) + " ");
        }

        // Print the remaining
        // FOUR.get(i), if any
        while (i < y)
            System.out.print(FOUR.get(i) + " ");

        // Print the NON_FOUR.get(i)
        // elements at the end
        for(int j = 0; j < (int)NON_FOUR.size(); j++)
            System.out.print(NON_FOUR.get(j) + " ");

        System.out.println();
    }
    else

        // No possible configuration
        System.out.println("Not Possible");
}

// Driver Code
public static void main(String[] args)
{
    Vector<Integer> arr = new Vector<Integer>();
    arr.add(2);
    arr.add(7);
    arr.add(1);
    arr.add(8);
    arr.add(2);
    arr.add(8);

    Permute(arr, arr.size());
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 program to rearray array
# elements such that the product
# of every two consecutive
# elements is a multiple of 4

# Function to rearrange array
# elements such that the every
# two consecutive elements is
# a multiple of 4
def Permute(arr, n):

    odd = 0
    four = 0
    non_four = 0
    ODD, FOUR, NON_FOUR = [], [], []

    for x in arr:

        # If element is odd
        if (x & 1):
            odd += 1

            # Odd
            ODD.append(x)

        # If element is divisible
        # by 4
        elif (x % 4 == 0):
            four += 1

            # Divisible by 4
            FOUR.append(x)

        # If element is not
        # divisible by 4
        else:
            non_four += 1

            # Even but not divisible
            # by 4
            NON_FOUR.append(x)

    # Condition for rearrangement
    # to be possible
    if (non_four == 0 and four >= odd - 1):
        x = len(ODD)
        y = len(FOUR)
        i = 0

        # Print ODD[i] and FOUR[i]
        # consecutively
        while i < x:
            print(ODD[i], end = " ")
            if (i < y):
                print(FOUR[i], end = " ")

        # Print the remaining
        # FOUR[i], if any
        while (i < y):
            print(FOUR[i], end = " ")
            i += 1
        print()

    # Condition for rearrangement
    # to be possible
    elif (non_four > 0 and four >= odd):
        x = len(ODD)
        y = len(FOUR)
        i = 0

        # Print ODD[i] and FOUR[i]
        # consecutively
        while i < x:
            print(ODD[i], end = " ")
            if (i < y):
                print(FOUR[i], end = " ")
            i += 1

        # Print the remaining
        # FOUR[i], if any
        while (i < y):
            print(FOUR[i], end = " ")
            i += 1

        # Print the NON_FOUR[i]
        # elements at the end
        for j in NON_FOUR:
            print(j, end = " ")
    else:

        # No possible configuration
        print("Not Possible")

# Driver Code
if __name__ == '__main__':

    arr = [ 2, 7, 1, 8, 2, 8 ]
    N = len(arr)

    Permute(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to rearray array
// elements such that the product
// of every two consecutive
// elements is a multiple of
using System;
using System.Collections.Generic;
class GFG{

// Function to rearrange array
// elements such that the every
// two consecutive elements is
// a multiple of 4
public static void Permute(List<int> arr,
                           int n)
{
  int odd = 0, four = 0;
  int non_four = 0;

  List<int> ODD =
            new List<int>();
  List<int> FOUR =
            new List<int>(n);
  List<int> NON_FOUR =
            new List<int>(n);

  foreach(int x in arr)
  {
    // If element is odd
    if (x % 2 != 0)
    {
      odd++;

      // Odd
      ODD.Add(x);
    }

    // If element is divisible
    // by 4
    else if (x % 4 == 0)
    {
      four++;

      // Divisible by 4
      FOUR.Add(x);
    }

    // If element is not
    // divisible by 4
    else
    {
      non_four++;

      // Even but not divisible
      // by 4
      NON_FOUR.Add(x);
    }
  }

  // Condition for rearrangement
  // to be possible
  if (non_four == 0 &&
      four >= odd - 1)
  {
    int x = ODD.Count;
    int y = FOUR.Count;
    int i;

    // Print ODD[i] and FOUR[i]
    // consecutively
    for(i = 0; i < x; i++)
    {
      Console.Write(ODD[i] + " ");

      if (i < y)
        Console.Write(FOUR[i] + " ");
    }

    // Print the remaining
    // FOUR[i], if any
    while (i < y)
      Console.Write(FOUR[i] + " ");

    Console.WriteLine();
  }

  // Condition for rearrangement
  // to be possible
  else if (non_four > 0 &&
           four >= odd)
  {
    int x = ODD.Count;
    int y = FOUR.Count;
    int i;

    // Print ODD[i] and FOUR[i]
    // consecutively
    for(i = 0; i < x; i++)
    {
      Console.Write(ODD[i] + " ");

      if (i < y)
        Console.Write(FOUR[i] + " ");
    }

    // Print the remaining
    // FOUR[i], if any
    while (i < y)
      Console.Write(FOUR[i] + " ");

    // Print the NON_FOUR[i]
    // elements at the end
    for(int j = 0;
            j < (int)NON_FOUR.Count; j++)
      Console.Write(NON_FOUR[j] + " ");

    Console.WriteLine();
  }
  else

    // No possible configuration
    Console.WriteLine("Not Possible");
}

// Driver Code
public static void Main(String[] args)
{
  List<int> arr = new List<int>();
  arr.Add(2);
  arr.Add(7);
  arr.Add(1);
  arr.Add(8);
  arr.Add(2);
  arr.Add(8);

  Permute(arr, arr.Count);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to rearray array
// elements such that the product
// of every two consecutive
// elements is a multiple of

// Function to rearrange array
// elements such that the every
// two consecutive elements is
// a multiple of 4
function Permute(arr,n)
{
    let odd = 0, four = 0;
    let non_four = 0;

    let ODD = [];
    let FOUR = [];
    let NON_FOUR = [];

    for(let x = 0; x < arr.length; x++)
    {

        // If element is odd
        if (arr[x] % 2 != 0)
        {
            odd++;

            // Odd
            ODD.push(arr[x]);
        }

        // If element is divisible
        // by 4
        else if (arr[x] % 4 == 0)
        {
            four++;

            // Divisible by 4
            FOUR.push(arr[x]);
        }

        // If element is not
        // divisible by 4
        else
        {
            non_four++;

            // Even but not divisible
            // by 4
            NON_FOUR.push(arr[x]);
        }
    }

    // Condition for rearrangement
    // to be possible
    if (non_four == 0 && four >= odd - 1)
    {
        let x = ODD.length;
        let y = FOUR.length;
        let i;

        // Print ODD.get(i) and FOUR.get(i)
        // consecutively
        for(i = 0; i < x; i++)
        {
            document.write(ODD[i] + " ");

            if (i < y)
                document.write(FOUR[i] + " ");
        }

        // Print the remaining
        // FOUR.get(i), if any
        while (i < y)
            document.write(FOUR[i] + " ");

        document.write("<br>");
    }

    // Condition for rearrangement
    // to be possible
    else if (non_four > 0 && four >= odd)
    {
        let x = ODD.length;
        let y = FOUR.length;
        let i;

        // Print ODD.get(i) and FOUR.get(i)
        // consecutively
        for(i = 0; i < x; i++)
        {
            document.write(ODD[i] + " ");

            if (i < y)
                document.write(FOUR[i] + " ");
        }

        // Print the remaining
        // FOUR.get(i), if any
        while (i < y)
            document.write(FOUR[i] + " ");

        // Print the NON_FOUR.get(i)
        // elements at the end
        for(let j = 0; j < NON_FOUR.length; j++)
            document.write(NON_FOUR[j] + " ");

        document.write("<br>");
    }
    else

        // No possible configuration
        document.write("Not Possible<br>");
}

// Driver Code
let arr=[2,7,1,8,2,8]
Permute(arr, arr.length);

// This code is contributed by patel2127
</script>
```

**输出:**

```
7 8 1 8 2 2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)