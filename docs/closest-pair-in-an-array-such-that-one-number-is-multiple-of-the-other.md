# 数组中最接近的一对，一个数是另一个数的倍数

> 原文:[https://www . geeksforgeeks . org/最接近数组中的一对，这样一个数就是另一个数的倍数/](https://www.geeksforgeeks.org/closest-pair-in-an-array-such-that-one-number-is-multiple-of-the-other/)

给定一个大小为 **N** 的整数[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到给定数组中最接近的一对，使得一个元素是另一个元素的倍数。如果不存在这样的配对，则打印 **-1** 。

**注意:**最接近对表示任意两个元素的指数之差必须最小。

**示例:**

> **输入:** arr[] = {2，3，4，5，6}
> **输出:** 2 4
> **解释:**
> 唯一可能的对是(2，4)、(2，6)、(3，6)，其中它们之间距离最小的对是(2，4)。
> 
> **输入:** arr[] = { 2，3，6，4，5 }
> **输出:** 3 6
> **解释:**
> 唯一可能的对是(2，4)、(2，6)、(3，6)，其中它们之间距离最小的对是(3，6)。

**方法:**思路是[生成给定数组的所有可能对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，如果一个元素是另一个元素的倍数，则检查数组中是否存在任何元素对，并用当前对更新所需的最小距离。在上述操作打印之后，这对具有它们之间的最小距离，并且一个是另一个的倍数。如果不存在这样的配对，则打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the minimum
// distance pair where one is the
// multiple of the other
void findPair(int a[], int n)
{

  // Initialize the variables
  int min_dist = INT_MAX;
  int index_a = -1, index_b = -1;

  // Iterate for all the elements
  for (int i = 0; i < n; i++)
  {

    // Loop to make pairs
    for (int j = i + 1; j < n; j++)
    {

      // Check for minimum distance
      if (j - i < min_dist)
      {

        // Check if one is a
        // multiple of other
        if (a[i] % a[j] == 0 || a[j] % a[i] == 0)
        {

          // Update the distance
          min_dist = j - i;

          // Store indexes
          index_a = i;
          index_b = j;
        }
      }
    }
  }

  // If no such pair exists
  if (index_a == -1)
  {
    cout << ("-1");
  }

  // Print the answer
  else
  {
    cout << "(" <<  a[index_a]
       <<  ", " <<  a[index_b]  << ")";
  }
}

// Driver Code
int main()
{
  // Given array arr[]
  int a[] = { 2, 3, 4, 5, 6 };
  int n = sizeof(a)/sizeof(int);

  // Function Call
  findPair(a, n);
}

// This code is contributed by rock_cool
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG {

    // Function to find the minimum
    // distance pair where one is the
    // multiple of the other
    public static void
    findPair(int a[], int n)
    {

        // Initialize the variables
        int min_dist = Integer.MAX_VALUE;
        int index_a = -1, index_b = -1;

        // Iterate for all the elements
        for (int i = 0; i < n; i++) {

            // Loop to make pairs
            for (int j = i + 1; j < n; j++) {

                // Check for minimum distance
                if (j - i < min_dist) {

                    // Check if one is a
                    // multiple of other
                    if (a[i] % a[j] == 0
                        || a[j] % a[i] == 0) {

                        // Update the distance
                        min_dist = j - i;

                        // Store indexes
                        index_a = i;
                        index_b = j;
                    }
                }
            }
        }

        // If no such pair exists
        if (index_a == -1) {
            System.out.println("-1");
        }

        // Print the answer
        else {
            System.out.print(
                "(" + a[index_a]
                + ", "
                + a[index_b] + ")");
        }
    }

    // Driver Code
    public static void
        main(String[] args)
    {
        // Given array arr[]
        int a[] = { 2, 3, 4, 5, 6 };
        int n = a.length;

        // Function Call
        findPair(a, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the minimum
# distance pair where one is the
# multiple of the other
def findPair(a, n):

    # Initialize the variables
    min_dist = sys.maxsize
    index_a = -1
    index_b = -1

    # Iterate for all the elements
    for i in range(n):

        # Loop to make pairs
        for j in range(i + 1, n):

            # Check for minimum distance
            if (j - i < min_dist):

                # Check if one is a
                # multiple of other
                if ((a[i] % a[j] == 0) or
                    (a[j] % a[i] == 0)):

                    # Update the distance
                    min_dist = j - i

                    # Store indexes
                    index_a = i
                    index_b = j

    # If no such pair exists
    if (index_a == -1):
        print("-1")

    # Print the answer
    else:
        print("(", a[index_a],
             ", ", a[index_b], ")")

# Driver Code

# Given array arr[]
a = [ 2, 3, 4, 5, 6 ]

n = len(a)

# Function call
findPair(a, n)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum
// distance pair where one is the
// multiple of the other
public static void findPair(int []a, int n)
{

    // Initialize the variables
    int min_dist = int.MaxValue;
    int index_a = -1, index_b = -1;

    // Iterate for all the elements
    for(int i = 0; i < n; i++)
    {

        // Loop to make pairs
        for(int j = i + 1; j < n; j++)
        {

            // Check for minimum distance
            if (j - i < min_dist)
            {

                // Check if one is a
                // multiple of other
                if (a[i] % a[j] == 0 ||
                    a[j] % a[i] == 0)
                {

                    // Update the distance
                    min_dist = j - i;

                    // Store indexes
                    index_a = i;
                    index_b = j;
                }
            }
        }
    }

    // If no such pair exists
    if (index_a == -1)
    {
        Console.WriteLine("-1");
    }

    // Print the answer
    else
    {
        Console.Write("(" + a[index_a] +
                     ", " + a[index_b] + ")");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []a = { 2, 3, 4, 5, 6 };

    int n = a.Length;

    // Function Call
    findPair(a, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum
// distance pair where one is the
// multiple of the other
function findPair(a, n)
{

    // Initialize the variables
    let min_dist = Number.MAX_VALUE;
    let index_a = -1, index_b = -1;

    // Iterate for all the elements
    for(let i = 0; i < n; i++)
    {

        // Loop to make pairs
        for(let j = i + 1; j < n; j++)
        {

            // Check for minimum distance
            if (j - i < min_dist)
            {

                // Check if one is a
                // multiple of other
                if (a[i] % a[j] == 0 ||
                    a[j] % a[i] == 0)
                {

                // Update the distance
                min_dist = j - i;

                // Store indexes
                index_a = i;
                index_b = j;
                }
            }
        }
    }

    // If no such pair exists
    if (index_a == -1)
    {
        document.write("-1");
    }

    // Print the answer
    else
    {
        document.write("(" + a[index_a] +
                      ", " + a[index_b] + ")");
    }
}

// Driver code

// Given array arr[]
let a = [ 2, 3, 4, 5, 6 ];
let n = a.length;

// Function Call
findPair(a, n);

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
(2, 4)
```

**时间复杂度:***O(N<sup>2</sup>)*
T7】辅助空间: *O(1)*