# 一个数组的元素与另一个数组的所有元素的按位异或之和

> 原文:[https://www . geeksforgeeks . org/一个数组的元素与另一个数组的所有元素的按位异或之和/](https://www.geeksforgeeks.org/sum-of-bitwise-xor-of-elements-of-an-array-with-all-elements-of-another-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**arr【】**和一个数组**Q【】**，任务是计算数组**arr【】**所有元素与数组**Q【】**每个元素的[位异或之和。](https://www.geeksforgeeks.org/xor-of-every-element-of-an-array-with-a-given-number-k/)

**示例:**

> **输入:** arr[ ] = {5，2，3}，Q[ ] = {3，8，7}
> **输出:** 7 34 11
> **解释:**
> 为 Q[0] ( = 3):总和= 5 ^ 3 + 2 ^ 3 + 3 ^ 3 = 7。
> 为 Q[1] ( = 8):总和= 5 ^ 8 + 2 ^ 8 + 3 ^ 8 = 34。
> 为 Q[2] ( = 7):总和= 5 ^ 7 + 2 ^ 7 + 3 ^ 7 = 11。
> 
> **输入:** arr[ ] = {2，3，4}，Q[ ] = {1，2}
> **输出:** 10 7

**天真法:**解决问题最简单的方法是遍历数组 **Q[]** ，对于每个数组元素，计算其与数组所有元素 **arr[]** 的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)之和。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**按照以下步骤优化上述方法:

*   初始化一个数组**计数[]** ，大小为 **32** 。在数组元素的每个位置存储设置位的计数 **arr[]。**
*   [穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr】。
*   相应更新数组**计数[]** 。在 **32 位** [二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)中，如果设置了 **i <sup>th</sup>** 位，则增加该位置的设置位[计数](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **Q[]** 并对每个数组元素执行以下操作:
    *   初始化变量，比如**和= 0，**存储按位异或所需的和。
    *   迭代当前元素的每个位位置。
    *   如果设置了当前位，将第 i <sup>个</sup>位未设置的**个元素的计数* 2 <sup>个</sup>** 加到**和**上。
    *   否则，加上**计数【I】* 2<sup>I</sup>T3。**
    *   最后，打印**和**的值。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of Bitwise
// XOR of elements of arr[] with k
int xorSumOfArray(int arr[], int n, int k, int count[])
{

    // Initialize sum to be zero
    int sum = 0;
    int p = 1;

    // Iterate over each set bit
    for (int i = 0; i < 31; i++) {

        // Stores contribution of
        // i-th bet to the sum
        int val = 0;

        // If the i-th bit is set
        if ((k & (1 << i)) != 0) {

            // Stores count of elements
            // whose i-th bit is not set
            int not_set = n - count[i];

            // Update value
            val = ((not_set)*p);
        }
        else {

            // Update value
            val = (count[i] * p);
        }

        // Add value to sum
        sum += val;

        // Move to the next
        // power of two
        p = (p * 2);
    }

    return sum;
}

void sumOfXors(int arr[], int n, int queries[], int q)
{

    // Stores the count of elements
    // whose i-th bit is set
    int count[32];

    // Initialize count to 0
    // for all positions
    memset(count, 0, sizeof(count));

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Iterate over each bit
        for (int j = 0; j < 31; j++) {

            // If the i-th bit is set
            if (arr[i] & (1 << j))

                // Increase count
                count[j]++;
        }
    }

    for (int i = 0; i < q; i++) {
        int k = queries[i];
        cout << xorSumOfArray(arr, n, k, count) << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 5, 2, 3 };
    int queries[] = { 3, 8, 7 };

    int n = sizeof(arr) / sizeof(int);
    int q = sizeof(queries) / sizeof(int);

    sumOfXors(arr, n, queries, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.util.Arrays;

class GFG{

// Function to calculate sum of Bitwise
// XOR of elements of arr[] with k
static int xorSumOfArray(int arr[], int n,
                         int k, int count[])
{

    // Initialize sum to be zero
    int sum = 0;
    int p = 1;

    // Iterate over each set bit
    for(int i = 0; i < 31; i++)
    {

        // Stores contribution of
        // i-th bet to the sum
        int val = 0;

        // If the i-th bit is set
        if ((k & (1 << i)) != 0)
        {

            // Stores count of elements
            // whose i-th bit is not set
            int not_set = n - count[i];

            // Update value
            val = ((not_set)*p);
        }
        else
        {

            // Update value
            val = (count[i] * p);
        }

        // Add value to sum
        sum += val;

        // Move to the next
        // power of two
        p = (p * 2);
    }
    return sum;
}

static void sumOfXors(int arr[], int n,
                      int queries[], int q)
{

    // Stores the count of elements
    // whose i-th bit is set
    int []count = new int[32];

    // Initialize count to 0
    // for all positions
    Arrays.fill(count,0);

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Iterate over each bit
        for(int j = 0; j < 31; j++)
        {

            // If the i-th bit is set
            if  ((arr[i] & (1 << j)) != 0)

                // Increase count
                count[j]++;
        }
    }

    for(int i = 0; i < q; i++)
    {
        int k = queries[i];
        System.out.print(
            xorSumOfArray(arr, n, k, count) + " ");
    }
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 5, 2, 3 };
    int queries[] = { 3, 8, 7 };
    int n = arr.length;
    int q = queries.length;

    sumOfXors(arr, n, queries, q);
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 Program for the above approach

# Function to calculate sum of Bitwise
# XOR of elements of arr[] with k
def xorSumOfArray(arr, n, k, count):

    # Initialize sum to be zero
    sum = 0
    p = 1

    # Iterate over each set bit
    for i in range(31):

        # Stores contribution of
        # i-th bet to the sum
        val = 0

        # If the i-th bit is set
        if ((k & (1 << i)) != 0):

            # Stores count of elements
            # whose i-th bit is not set
            not_set = n - count[i]

            # Update value
            val = ((not_set)*p)

        else:

            # Update value
            val = (count[i] * p)

        # Add value to sum
        sum += val

        # Move to the next
        # power of two
        p = (p * 2)

    return sum

def sumOfXors(arr, n, queries, q):

    # Stores the count of elements
    # whose i-th bit is set
    count = [0 for i in range(32)]

    # Traverse the array
    for i in range(n):

        # Iterate over each bit
        for j in range(31):

            # If the i-th bit is set
            if (arr[i] & (1 << j)):

                # Increase count
                count[j] += 1

    for i in range(q):
        k = queries[i]

        print(xorSumOfArray(arr, n, k, count), end = " ")

# Driver Code
if __name__ == '__main__':

    arr = [ 5, 2, 3 ]
    queries = [ 3, 8, 7 ]
    n = len(arr)
    q = len(queries)

    sumOfXors(arr, n, queries, q)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# Program for the above approach
using System;

public class GFG{

// Function to calculate sum of Bitwise
// XOR of elements of arr[] with k
static int xorSumOfArray(int []arr, int n, int k, int []count)
{

    // Initialize sum to be zero
    int sum = 0;
    int p = 1;

    // Iterate over each set bit
    for (int i = 0; i < 31; i++) {

        // Stores contribution of
        // i-th bet to the sum
        int val = 0;

        // If the i-th bit is set
        if ((k & (1 << i)) != 0) {

            // Stores count of elements
            // whose i-th bit is not set
            int not_set = n - count[i];

            // Update value
            val = ((not_set)*p);
        }
        else {

            // Update value
            val = (count[i] * p);
        }

        // Add value to sum
        sum += val;

        // Move to the next
        // power of two
        p = (p * 2);
    }

    return sum;
}

static void sumOfXors(int []arr, int n, int []queries, int q)
{

    // Stores the count of elements
    // whose i-th bit is set
    int []count = new int[32];

    // Initialize count to 0
    // for all positions

    for(int i = 0; i < 32; i++)
        count[i] = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Iterate over each bit
        for (int j = 0; j < 31; j++) {

            // If the i-th bit is set
            if ((arr[i] & (1 << j)) != 0)

                // Increase count
                count[j]++;
        }
    }

    for (int i = 0; i < q; i++) {
        int k = queries[i];
        Console.Write(xorSumOfArray(arr, n, k, count) + " ");
    }
}

// Driver Code
static public void Main ()
{
    int []arr = { 5, 2, 3 };
    int []queries = { 3, 8, 7 };

    int n = arr.Length;
    int q = queries.Length;

    sumOfXors(arr, n, queries, q);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate sum of Bitwise
// XOR of elements of arr[] with k
function xorSumOfArray(arr, n, k, count)
{

    // Initialize sum to be zero
    var sum = 0;
    var p = 1;

    // Iterate over each set bit
    for(var i = 0; i < 31; i++)
    {

        // Stores contribution of
        // i-th bet to the sum
        var val = 0;

        // If the i-th bit is set
        if ((k & (1 << i)) != 0)
        {

            // Stores count of elements
            // whose i-th bit is not set
            var not_set = n - count[i];

            // Update value
            val = ((not_set)*p);
        }
        else
        {

            // Update value
            val = (count[i] * p);
        }

        // Add value to sum
        sum += val;

        // Move to the next
        // power of two
        p = (p * 2);
    }
    return sum;
}

function sumOfXors(arr, n, queries, q)
{

    // Stores the count of elements
    // whose i-th bit is set
    var count = new Array(32);

    // Initialize count to 0
    // for all positions
    count.fill(0);

    // Traverse the array
    for(var i = 0; i < n; i++)
    {

        // Iterate over each bit
        for(var j = 0; j < 31; j++)
        {

            // If the i-th bit is set
            if (arr[i] & (1 << j))

                // Increase count
                count[j]++;
        }
    }

    for(var i = 0; i < q; i++)
    {
        var k = queries[i];
        document.write(xorSumOfArray(
            arr, n, k, count) + " ");
    }
}

// Driver code
var arr = [ 5, 2, 3 ];
var queries = [ 3, 8, 7 ];
var n = arr.length;
var q = queries.length;

sumOfXors(arr, n, queries, q);

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
7 34 11
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)