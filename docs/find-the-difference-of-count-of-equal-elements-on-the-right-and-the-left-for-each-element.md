# 求每一个元素左右相等元素个数的差

> 原文:[https://www . geeksforgeeks . org/find-每个元素的右数和左数之差/](https://www.geeksforgeeks.org/find-the-difference-of-count-of-equal-elements-on-the-right-and-the-left-for-each-element/)

给定一个大小为 **N** 的数组 **arr[]** 。任务是为每个元素找到**X–Y**，其中 **X** 是 **j** 的计数，这样 **arr[i] = arr[j]** 和 **j > i** 。 **Y** 是 **j** 的计数，这样 **arr[i] = arr[j]** 和 **j < i** 。
**举例:**

> **输入:** arr[] = {1，2，3，2，1}
> **输出:** 1 1 0 -1 -1
> 对于索引 0，X–Y = 1–0 = 1
> 对于索引 1，X–Y = 1–0 = 1
> 对于索引 2，X–Y = 0–0 = 0
> 对于索引 3，X–Y = 0–1 =-1
> 对于索引 4， x–Y = 0–1 =-1
> **输入:** arr[] = {1，1，1，1，1}
> **输出:** 4 2 0 -2 -4

**方法:**一个有效的方法是使用[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。一个映射存储数组中每个元素的计数，另一个映射计算每个元素剩余的相同元素的数量。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of equal
// elements to the right - count of equal
// elements to the left for each of the element
void right_left(int a[], int n)
{

    // Maps to store the frequency and same
    // elements to the left of an element
    unordered_map<int, int> total, left;

    // Count the frequency of each element
    for (int i = 0; i < n; i++)
        total[a[i]]++;

    for (int i = 0; i < n; i++) {

        // Print the answer for each element
        cout << (total[a[i]] - 1 - (2 * left[a[i]])) << " ";

        // Increment it's left frequency
        left[a[i]]++;
    }
}

// Driver code
int main()
{
    int a[] = { 1, 2, 3, 2, 1 };
    int n = sizeof(a) / sizeof(a[0]);

    right_left(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to find the count of equal
// elements to the right - count of equal
// elements to the left for each of the element
static void right_left(int a[], int n)
{

    // Maps to store the frequency and same
    // elements to the left of an element
    Map<Integer, Integer> total = new HashMap<>();
    Map<Integer, Integer> left = new HashMap<>();

    // Count the frequency of each element
    for (int i = 0; i < n; i++)
        total.put(a[i],
        total.get(a[i]) == null ? 1 :
        total.get(a[i]) + 1);

    for (int i = 0; i < n; i++)
    {

        // Print the answer for each element
        System.out.print((total.get(a[i]) - 1 -
                         (2 * (left.containsKey(a[i]) == true ?
                               left.get(a[i]) : 0))) + " ");

        // Increment it's left frequency
        left.put(a[i],
        left.get(a[i]) == null ? 1 :
        left.get(a[i]) + 1);
    }
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 1, 2, 3, 2, 1 };
    int n = a.length;

    right_left(a, n);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the count of equal
# elements to the right - count of equal
# elements to the left for each of the element
def right_left(a, n) :

    # Maps to store the frequency and same
    # elements to the left of an element
    total = dict.fromkeys(a, 0);
    left = dict.fromkeys(a, 0);

    # Count the frequency of each element
    for i in range(n) :
        if a[i] not in total :
            total[a[i]] = 1
        total[a[i]] += 1;

    for i in range(n) :

        # Print the answer for each element
        print(total[a[i]] - 1 - (2 * left[a[i]]),
                                      end = " ");

        # Increment it's left frequency
        left[a[i]] += 1;

# Driver code
if __name__ == "__main__" :

    a = [ 1, 2, 3, 2, 1 ];
    n = len(a);

    right_left(a, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the count of equal
// elements to the right - count of equal
// elements to the left for each of the element
static void right_left(int []a, int n)
{

    // Maps to store the frequency and same
    // elements to the left of an element
    Dictionary<int, int> total = new Dictionary<int, int>();
    Dictionary<int, int> left = new Dictionary<int, int>();

    // Count the frequency of each element
    for (int i = 0; i < n; i++)
    {
        if(total.ContainsKey(a[i]))
        {
            total[a[i]] = total[a[i]] + 1;
        }
        else{
            total.Add(a[i], 1);
        }
    }

    for (int i = 0; i < n; i++)
    {

        // Print the answer for each element
        Console.Write((total[a[i]] - 1 -
                      (2 * (left.ContainsKey(a[i]) == true ?
                                   left[a[i]] : 0))) + " ");

        // Increment it's left frequency
        if(left.ContainsKey(a[i]))
        {
            left[a[i]] = left[a[i]] + 1;
        }
        else
        {
            left.Add(a[i], 1);
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 1, 2, 3, 2, 1 };
    int n = a.Length;

    right_left(a, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

// Function to find the count of equal
// elements to the right - count of equal
// elements to the left for each of the element
function right_left(a, n)
{

    // Maps to store the frequency and same
    // elements to the left of an element
   let total = new Map();
    let left = new Map();

    // Count the frequency of each element
    for (let i = 0; i < n; i++)
        total.set(a[i],
        total.get(a[i]) == null ? 1 :
        total.get(a[i]) + 1);

    for (let i = 0; i < n; i++)
    {

        // Prlet the answer for each element
        document.write((total.get(a[i]) - 1 -
                         (2 * (left.has(a[i]) == true ?
                               left.get(a[i]) : 0))) + " ");

        // Increment it's left frequency
        left.set(a[i],
        left.get(a[i]) == null ? 1 :
        left.get(a[i]) + 1);
    }
}

    // Driver code

        let a = [ 1, 2, 3, 2, 1 ];
    let n = a.length;

    right_left(a, n);

    // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
1 1 0 -1 -1
```