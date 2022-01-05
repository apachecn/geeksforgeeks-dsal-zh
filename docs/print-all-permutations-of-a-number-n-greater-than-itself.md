# 打印大于自身 N 的数字的所有排列

> 原文:[https://www . geesforgeks . org/print-number-n 的所有排列-大于自身/](https://www.geeksforgeeks.org/print-all-permutations-of-a-number-n-greater-than-itself/)

给定一个**数 N** ，我们的任务是打印那些大于 N 的整数 N 的排列
T3】示例:T5】

> **输入:** N = 534
> **输出:** 543
> **输入:** N = 324
> **输出:** 342、423、432

**方法:**为了解决这个问题，我们可以使用 C++中的[**next _ arrangement()**](https://www.geeksforgeeks.org/stdnext_permutation-prev_permutation-c/)方法获得 N 的所有字典上较大的排列。得到所有这些数字后，打印出来。
对于其他语言，[找到数字 N 的排列](https://www.geeksforgeeks.org/heaps-algorithm-for-generating-permutations/)打印大于 N 的数字
以下是上述方法的实现:

## C++

```
// C++ implementation to print all the
// permutation greater than the integer N

#include <bits/stdc++.h>
using namespace std;

// Function to print all the permutation
// which are greater than N itself
void printPermutation(int N)
{
    int temp = N, count = 0;

    // Iterate and count the
    // number of digits in N
    while (temp > 0) {
        count++;
        temp /= 10;
    }

    // vector to print the
    // permutations of N
    vector<int> num(count);

    // Store digits of N
    // in the vector num
    while (N > 0) {
        num[count-- - 1] = N % 10;
        N = N / 10;
    }

    // Iterate over every permutation of N
    // which is greater than N
    while (next_permutation(
        num.begin(), num.end())) {

        // Print the current permutation of N
        for (int i = 0; i < num.size(); i++)
            cout << num[i];

        cout << "\n";
    }
}

// Driver Code
int main()
{
    int N = 324;

    printPermutation(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print all the
// permutation greater than the integer N
import java.util.*;
class GFG{

static void printPermutation(int N)
{
    int temp = N, count = 0;

    // Iterate and count the
    // number of digits in N
    while (temp > 0)
    {
      count++;
      temp /= 10;
    }

    // vector to print the
    // permutations of N
    int[] num = new int[count];

    // Store digits of N
    // in the vector num
    while (N > 0)
    {
      num[count-- - 1] = N % 10;
      N = N / 10;
    }

    // Iterate over every permutation of N
    // which is greater than N
    while (next_permutation(num))
    {

      // Print the current permutation of N
      for (int i = 0; i < num.length; i++)
        System.out.print(num[i]);

      System.out.print("\n");
    }
  }

  // Function to print all the permutation
  // which are greater than N itself
  static boolean next_permutation(int[] p)
  {
    for (int a = p.length - 2; a >= 0; --a)
      if (p[a] < p[a + 1])
        for (int b = p.length - 1;; --b)
          if (p[b] > p[a])
          {
            int t = p[a];
            p[a] = p[b];
            p[b] = t;
            for (++a, b = p.length - 1; a < b; ++a, --b)
            {
              t = p[a];
              p[a] = p[b];
              p[b] = t;
            }
            return true;
          }
    return false;
  }

// Driver Code
public static void main(String[] args)
{
  int N = 324;

  printPermutation(N);
}
}

// This code contributed by sapnasingh4991
```

## C#

```
// C# implementation to print all the
// permutation greater than the integer N
using System;
class GFG{

static void printPermutation(int N)
{
    int temp = N, count = 0;

    // Iterate and count the
    // number of digits in N
    while (temp > 0)
    {
      count++;
      temp /= 10;
    }

    // vector to print the
    // permutations of N
    int[] num = new int[count];

    // Store digits of N
    // in the vector num
    while (N > 0)
    {
      num[count-- - 1] = N % 10;
      N = N / 10;
    }

    // Iterate over every permutation of N
    // which is greater than N
    while (next_permutation(num))
    {

      // Print the current permutation of N
      for (int i = 0; i < num.Length; i++)
        Console.Write(num[i]);

      Console.Write("\n");
    }
  }

  // Function to print all the permutation
  // which are greater than N itself
  static bool next_permutation(int[] p)
  {
    for (int a = p.Length - 2; a >= 0; --a)
      if (p[a] < p[a + 1])
        for (int b = p.Length - 1;; --b)
          if (p[b] > p[a])
          {
            int t = p[a];
            p[a] = p[b];
            p[b] = t;
            for (++a, b = p.Length - 1;
                       a < b; ++a, --b)
            {
              t = p[a];
              p[a] = p[b];
              p[b] = t;
            }
            return true;
          }
    return false;
  }

// Driver Code
public static void Main(String[] args)
{
  int N = 324;

  printPermutation(N);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

    // JavaScript implementation to print all the
    // permutation greater than the integer N

    function printPermutation(N)
    {
        let temp = N, count = 0;

        // Iterate and count the
        // number of digits in N
        while (temp > 0)
        {
          count++;
          temp = parseInt(temp / 10, 10);
        }

        // vector to print the
        // permutations of N
        let num = new Array(count);
        num.fill(0);

        // Store digits of N
        // in the vector num
        while (N > 0)
        {
          num[count-- - 1] = N % 10;
          N = parseInt(N / 10, 10);
        }

        // Iterate over every permutation of N
        // which is greater than N
        while (next_permutation(num))
        {

          // Print the current permutation of N
          for (let i = 0; i < num.length; i++)
            document.write(num[i]);

          document.write("</br>");
        }
    }

    // Function to print all the permutation
    // which are greater than N itself
    function next_permutation(p)
    {
      for (let a = p.length - 2; a >= 0; --a)
        if (p[a] < p[a + 1])
          for (let b = p.length - 1;; --b)
            if (p[b] > p[a])
            {
              let t = p[a];
              p[a] = p[b];
              p[b] = t;
              for (++a, b = p.length - 1; a < b; ++a, --b)
              {
                t = p[a];
                p[a] = p[b];
                p[b] = t;
              }
              return true;
            }
      return false;
    }

    let N = 324;

      printPermutation(N);

</script>
```

**Output:** 

```
342
423
432
```