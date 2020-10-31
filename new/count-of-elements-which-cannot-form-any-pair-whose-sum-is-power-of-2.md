# 不能形成总和为 2 的幂的任何对的元素计数

> 原文：[https://www.geeksforgeeks.org/count-of-elements-which-cannot-form-any-pair-whose-sum-is-power-of-2/](https://www.geeksforgeeks.org/count-of-elements-which-cannot-form-any-pair-whose-sum-is-power-of-2/)

给定长度为`N`的数组`arr[]`，任务是打印无法与任何其他数组元素成对的数组元素，其总和为 2 的幂。

**范例**：

> **输入**：`arr[] = {6, 2, 11}`
>
> **输出**：1
>
> **说明**：
>
> 因为 6 和 2 可以 与总和 8（`= 2 ^ 3`）形成一对。 因此，仅 11 个必须删除，因为它不构成 2 的幂的和。
>
> **输入**：`arr[] = [1, 1, 1, 1023]`
>
> **输出**：0
>
> **说明**：
>
> 给定的数组元素可以分为以下两对：
>
> `(1, 1)`，和为 2（`= 2 ^ 1`）
>
> `(1, 1024)`，和为 1024（`= 2 ^ 10`）
>
> 因此，不需要删除任何元素。

**方法**：

要解决上述问题，请执行以下步骤：

*   将所有数组元素的频率存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。

*   对于每个数组元素`a[i]`，迭代所有可能的总和`p = {2 ^ 0, 2 ^ 1, ...., 2 ^ 30}`并检查数组中是否存在`p – a [i]`。

*   需要满足以下两个条件之一：

    1.  令`s = p – a[i]`。 如果`s`在数组中出现的次数不止一次，那么由`a[i]`和`p`组成的一对是可能的。

    2.  如果`s`在数组中仅出现一次，则对于可能的对，`s`必须与`a[i]`不同。

    3.  如果以上两个条件都不满足，则由`a[i]`组成的对不可能和为`p`。

*   如果上述两个条件对于当前`a[i]`的任何`p`不满足，则增加`count`，因为`a[i]`无法与任何其他数组元素形成 2 的幂的和。

*   打印`count`的最终值。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to count of
// array elements which do
// not form a pair with sum
// equal to a power of 2
// with any other array element

#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// and return the
// count of elements

int powerOfTwo(int a[], int n)
{
    // Stores the frequencies
    // of every array element

    map<int, int> mp;

    for (int i = 0; i < n; i++)
        mp[a[i]]++;

    // Stores the count
    // of removals

    int count = 0;

    for (int i = 0; i < n; i++) {
        bool f = false;

        // For every element, check if
        // it can form a sum equal to
        // any power of 2 with any other
        // element

        for (int j = 0; j < 31; j++) {

            // Store pow(2, j) - a[i]
            int s = (1 << j) - a[i];

            // Check if s is present
            // in the array
            if (mp.count(s)

                // If frequency of s
                // exceeds 1
                && (mp[s] > 1

                    // If s has frequency 1
                    // but is different from
                    // a[i]
                    || mp[s] == 1 && s != a[i]))

                // Pair possible
                f = true;
        }

        // If no pair possible for
        // the current element

        if (f == false)
            count++;
    }

    // Return the answer
    return count;
}

// Driver Code
int main()
{
    int a[] = { 6, 2, 11 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << powerOfTwo(a, n);

    return 0;
}

```

## Java

```java

// Java program to count of array
// elements which do not form a 
// pair with sum equal to a power
// of 2 with any other array element
import java.util.*;

class GFG{

// Function to calculate and return
// the count of elements
static int powerOfTwo(int a[], int n)
{

    // Stores the frequencies
    // of every array element
    HashMap<Integer, 
            Integer> mp = new HashMap<Integer, 
                                      Integer>();

    for(int i = 0; i < n; i++)
    {
       if(mp.containsKey(a[i]))
       {
           mp.put(a[i], mp.get(a[i]) + 1);
       }
       else
       {
           mp.put(a[i], 1);
       }
    }

    // Stores the count
    // of removals
    int count = 0;

    for(int i = 0; i < n; i++)
    {
       boolean f = false;

       // For every element, check if
       // it can form a sum equal to
       // any power of 2 with any other
       // element
       for(int j = 0; j < 31; j++)
       {

          // Store Math.pow(2, j) - a[i]
          int s = (1 << j) - a[i];

          // Check if s is present
          // in the array
          if (mp.containsKey(s) && 

             // If frequency of s
             // exceeds 1
             (mp.get(s) > 1 || 

              // If s has frequency 1
              // but is different from
              // a[i]
              mp.get(s) == 1 && s != a[i]))

             // Pair possible
             f = true;
       }

       // If no pair possible for
       // the current element
       if (f == false)
           count++;
    }

    // Return the answer
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 6, 2, 11 };
    int n = a.length;

    System.out.print(powerOfTwo(a, n));
}
}

// This code is contributed by Amit Katiyar

```

## Python3

```py

# Python3 program to count of
# array elements which do
# not form a pair with sum
# equal to a power of 2
# with any other array element
from collections import defaultdict

# Function to calculate
# and return the
# count of elements
def powerOfTwo(a, n):

    # Stores the frequencies
    # of every array element
    mp = defaultdict (int)

    for i in range (n):
        mp[a[i]] += 1

    # Stores the count
    # of removals
    count = 0

    for i in range (n):
        f = False

        # For every element, check if
        # it can form a sum equal to
        # any power of 2 with any other
        # element

        for j in range (31):

            # Store pow(2, j) - a[i]
            s = (1 << j) - a[i]

            # Check if s is present
            # in the array
            if (s in mp

                # If frequency of s
                # exceeds 1
                and (mp[s] > 1

                    # If s has frequency 1
                    # but is different from
                    # a[i]
                    or mp[s] == 1 and
                       s != a[i])):

                # Pair possible
                f = True

        # If no pair possible for
        # the current element
        if (f == False):
            count += 1

    # Return the answer
    return count

# Driver Code
if __name__ == "__main__":

    a = [6, 2, 11]
    n = len(a)
    print(powerOfTwo(a, n))

# This code is contributed by Chitranayal

```

## C#

```cs

// C# program to count of array
// elements which do not form a 
// pair with sum equal to a power
// of 2 with any other array element
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate and return
// the count of elements
static int powerOfTwo(int []a, int n)
{

    // Stores the frequencies
    // of every array element
    Dictionary<int, 
               int> mp = new Dictionary<int, 
                                        int>();

    for(int i = 0; i < n; i++)
    {
        if(mp.ContainsKey(a[i]))
        {
            mp[a[i]] = mp[a[i]] + 1;
        }
        else
        {
            mp.Add(a[i], 1);
        }
    }

    // Stores the count
    // of removals
    int count = 0;

    for(int i = 0; i < n; i++)
    {
        bool f = false;

        // For every element, check if
        // it can form a sum equal to
        // any power of 2 with any other
        // element
        for(int j = 0; j < 31; j++)
        {

            // Store Math.Pow(2, j) - a[i]
            int s = (1 << j) - a[i];

            // Check if s is present
            // in the array
            if (mp.ContainsKey(s) && 

                // If frequency of s
                // exceeds 1
                (mp[s] > 1 || 

                // If s has frequency 1
                // but is different from
                // a[i]
                mp[s] == 1 && s != a[i]))

                // Pair possible
                f = true;
        }

        // If no pair possible for
        // the current element
        if (f == false)
            count++;
    }

    // Return the answer
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 6, 2, 11 };
    int n = a.Length;

    Console.Write(powerOfTwo(a, n));
}
}

// This code is contributed by Amit Katiyar 

```

**Output:** 

```
1

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



