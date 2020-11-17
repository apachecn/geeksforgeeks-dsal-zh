# 将数组拆分为三个子数组，其中第一和第三子数组的总和相等且最大

> 原文：[https://www.geeksforgeeks.org/split-array-to-three-subarrays-such-that-sum-of-first-and-third-subarray-is-equal-and-maximum/](https://www.geeksforgeeks.org/split-array-to-three-subarrays-such-that-sum-of-first-and-third-subarray-is-equal-and-maximum/)

给定一个由`N`个整数组成的数组，任务是通过将数组精确地分成三个子数组来打印第一个子数组的和，以使第一个和第三个子数组元素的和等于最大。

**注意**：所有元素必须属于一个子数组，并且子数组也可以为空。

**示例**：

> **输入**：`a[] = {1, 3, 1, 1, 4}`
>
> **输出**：5
>
> 将`N`个数字分割为`[1, 3, 1]`，`[]`和`[1, 4]`。
> 
> **输入**：`a[] = {1, 3, 2, 1, 4}`
>
> **输出**：4
>
> 将`N`个数字分割为`[1, 3]`, `[2, 1]`和`[4]`。

**方法 1**

一种**朴素的方法**是检查所有可能的分区，并使用前缀和概念查找分区。 给出第一个子数组最大和的分区就是答案。

**有效方法**如下：

*   存储`N`个数字的[前缀总和和后缀总和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。

*   使用 C++ 中的[`unordered_map`](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)和 Java 中的[`HashMap`](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)来散列后缀总和的索引。

*   从数组的开头进行迭代，并检查前缀和是否存在于当前索引`i`之外的后缀数组中。

*   如果是这样，则检查先前的最大值并相应地进行更新。

下面是上述方法的实现：

## C++

```cpp

// C++ program for Split the array into three
// subarrays such that summation of first
// and third subarray is equal and maximum
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of
// the first subarray
int sumFirst(int a[], int n)
{
    unordered_map<int, int> mp;
    int suf = 0;

    // calculate the suffix sum
    for (int i = n - 1; i >= 0; i--) 
    {
        suf += a[i];
        mp[suf] = i;
    }

    int pre = 0;
    int maxi = -1;

    // iterate from beginning
    for (int i = 0; i < n; i++) 
    {
        // prefix sum
        pre += a[i];

        // check if it exists beyond i
        if (mp[pre] > i)
        {
            // if greater then previous
            // then update maximum
            if (pre > maxi) 
            {
                maxi = pre;
            }
        }
    }

    // First and second subarray empty
    if (maxi == -1)
        return 0;

    // partition done
    else
        return maxi;
}

// Driver Code
int main()
{
    int a[] = { 1, 3, 2, 1, 4 };
    int n = sizeof(a) / sizeof(a[0]);

    // Function call
    cout << sumFirst(a, n);
    return 0;
}

```

## Java

```java

// Java program for Split the array into three
// subarrays such that summation of first
// and third subarray is equal and maximum
import java.util.HashMap;
import java.util.Map;

class GfG {

    // Function to return the sum
    // of the first subarray
    static int sumFirst(int a[], int n)
    {
        HashMap<Integer, Integer> mp = new HashMap<>();
        int suf = 0;

        // calculate the suffix sum
        for (int i = n - 1; i >= 0; i--)
        {
            suf += a[i];
            mp.put(suf, i);
        }

        int pre = 0, maxi = -1;

        // iterate from beginning
        for (int i = 0; i < n; i++) 
        {
            // prefix sum
            pre += a[i];

            // check if it exists beyond i
            if (mp.containsKey(pre) && mp.get(pre) > i) 
            {
                // if greater then previous
                // then update maximum
                if (pre > maxi)
                {
                    maxi = pre;
                }
            }
        }

        // First and second subarray empty
        if (maxi == -1)
            return 0;

        // partition done
        else
            return maxi;
    }

    // Driver code
    public static void main(String[] args)
    {

        int a[] = { 1, 3, 2, 1, 4 };
        int n = a.length;

        // Function call
        System.out.println(sumFirst(a, n));
    }
}

// This code is contributed by Rituraj Jain

```

## Python3

```py

# Python 3 program for Split the array into three
# subarrays such that summation of first
# and third subarray is equal and maximum

# Function to return the sum of
# the first subarray

def sumFirst(a, n):
    mp = {i: 0 for i in range(7)}
    suf = 0
    i = n - 1

    # calculate the suffix sum
    while(i >= 0):
        suf += a[i]
        mp[suf] = i
        i -= 1

    pre = 0
    maxi = -1

    # iterate from beginning
    for i in range(n):

        # prefix sum
        pre += a[i]

        # check if it exists beyond i
        if (mp[pre] > i):

            # if greater then previous
            # then update maximum
            if (pre > maxi):
                maxi = pre

    # First and second subarray empty
    if (maxi == -1):
        return 0

    # partition done
    else:
        return maxi

# Driver Code
if __name__ == '__main__':
    a = [1, 3, 2, 1, 4]
    n = len(a)

    # Function call
    print(sumFirst(a, n))

# This code is contributed by
# Surendra_Gangwar

```

## C#

```cs

// C# program for Split the array into three
// subarrays such that summation of first
// and third subarray is equal and maximum
using System;
using System.Collections.Generic;

class GfG {

    // Function to return the sum
    // of the first subarray
    static int sumFirst(int[] a, int n)
    {
        Dictionary<int, int> mp
            = new Dictionary<int, int>();
        int suf = 0;

        // calculate the suffix sum
        for (int i = n - 1; i >= 0; i--) 
        {
            suf += a[i];
            mp.Add(suf, i);
            if (mp.ContainsKey(suf))
            {
                mp.Remove(suf);
            }
            mp.Add(suf, i);
        }

        int pre = 0, maxi = -1;

        // iterate from beginning
        for (int i = 0; i < n; i++) 
        {

            // prefix sum
            pre += a[i];

            // check if it exists beyond i
            if (mp.ContainsKey(pre) && mp[pre] > i)
            {
                // if greater then previous
                // then update maximum
                if (pre > maxi) 
                {
                    maxi = pre;
                }
            }
        }

        // First and second subarray empty
        if (maxi == -1)
            return 0;

        // partition done
        else
            return maxi;
    }

    // Driver code
    public static void Main(String[] args)
    {

        int[] a = { 1, 3, 2, 1, 4 };
        int n = a.Length;

        // Function call
        Console.WriteLine(sumFirst(a, n));
    }
}

// This code is contributed by Rajput-Ji

```

**输出**：

```
4

```

**方法 2**

**方法**：我们将使用两个指针的概念，其中一个指针将从前面开始，另一个指针从后面开始。 在每次迭代中，比较第一个和最后一个子数组的总和，如果它们相同，则在答案变量中更新总和。

**算法**：

*   将`front_pointer`初始化为 0，并将`back_pointer`初始化为`n-1`。

*   将**前缀和**初始化为`arr[front_pointer]`和**后缀和**为`arr[back_pointer]`。

*   比较总和。

    *   如果前缀和大于后缀和，`back_pointer`减 1，后缀和`+= arr[back_pointer]`。

    *   如果前缀和小于后缀和，`front_pointer`加 1，并且前缀和`+= arr[front_pointer]`。

    *   如果它们相同，将总和更新到`answer`变量，将两个指针都移动了一步，并且将前缀和后缀也都进行相应的更新。

*   继续上述步骤，直到`front_pointer`不小于`back_pointer`。

下面是上述方法的实现：

## C++

```cpp

// C++ program for Split the array into three
// subarrays such that summation of first
// and third subarray is equal and maximum
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of
// the first subarray
int sumFirst(int a[], int n)
{
    // two pointers are initialized
    // one at the front and the other
    // at the back
    int front_pointer = 0;
    int back_pointer = n - 1;

    // prefixsum and suffixsum initialized
    int prefixsum = a[front_pointer];
    int suffixsum = a[back_pointer];

    // answer variable initialized to 0
    int answer = 0;

    while (front_pointer < back_pointer) 
    {
        // if the summation are equal
        if (prefixsum == suffixsum)
        {
            // answer updated
            answer = max(answer, prefixsum);

            // both the pointers are moved by step
            front_pointer++;
            back_pointer--;

            // prefixsum and suffixsum are updated
            prefixsum += a[front_pointer];
            suffixsum += a[back_pointer];
        }
        else if (prefixsum > suffixsum)
        {
            // if prefixsum is more,then back pointer is
            // moved by one step and suffixsum updated.
            back_pointer--;
            suffixsum += a[back_pointer];
        }
        else
        {
            // if prefixsum is less,then front pointer is
            // moved by one step and prefixsum updated.
            front_pointer++;
            prefixsum += a[front_pointer];
        }
    }

    // answer is returned
    return answer;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 2, 1, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << sumFirst(arr, n);

    // This code is contributed by Arif
}

```

**输出**：

```
4

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(1)`。



* * *

* * *



