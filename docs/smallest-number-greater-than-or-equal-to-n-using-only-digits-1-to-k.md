# 仅使用数字 1 至 K 的大于或等于 N 的最小数字

> 原文:[https://www . geesforgeks . org/最小数字大于或等于 n-仅使用数字-1 到-k/](https://www.geeksforgeeks.org/smallest-number-greater-than-or-equal-to-n-using-only-digits-1-to-k/)

给定一个数字 **N** 和一个整数 **K** ，任务是找到大于或等于 **N** 的最小数字，该数字仅使用第一个 **K** 非零数字(1，2，…，K-1，K)形成。
**示例:**

> **输入:** N = 124，K = 3
> **输出:** 131
> **说明:**
> 大于等于 124 的最小数，只由数字 1、2、3 组成就是 131。
> 
> **输入:** N = 325242，K = 4
> **输出:** 331111

**天真方法:**
最简单的解决方法是从 **N + 1** 开始一个 for 循环，找到由第一个 **K** 数字组成的第一个数字。

**高效解决方案:**

*   为了获得有效的解决方案，我们需要了解一个事实，即最多可以形成 9 位数，直到 10 <sup>10</sup> 。因此，我们将反向迭代数字并检查:
    1.  如果**当前数字> = K** ，则使**数字= 1** 。
    2.  如果**当前数字< K** 之后没有比 **K** 更大的数字**，则**将数字**增加 1，并原样复制所有剩余的数字。**
*   一旦我们迭代了所有的数字，仍然没有找到任何小于 K 的数字，那么我们需要在答案中加上一个数字(1)。

下面是上述方法的实现:

## C++

```
// C++ Program to find the smallest
// number greater than or equal
// to N which is made up of
// first K digits
#include <bits/stdc++.h>
using namespace std;

// Function to count the
// digits greater than K
int CountGreater(int n, int k)
{
    int a = 0;
    while (n) {
        if ((n % 10) > k) {
            a++;
        }
        n = n / 10;
    }
    return a;
}

// Function to print the list
int PrintList(list<int> ans)
{
    for (auto it = ans.begin();
         it != ans.end(); it++)
        cout << *it;
}

// Function to find the number
// greater than or equal to n,
// which is only made of first
// k digits
void getNumber(int n, int k)
{
    int count = CountGreater(n, k);

    // If the number itself
    // satisfy the conditions
    if (count == 0) {
        cout << n;
        return;
    }

    list<int> ans;
    bool changed = false;

    // Check digit from back
    while (n > 0) {
        int digit = n % 10;
        if (changed == true) {
            ans.push_front(digit);
        }
        else {
            // If digit > K is
            // present previously and
            // current digit is less
            // than K
            if (count == 0 && digit < k) {
                ans.push_front(digit + 1);
                changed = true;
            }
            else {
                ans.push_front(1);
                // If current digit is
                // greater than K
                if (digit > k) {
                    count--;
                }
            }
        }
        n = n / 10;
    }

    // If an extra digit needs
    // to be added
    if (changed == false) {
        ans.push_front(1);
    }

    // Print the number
    PrintList(ans);

    return;
}

// Driver Code
int main()
{
    int N = 51234;
    int K = 4;
    getNumber(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest
// number greater than or equal
// to N which is made up of
// first K digits
import java.util.*;

class GFG{

// Function to count the
// digits greater than K
static int CountGreater(int n, int k)
{
    int a = 0;

    while (n > 0)
    {
        if ((n % 10) > k)
        {
            a++;
        }
        n = n / 10;
    }
    return a;
}

// Function to print the list
static void PrintList(List<Integer> ans)
{
    for(int it : ans)
        System.out.print(it);
}

// Function to find the number
// greater than or equal to n,
// which is only made of first
// k digits
static void getNumber(int n, int k)
{
    int count = CountGreater(n, k);

    // If the number itself
    // satisfy the conditions
    if (count == 0)
    {
        System.out.print(n);
        return;
    }

    List<Integer> ans = new LinkedList<>();
    boolean changed = false;

    // Check digit from back
    while (n > 0)
    {
        int digit = n % 10;

        if (changed == true)
        {
            ans.add(0, digit);
        }
        else
        {

            // If digit > K is
            // present previously and
            // current digit is less
            // than K
            if (count == 0 && digit < k)
            {
                ans.add(0, digit + 1);
                changed = true;
            }
            else
            {
                ans.add(0, 1);

                // If current digit is
                // greater than K
                if (digit > k)
                {
                    count--;
                }
            }
        }
        n = n / 10;
    }

    // If an extra digit needs
    // to be added
    if (changed == false)
    {
        ans.add(0, 1);
    }

    // Print the number
    PrintList(ans);

    return;
}

// Driver Code
public static void main(String[] args)
{
    int N = 51234;
    int K = 4;

    getNumber(N, K);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to find the smallest
# number greater than or equal
# to N which is made up of
# first K digits

# Function to count the
# digits greater than K
def CountGreater(n, k):

    a = 0
    while (n > 0):
        if ((n % 10) > k):
            a += 1

        n = n // 10

    return a

# Function to print the list
def PrintList (ans):

    for i in ans:
        print(i, end = '')

# Function to find the number
# greater than or equal to n,
# which is only made of first
# k digits
def getNumber(n, k):

    count = CountGreater(n, k)

    # If the number itself
    # satisfy the conditions
    if (count == 0):
        print(n)
        return

    ans = []
    changed = False

    # Check digit from back
    while (n > 0):
        digit = n % 10
        if (changed == True):
            ans.insert(0, digit)

        else:

            # If digit > K is
            # present previously and
            # current digit is less
            # than K
            if (count == 0 and digit < k):
                ans.insert(0, digit + 1)
                changed = True

            else:
                ans.insert(0, 1)

                # If current digit is
                # greater than K
                if (digit > k):
                    count -= 1

        n = n // 10

    # If an extra digit needs
    # to be added
    if (changed == False):
        ans.insert(0, 1)

    # Print the number
    PrintList(ans)
    return

# Driver Code
N = 51234
K = 4

getNumber(N, K)

# This code is contributed by himanshu77
```

## C#

```
// C# program to find the smallest
// number greater than or equal
// to N which is made up of
// first K digits
using System;
using System.Collections.Generic;
class GFG{

// Function to count the
// digits greater than K
static int CountGreater(int n, int k)
{
  int a = 0;

  while (n > 0)
  {
    if ((n % 10) > k)
    {
      a++;
    }
    n = n / 10;
  }
  return a;
}

// Function to print the list
static void PrintList(List<int> ans)
{
  foreach(int it in ans)
    Console.Write(it);
}

// Function to find the number
// greater than or equal to n,
// which is only made of first
// k digits
static void getNumber(int n, int k)
{
  int count = CountGreater(n, k);

  // If the number itself
  // satisfy the conditions
  if (count == 0)
  {
    Console.Write(n);
    return;
  }

  List<int> ans = new List<int>();
  bool changed = false;

  // Check digit from back
  while (n > 0)
  {
    int digit = n % 10;

    if (changed == true)
    {
      ans.Insert(0, digit);
    }
    else
    {
      // If digit > K is
      // present previously and
      // current digit is less
      // than K
      if (count == 0 && digit < k)
      {
        ans.Insert(0, digit + 1);
        changed = true;
      }
      else
      {
        ans.Insert(0, 1);

        // If current digit is
        // greater than K
        if (digit > k)
        {
          count--;
        }
      }
    }
    n = n / 10;
  }

  // If an extra digit needs
  // to be added
  if (changed == false)
  {
    ans.Insert(0, 1);
  }

  // Print the number
  PrintList(ans);

  return;
}

// Driver Code
public static void Main(String[] args)
{
  int N = 51234;
  int K = 4;
  getNumber(N, K);
}
}

// This code is contributed by Princi Singh
```

**Output:** 

```
111111

```