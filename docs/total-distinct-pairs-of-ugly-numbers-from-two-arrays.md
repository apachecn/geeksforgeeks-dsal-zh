# 两个数组中完全不同的丑陋数字对

> 原文:[https://www . geeksforgeeks . org/total-distinct-pairs-from-two-array-numbers/](https://www.geeksforgeeks.org/total-distinct-pairs-of-ugly-numbers-from-two-arrays/)

给定两个大小为 **N** 和 **M** 的数组 **arr1[]** 和 **arr2[]** ，其中 **0 ≤ arr1[i]，arr2[i] ≤ 1000** 对于所有有效的 **i** ，任务是从第一个数组中取出一个元素，从第二个数组中取出一个元素，这样两个数组都是丑陋的数字。我们称之为一对(a，b)。你必须找到所有这些不同对的计数。**注**a、b、a 不明显。
难看的数字是唯一质因数为 **2、3 或 5** 的数字。
序列 **1，2，3，4，5，6，8，9，10，12，15，…..**显示前几个难看的数字。按照惯例，包括 1。
**例:**

> **输入:** arr1[] = {7，2，3，14}，arr2[] = {2，11，10}
> **输出:** 4
> 所有不同的对为(2，2)，(2，10)，(3，2)和(3，10)
> **输入:**arr 1[= { 1，2，3}，arr 2[= { 1，1}
> **输出:** 3
> All

**进场:**

*   首先生成所有难看的数字，并将其插入一个[无序 _ 集合](https://www.geeksforgeeks.org/unorderd_set-stl-uses/) s1。
*   再取空[套](https://www.geeksforgeeks.org/set-in-cpp-stl/) s2。
*   运行两个嵌套循环，从两个数组中生成所有可能的对，从第一个数组中获取一个元素(称之为 a)，从第二个数组中获取一个元素(称之为 b)。
*   检查 s1 中是否存在 a。如果是，则检查 arr2[]的每个元素是否也存在于 s1 中。
*   如果 a 和 b 都是难看的数字，那么如果 a 小于 b，则在 s2 中插入对(a，b ),否则插入(b，a)。这样做是为了避免重复。
*   Total pairs 是集合 s2 的大小。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to get the nth ugly number
unsigned uglyNumber(int n)
{

    // To store ugly numbers
    int ugly[n];
    int i2 = 0, i3 = 0, i5 = 0;
    int next_multiple_of_2 = 2;
    int next_multiple_of_3 = 3;
    int next_multiple_of_5 = 5;
    int next_ugly_no = 1;

    ugly[0] = 1;
    for (int i = 1; i < n; i++) {
        next_ugly_no = min(next_multiple_of_2,
                           min(next_multiple_of_3,
                               next_multiple_of_5));
        ugly[i] = next_ugly_no;
        if (next_ugly_no == next_multiple_of_2) {
            i2 = i2 + 1;
            next_multiple_of_2 = ugly[i2] * 2;
        }
        if (next_ugly_no == next_multiple_of_3) {
            i3 = i3 + 1;
            next_multiple_of_3 = ugly[i3] * 3;
        }
        if (next_ugly_no == next_multiple_of_5) {
            i5 = i5 + 1;
            next_multiple_of_5 = ugly[i5] * 5;
        }
    }

    return next_ugly_no;
}

// Function to return the required count of pairs
int totalPairs(int arr1[], int arr2[], int n, int m)
{
    unordered_set<int> s1;
    int i = 1;

    // Insert ugly numbers in set
    // which are less than 1000
    while (1) {
        int next_ugly_number = uglyNumber(i);
        if (next_ugly_number > 1000)
            break;
        s1.insert(next_ugly_number);
        i++;
    }

    // Set is used to avoid duplicate pairs
    set<pair<int, int> > s2;

    for (int i = 0; i < n; i++) {

        // Check if arr1[i] is an ugly number
        if (s1.find(arr1[i]) != s1.end()) {

            for (int j = 0; j < m; j++) {

                // Check if arr2[i] is an ugly number
                if (s1.find(arr2[j]) != s1.end()) {
                    if (arr1[i] < arr2[j])
                        s2.insert(make_pair(arr1[i], arr2[j]));
                    else
                        s2.insert(make_pair(arr2[j], arr1[i]));
                }
            }
        }
    }

    // Return the size of the set s2
    return s2.size();
}

// Driver code
int main()
{
    int arr1[] = { 3, 7, 1 };
    int arr2[] = { 5, 1, 10, 4 };
    int n = sizeof(arr1) / sizeof(arr1[0]);
    int m = sizeof(arr2) / sizeof(arr2[0]);

    cout << totalPairs(arr1, arr2, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
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

// Function to get the nth ugly number
static int uglyNumber(int n)
{

    // To store ugly numbers
    int []ugly = new int[n];
    int i2 = 0, i3 = 0, i5 = 0;
    int next_multiple_of_2 = 2;
    int next_multiple_of_3 = 3;
    int next_multiple_of_5 = 5;
    int next_ugly_no = 1;

    ugly[0] = 1;
    for (int i = 1; i < n; i++)
    {
        next_ugly_no = Math.min(next_multiple_of_2,
                       Math.min(next_multiple_of_3,
                                next_multiple_of_5));
        ugly[i] = next_ugly_no;
        if (next_ugly_no == next_multiple_of_2)
        {
            i2 = i2 + 1;
            next_multiple_of_2 = ugly[i2] * 2;
        }
        if (next_ugly_no == next_multiple_of_3)
        {
            i3 = i3 + 1;
            next_multiple_of_3 = ugly[i3] * 3;
        }
        if (next_ugly_no == next_multiple_of_5)
        {
            i5 = i5 + 1;
            next_multiple_of_5 = ugly[i5] * 5;
        }
    }

    return next_ugly_no;
}

// Function to return the required count of pairs
static int totalPairs(int arr1[], int arr2[],
                      int n, int m)
{
    HashSet<Integer> s1 = new HashSet<Integer>();
    int i = 1;

    // Insert ugly numbers in set
    // which are less than 1000
    while (true)
    {
        int next_ugly_number = uglyNumber(i);
        if (next_ugly_number > 1000)
            break;
        s1.add(next_ugly_number);
        i++;
    }

    // Set is used to avoid duplicate pairs
    HashSet<pair> s2 = new HashSet<pair>();

    for (i = 0; i < n; i++)
    {

        // Check if arr1[i] is an ugly number
        if (s1.contains(arr1[i]))
        {
            for (int j = 0; j < m; j++)
            {

                // Check if arr2[i] is an ugly number
                if (s1.contains(arr2[j]))
                {
                    if (arr1[i] < arr2[j])
                        s2.add(new pair(arr1[i], arr2[j]));
                    else
                        s2.add(new pair(arr2[j], arr1[i]));
                }
            }
        }
    }

    // Return the size of the set s2
    return s2.size();
}

// Driver code
public static void main(String[] args)
{
    int arr1[] = { 3, 7, 1 };
    int arr2[] = { 5, 1, 10, 4 };
    int n = arr1.length;
    int m = arr2.length;

    System.out.println(totalPairs(arr1, arr2, n, m));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to get the nth ugly number
def uglyNumber(n):

    # To store ugly numbers
    ugly = [None] * n
    i2 = i3 = i5 = 0
    next_multiple_of_2 = 2
    next_multiple_of_3 = 3
    next_multiple_of_5 = 5
    next_ugly_no = 1

    ugly[0] = 1
    for i in range(1, n): 
        next_ugly_no = min(next_multiple_of_2,
                        min(next_multiple_of_3,
                            next_multiple_of_5))
        ugly[i] = next_ugly_no
        if (next_ugly_no == next_multiple_of_2): 
            i2 = i2 + 1
            next_multiple_of_2 = ugly[i2] * 2

        if (next_ugly_no == next_multiple_of_3): 
            i3 = i3 + 1
            next_multiple_of_3 = ugly[i3] * 3

        if (next_ugly_no == next_multiple_of_5):
            i5 = i5 + 1
            next_multiple_of_5 = ugly[i5] * 5

    return next_ugly_no

# Function to return the required count of pairs
def totalPairs(arr1, arr2, n, m):

    s1 = set()
    i = 1

    # Insert ugly numbers in set
    # which are less than 1000
    while True: 
        next_ugly_number = uglyNumber(i)
        if (next_ugly_number > 1000):
            break
        s1.add(next_ugly_number)
        i += 1

    # Set is used to avoid duplicate pairs
    s2 = set()

    for i in range(0, n): 

        # Check if arr1[i] is an ugly number
        if arr1[i] in s1: 

            for j in range(0, m): 

                # Check if arr2[i] is an ugly number
                if arr2[j] in s1: 
                    if (arr1[i] < arr2[j]):
                        s2.add((arr1[i], arr2[j]))
                    else:
                        s2.add((arr2[j], arr1[i]))

    # Return the size of the set s2
    return len(s2)

# Driver code
if __name__ == "__main__":

    arr1 = [3, 7, 1] 
    arr2 = [5, 1, 10, 4] 
    n = len(arr1)
    m = len(arr2)

    print(totalPairs(arr1, arr2, n, m))

# This code is contributed by Rituraj Jain
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

// Function to get the nth ugly number
static int uglyNumber(int n)
{

    // To store ugly numbers
    int []ugly = new int[n];
    int i2 = 0, i3 = 0, i5 = 0;
    int next_multiple_of_2 = 2;
    int next_multiple_of_3 = 3;
    int next_multiple_of_5 = 5;
    int next_ugly_no = 1;

    ugly[0] = 1;
    for (int i = 1; i < n; i++)
    {
        next_ugly_no = Math.Min(next_multiple_of_2,
                       Math.Min(next_multiple_of_3,
                                next_multiple_of_5));
        ugly[i] = next_ugly_no;
        if (next_ugly_no == next_multiple_of_2)
        {
            i2 = i2 + 1;
            next_multiple_of_2 = ugly[i2] * 2;
        }
        if (next_ugly_no == next_multiple_of_3)
        {
            i3 = i3 + 1;
            next_multiple_of_3 = ugly[i3] * 3;
        }
        if (next_ugly_no == next_multiple_of_5)
        {
            i5 = i5 + 1;
            next_multiple_of_5 = ugly[i5] * 5;
        }
    }

    return next_ugly_no;
}

// Function to return the required count of pairs
static int totalPairs(int []arr1, int []arr2,
                      int n, int m)
{
    HashSet<int> s1 = new HashSet<int>();
    int i = 1;

    // Insert ugly numbers in set
    // which are less than 1000
    while (true)
    {
        int next_ugly_number = uglyNumber(i);
        if (next_ugly_number > 1000)
            break;
        s1.Add(next_ugly_number);
        i++;
    }

    // Set is used to avoid duplicate pairs
    HashSet<pair> s2 = new HashSet<pair>();

    for (i = 0; i < n; i++)
    {

        // Check if arr1[i] is an ugly number
        if (s1.Contains(arr1[i]))
        {
            for (int j = 0; j < m; j++)
            {

                // Check if arr2[i] is an ugly number
                if (s1.Contains(arr2[j]))
                {
                    if (arr1[i] < arr2[j])
                        s2.Add(new pair(arr1[i],
                                        arr2[j]));
                    else
                        s2.Add(new pair(arr2[j],
                                        arr1[i]));
                }
            }
        }
    }

    // Return the size of the set s2
    return s2.Count;
}

// Driver code
public static void Main(String[] args)
{
    int []arr1 = { 3, 7, 1 };
    int []arr2 = { 5, 1, 10, 4 };
    int n = arr1.Length;
    int m = arr2.Length;

    Console.WriteLine(totalPairs(arr1, arr2, n, m));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to get the nth ugly number
function uglyNumber(n) {

    // To store ugly numbers
    let ugly = new Array(n);
    let i2 = 0, i3 = 0, i5 = 0;
    let next_multiple_of_2 = 2;
    let next_multiple_of_3 = 3;
    let next_multiple_of_5 = 5;
    let next_ugly_no = 1;

    ugly[0] = 1;
    for (let i = 1; i < n; i++) {
        next_ugly_no = Math.min(next_multiple_of_2,
            Math.min(next_multiple_of_3,
                next_multiple_of_5));
        ugly[i] = next_ugly_no;
        if (next_ugly_no == next_multiple_of_2) {
            i2 = i2 + 1;
            next_multiple_of_2 = ugly[i2] * 2;
        }
        if (next_ugly_no == next_multiple_of_3) {
            i3 = i3 + 1;
            next_multiple_of_3 = ugly[i3] * 3;
        }
        if (next_ugly_no == next_multiple_of_5) {
            i5 = i5 + 1;
            next_multiple_of_5 = ugly[i5] * 5;
        }
    }

    return next_ugly_no;
}

// Function to return the required count of pairs
function totalPairs(arr1, arr2, n, m) {
    let s1 = new Set();
    let i = 1;

    // Insert ugly numbers in set
    // which are less than 1000
    while (1) {
        let next_ugly_number = uglyNumber(i);
        if (next_ugly_number > 1000)
            break;
        s1.add(next_ugly_number);
        i++;
    }

    // Set is used to avoid duplicate pairs
    let s2 = new Set();

    for (let i = 0; i < n; i++) {

        // Check if arr1[i] is an ugly number
        if (s1.has(arr1[i])) {

            for (let j = 0; j < m; j++) {

                // Check if arr2[i] is an ugly number
                if (s1.has(arr2[j])) {
                    if (arr1[i] < arr2[j])
                        s2.add([arr1[i], arr2[j]]);
                    else
                        s2.add([arr2[j], arr1[i]]);
                }
            }
        }
    }

    // Return the size of the set s2
    return s2.size;
}

// Driver code

let arr1 = [3, 7, 1];
let arr2 = [5, 1, 10, 4];
let n = arr1.length;
let m = arr2.length;

document.write(totalPairs(arr1, arr2, n, m));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
8
```