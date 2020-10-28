# 在给定数组

中对相等的元素对进行计数

给定表示手套长度的 **N** 个整数的数组 **arr []** ，任务是从给定的数组中计算最大可能的手套对。 **注意**手套只能与相同尺寸的手套配对，并且只能是单副手套的一部分。

**示例**：

> **输入**：arr [] = {6，5，2，3，5，2，2，1}
> **输出**：2
> （arr [1]， arr [4]）和（arr [2]，arr [5]）是唯一可能的对。
> 
> **输入**：arr [] = {1、2、3、1、2}。
> **输出**：2

**简单方法**：[对给定数组进行](https://www.geeksforgeeks.org/merge-sort/)排序，以便所有相等的元素彼此相邻。 现在，遍历数组，对于每个元素，如果它等于其旁边的元素，则为有效对，并跳过这两个元素。 否则，当前元素无法与任何其他元素进行有效配对，因此仅跳过当前元素。

下面是上述方法的实现：

## C++ 14

```

// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// possible pairs of gloves
int cntgloves(int arr[], int n)
{
    // To store the required count
    int count = 0;

    // Sort the original array
    sort(arr, arr + n);

    for (int i = 0; i < n - 1;) {

        // A valid pair is found
        if (arr[i] == arr[i + 1]) {
            count++;

            // Skip the elements of
            // the current pair
            i = i + 2;
        }

        // Current elements doesn't make
        // a valid pair with any other element
        else {
            i++;
        }
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 6, 5, 2, 3, 5, 2, 2, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << cntgloves(arr, n);

    return 0;
}

```

## Java

```java

// Java implementation of the approach
import java.util.*;

class GFG {

    // Function to return the maximum
    // possible pairs of gloves
    static int cntgloves(int arr[], int n)
    {
        // Sort the original array
        Arrays.sort(arr);
        int res = 0;
        int i = 0;

        while (i < n) {

            // take first number
            int number = arr[i];
            int count = 1;
            i++;

            // count all duplicates
            while (i < n && arr[i] == number) {
                count++;
                i++;
            }

            // if we spotted number just 2 times, increment
            // result
            if (count >= 2) {
                res = res + count;
            }
        }
        return res / 2; // quotient
    }

    // Driver code
    public static void main(String[] args)
    {

        int arr[] = {6, 5, 2, 3, 5, 2, 2, 1};
        int n = arr.length;

        // Function call
        System.out.println(cntgloves(arr, n));
    }
}

// This code is contributed by Lakhan murmu

```

## Python3

```py

# Python3 implementation of the approach

# Function to return the maximum
# possible pairs of gloves

def cntgloves(arr, n):

    # To store the required count
    count = 0

    # Sort the original array
    arr.sort()
    i = 0
    while i < (n-1):

        # A valid pair is found
        if (arr[i] == arr[i + 1]):
            count += 1

            # Skip the elements of
            # the current pair
            i = i + 2

        # Current elements doesn't make
        # a valid pair with any other element
        else:
            i += 1

    return count

# Driver code
if __name__ == "__main__":

    arr = [6, 5, 2, 3, 5, 2, 2, 1]
    n = len(arr)

    # Function call
    print(cntgloves(arr, n))

    # This code is contributed by AnkitRai01

```

## C#

```cs

// C# implementation of the approach
using System;

class GFG {

    // Function to return the maximum
    // possible pairs of gloves
    static int cntgloves(int[] arr, int n)
    {
        // To store the required count
        int count = 0;

        // Sort the original array
        Array.Sort(arr);

        for (int i = 0; i < n - 1;) {

            // A valid pair is found
            if (arr[i] == arr[i + 1]) {
                count++;

                // Skip the elements of
                // the current pair
                i = i + 2;
            }

            // Current elements doesn't make
            // a valid pair with any other element
            else {
                i++;
            }
        }
        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 6, 5, 2, 3, 5, 2, 2, 1 };
        int n = arr.Length;

        // Function call
        Console.WriteLine(cntgloves(arr, n));
    }
}

// This code is contributed by Princi Singh

```

**Output:** 

```
2

```

**高效方法**，

1）创建一个空哈希表（C++中的 unordered_map，Java 中的 HashMap，Python 中的 Dictionary）

2）存储所有元素的频率。

3）遍历哈希表。 对于每个元素，找到其频率。 对于每个元素，将结果按频率/ 2 递增，



* * *

* * *



