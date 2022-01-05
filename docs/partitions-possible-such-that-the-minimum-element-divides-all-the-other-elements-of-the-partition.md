# 可能的分区，使得最小元素划分分区的所有其他元素

> 原文:[https://www . geesforgeks . org/partitions-可能的最小元素划分分区的所有其他元素/](https://www.geeksforgeeks.org/partitions-possible-such-that-the-minimum-element-divides-all-the-other-elements-of-the-partition/)

给定一个整数数组 **arr[]** ，任务是计算可能的分区数量，以便在每个分区中最小元素划分分区的所有其他元素。分区不必是连续的。
**例:**

> **输入:** arr[] = {10，7，20，21，13}
> **输出:** 3
> 可能的分区有{10，20}、{7，21}和{13}。
> 在每个分区中，所有元素都可以被分区的最小元素
> 整除。
> **输入:** arr[] = {7，6，5，4，3，2，2，3}
> **输出:** 4

**进场:**

1.  求数组中不等于 *INT_MAX* 的最小元素。
2.  从可被最小元素整除的数组中移除所有元素(替换为 *INT_MAX* )。
3.  作为操作结果的有效最小元素数是所需的分区数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count partitions
// possible from the given array such that
// the minimum element of any partition
// divides all the other elements
// of that partition
int countPartitions(int A[], int N)
{
    // Initialize the count variable
    int count = 0;

    for (int i = 0; i < N; i++) {

        // Find the minimum element
        int min_elem = *min_element(A, A + N);

        // Break if no minimum element present
        if (min_elem == INT_MAX)
            break;

        // Increment the count if
        // minimum element present
        count++;

        // Replace all the element
        // divisible by min_elem
        for (int i = 0; i < N; i++) {
            if (A[i] % min_elem == 0)
                A[i] = INT_MAX;
        }
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 7, 6, 5, 4, 3, 2, 2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << countPartitions(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    static int INT_MAX = Integer.MAX_VALUE ;

    static int min_element(int []A, int N)
    {
        int min = A[0];
        int i;
        for( i = 1; i < N ; i++)
        {
            if (min > A[i])
            {
                min = A[i];
            }
        }
        return min;
    }

    // Function to return the count partitions
    // possible from the given array such that
    // the minimum element of any partition
    // divides all the other elements
    // of that partition
    static int countPartitions(int []A, int N)
    {
        // Initialize the count variable
        int count = 0;
        int i, j;

        for (i = 0; i < N; i++)
        {

            // Find the minimum element
            int min_elem = min_element(A, N);

            // Break if no minimum element present
            if (min_elem == INT_MAX)
                break;

            // Increment the count if
            // minimum element present
            count++;

            // Replace all the element
            // divisible by min_elem
            for (j = 0; j < N; j++)
            {
                if (A[j] % min_elem == 0)
                    A[j] = INT_MAX;
            }
        }
        return count;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 7, 6, 5, 4, 3, 2, 2, 3 };
        int N = arr.length;

        System.out.println(countPartitions(arr, N));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

INT_MAX = sys.maxsize;

# Function to return the count partitions
# possible from the given array such that
# the minimum element of any partition
# divides all the other elements
# of that partition
def countPartitions(A, N) :

    # Initialize the count variable
    count = 0;

    for i in range(N) :

        # Find the minimum element
        min_elem = min(A);

        # Break if no minimum element present
        if (min_elem == INT_MAX) :
            break;

        # Increment the count if
        # minimum element present
        count += 1;

        # Replace all the element
        # divisible by min_elem
        for i in range(N) :
            if (A[i] % min_elem == 0) :
                A[i] = INT_MAX;

    return count;

# Driver code
if __name__ == "__main__" :

    arr = [ 7, 6, 5, 4, 3, 2, 2, 3 ];
    N = len(arr);

    print(countPartitions(arr, N));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int INT_MAX = int.MaxValue ;

    static int min_element(int []A, int N)
    {
        int min = A[0];
        int i;
        for( i = 1; i < N ; i++)
        {
            if (min > A[i])
            {
                min = A[i];
            }
        }
        return min;
    }

    // Function to return the count partitions
    // possible from the given array such that
    // the minimum element of any partition
    // divides all the other elements
    // of that partition
    static int countPartitions(int []A, int N)
    {
        // Initialize the count variable
        int count = 0;
        int i, j;

        for (i = 0; i < N; i++)
        {

            // Find the minimum element
            int min_elem = min_element(A, N);

            // Break if no minimum element present
            if (min_elem == INT_MAX)
                break;

            // Increment the count if
            // minimum element present
            count++;

            // Replace all the element
            // divisible by min_elem
            for (j = 0; j < N; j++)
            {
                if (A[j] % min_elem == 0)
                    A[j] = INT_MAX;
            }
        }
        return count;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 7, 6, 5, 4, 3, 2, 2, 3 };
        int N = arr.Length;

        Console.WriteLine(countPartitions(arr, N));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
var INT_MAX = 1000000000;

function min_element(A, N)
{
    var min = A[0];
    var i;
    for( i = 1; i < N ; i++)
    {
        if (min > A[i])
        {
            min = A[i];
        }
    }
    return min;
}

// Function to return the count partitions
// possible from the given array such that
// the minimum element of any partition
// divides all the other elements
// of that partition
function countPartitions(A, N)
{
    // Initialize the count variable
    var count = 0;
    var i, j;

    for (i = 0; i < N; i++)
    {

        // Find the minimum element
        var min_elem = min_element(A, N);

        // Break if no minimum element present
        if (min_elem == INT_MAX)
            break;

        // Increment the count if
        // minimum element present
        count++;

        // Replace all the element
        // divisible by min_elem
        for (j = 0; j < N; j++)
        {
            if (A[j] % min_elem == 0)
                A[j] = INT_MAX;
        }
    }
    return count;
}

// Driver code
var arr = [ 7, 6, 5, 4, 3, 2, 2, 3 ];
var N = arr.length;
document.write(countPartitions(arr, N)); 

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N <sup>2</sup> )