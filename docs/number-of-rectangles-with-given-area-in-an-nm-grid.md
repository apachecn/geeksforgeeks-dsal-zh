# N * M 网格中给定面积的矩形数量

> 原文:[https://www . geeksforgeeks . org/纳米网格中给定区域的矩形数量/](https://www.geeksforgeeks.org/number-of-rectangles-with-given-area-in-an-nm-grid/)

给定三个正整数 **N** 、 **M** 和 **A** ，任务是计算 **M * N** 网格中面积等于 **A** 的矩形数量。

**示例:**

> **输入:** N = 2，M = 2，A = 2
> **输出:** 4
> **说明:**
> 在给定的尺寸为 2 × 2 的网格中，可以内接 2 个尺寸为 2 × 1 的矩形和 2 个尺寸为 1 × 2 的矩形。
> 因此，要求输出为 4。
> 
> **输入:** N = 2，M = 2，A = 3
> **输出:** 0
> **说明:**
> 面积 A (= 3)的可能矩形的尺寸为 1 × 3 或 3 × 1。
> 但是，网格中一条边的最大长度只能是 2。因此，网格内不能有矩形。

**方法:**根据以下观察结果可以解决问题:

> 在长度段 **M** 上选择长度段 **X** 的方式总数等于**(M–X+1)**。
> 因此，尺寸 **M * N** 的矩形中尺寸 **X * Y** 的矩形总数等于**(M–X+1)*(N–Y+1)**。

按照以下步骤解决问题:

*   迭代范围**【1，√A】**。每次 **i <sup>第</sup>T5】次迭代，找到矩形长度和宽度的所有可能值，比如说给定网格内的 **{ i，(A / i)}** 或 **{ (A / i)，i }** 。**
*   迭代所有可能的长度值，比如说 **X** 和宽度值，比如说 **Y** ，并将矩形的数量增加**(M–X+1)*(N–Y+1)**。
*   最后，打印获得的计数。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of rectangles
// in an M * N grid such that the area of
// the rectangles is equal to A
int count_number(int N, int M, int A)
{

    // Stores all possible values of length
    // and breadth whose area equal to A
    vector<pair<int, int> > v;

    // Calculate all divisors of A
    for (int i = 1; i * i <= A; i++) {

        // If N is divisible by i
        if (N % i == 0) {

            // Stores length of the rectangle
            int length = i;

            // Stores breadth of the rectangle
            int breadth = A / i;

            // If length of rectangle is not
            // equal to breadth of rectangle
            if (length != breadth) {

                // Insert { length, breadth }
                v.push_back({ length, breadth });

                // Insert { breadth, length }
                v.push_back({ breadth, length });
            }
            else {

                // Insert { length, breadth}
                // because both are equal
                v.push_back({ length, breadth });
            }
        }
    }

    // Stores the count of rectangles
    // in a grid whose area equal to A
    long long total = 0;

    // Iterate over all possible
    // values of { length, breadth }
    for (auto it : v) {

        // Stores total count of ways to
        // select a segment of length it.first
        // on the segment of length M
        int num1 = (max(0, M - it.first + 1));

        // Stores total count of ways to
        // select a segment of length it.second
        // on the segment of length N
        int num2 = (max(0, N - it.second + 1));

        // Update total
        total += (num1 * num2);
    }

    return total;
}

// Drivers Code
int main()
{

    // Input
    int N = 2, M = 2, A = 2;

    // Print the result
    cout << count_number(N, M, A) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;
class GFG
{

static class pair
{
    int first, second;
    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}

// Function to find the count of rectangles
// in an M * N grid such that the area of
// the rectangles is equal to A
static int count_number(int N, int M, int A)
{

    // Stores all possible values of length
    // and breadth whose area equal to A
    Vector<pair> v = new Vector<pair>();

    // Calculate all divisors of A
    for (int i = 1; i * i <= A; i++)
    {

        // If N is divisible by i
        if (N % i == 0)
        {

            // Stores length of the rectangle
            int length = i;

            // Stores breadth of the rectangle
            int breadth = A / i;

            // If length of rectangle is not
            // equal to breadth of rectangle
            if (length != breadth)
            {

                // Insert { length, breadth }
                v.add(new pair(length, breadth));

                // Insert { breadth, length }
                v.add(new pair(breadth, length));
            }
            else
            {

                // Insert { length, breadth}
                // because both are equal
                v.add(new pair(length, breadth));
            }
        }
    }

    // Stores the count of rectangles
    // in a grid whose area equal to A
    int total = 0;

    // Iterate over all possible
    // values of { length, breadth }
    for (pair it : v)
    {

        // Stores total count of ways to
        // select a segment of length it.first
        // on the segment of length M
        int num1 = (Math.max(0, M - it.first + 1));

        // Stores total count of ways to
        // select a segment of length it.second
        // on the segment of length N
        int num2 = (Math.max(0, N - it.second + 1));

        // Update total
        total += (num1 * num2);
    }
    return total;
}

// Drivers Code
public static void main(String[] args)
{

    // Input
    int N = 2, M = 2, A = 2;

    // Print the result
    System.out.print(count_number(N, M, A) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program of the above approach

# Function to find the count of rectangles
# in an M * N grid such that the area of
# the rectangles is equal to A
def count_number(N, M, A):

    # Stores all possible values of length
    # and breadth whose area equal to A
    v = []

    # Calculate all divisors of A
    for i in range(1, A + 1):

        if i * i > A:
            break

        # If N is divisible by i
        if (N % i == 0):

            # Stores length of the rectangle
            length = i

            # Stores breadth of the rectangle
            breadth = A // i

            # If length of rectangle is not
            # equal to breadth of rectangle
            if (length != breadth):

                # Insert { length, breadth }
                v.append([length, breadth ])

                # Insert { breadth, length }
                v.append([breadth, length ])
            else:
                # Insert { length, breadth}
                # because both are equal
                v.append([length, breadth ])

    # Stores the count of rectangles
    # in a grid whose area equal to A
    total = 0

    # Iterate over all possible
    # values of { length, breadth }
    for it in v:

        # Stores total count of ways to
        # select a segment of length it.first
        # on the segment of length M
        num1 = (max(0, M - it[0] + 1))

        # Stores total count of ways to
        # select a segment of length it.second
        # on the segment of length N
        num2 = (max(0, N - it[1] + 1))

        # Update total
        total += (num1 * num2)
    return total

# Drivers Code
if __name__ == '__main__':

    # Input
    N, M, A = 2, 2, 2

    # Print the result
    print(count_number(N, M, A))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG
{

  public class pair 
  { 
    public int first, second; 
    public pair(int first, int second) 
    { 
      this.first = first; 
      this.second = second; 
    } 
  }

  // Function to find the count of rectangles
  // in an M * N grid such that the area of
  // the rectangles is equal to A
  static int count_number(int N, int M, int A)
  {

    // Stores all possible values of length
    // and breadth whose area equal to A
    List<pair> v = new List<pair>();

    // Calculate all divisors of A
    for (int i = 1; i * i <= A; i++)
    {

      // If N is divisible by i
      if (N % i == 0)
      {

        // Stores length of the rectangle
        int length = i;

        // Stores breadth of the rectangle
        int breadth = A / i;

        // If length of rectangle is not
        // equal to breadth of rectangle
        if (length != breadth)
        {

          v.Add(new pair(length, breadth));

          // Insert { breadth, length }
          v.Add(new pair(breadth, length));
        }
        else
        {

          // Insert { length, breadth}
          // because both are equal
          v.Add(new pair(length, breadth));
        }
      }
    }

    // Stores the count of rectangles
    // in a grid whose area equal to A
    int total = 0;

    // Iterate over all possible
    // values of { length, breadth }
    foreach (pair it in v)
    {

      // Stores total count of ways to
      // select a segment of length it.first
      // on the segment of length M
      int num1 = (Math.Max(0, M - it.first + 1));

      // Stores total count of ways to
      // select a segment of length it.second
      // on the segment of length N
      int num2 = (Math.Max(0, N - it.second + 1));

      // Update total
      total += (num1 * num2);
    }
    return total;
  }

  // Driver code
  public static void Main(String[] args)
  {
    // Input
    int N = 2, M = 2, A = 2;

    // Print the result
    Console.Write(count_number(N, M, A) +"\n");
  }
}

// This code is contributed by susmitakundugoaldang
```

## java 描述语言

```
<script>
// Javascript program of the above approach

class pair
{
    constructor(first,second)
    {
        this.first = first;
        this.second = second;
    }
}

function count_number(N,M,A)
{
    // Stores all possible values of length
    // and breadth whose area equal to A
    let v = [];

    // Calculate all divisors of A
    for (let i = 1; i * i <= A; i++)
    {

        // If N is divisible by i
        if (N % i == 0)
        {

            // Stores length of the rectangle
            let length = i;

            // Stores breadth of the rectangle
            let breadth = A / i;

            // If length of rectangle is not
            // equal to breadth of rectangle
            if (length != breadth)
            {

                // Insert { length, breadth }
                v.push(new pair(length, breadth));

                // Insert { breadth, length }
                v.push(new pair(breadth, length));
            }
            else
            {

                // Insert { length, breadth}
                // because both are equal
                v.push(new pair(length, breadth));
            }
        }
    }

    // Stores the count of rectangles
    // in a grid whose area equal to A
    let total = 0;

    // Iterate over all possible
    // values of { length, breadth }
    for (let it=0;it< v.length;it++)
    {

        // Stores total count of ways to
        // select a segment of length it.first
        // on the segment of length M
        let num1 = (Math.max(0, M - v[it].first + 1));

        // Stores total count of ways to
        // select a segment of length it.second
        // on the segment of length N
        let num2 = (Math.max(0, N - v[it].second + 1));

        // Update total
        total += (num1 * num2);
    }
    return total;
}

// Drivers Code
// Input
let N = 2, M = 2, A = 2;

// Print the result
document.write(count_number(N, M, A) +"<br>");

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(sqrt(N))*
***辅助空间:** O(sqrt(N))*