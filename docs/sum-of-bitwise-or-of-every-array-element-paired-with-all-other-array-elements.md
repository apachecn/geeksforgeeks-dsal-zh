# 与所有其他数组元素配对的每个数组元素的按位“或”之和

> 原文:[https://www . geeksforgeeks . org/每一个数组元素与所有其他数组元素的按位或和/](https://www.geeksforgeeks.org/sum-of-bitwise-or-of-every-array-element-paired-with-all-other-array-elements/)

给定一个由非负整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，每个数组元素 **arr[i]** 的任务是打印所有对 **(arr[i]，arr[j])** ( *0 ≤ j ≤ N* )的**和**。

**示例:**

> **输入:** arr[] = {1，2，3， 4}
> **输出:** 12 14 16 22
> **说明:**
> 对于 **i = 0** 所需的和将是**(1 | 1)+(1 | 2)+(1 | 3)+(1 | 4)= 12**
> 对于 **i = 1** 所需的和将是 **(2 | 1) + (2 | 2) + (2 | 3) +) = 14**
> 对于 **i = 2** 所需的总和将是**(3 | 1)+(3 | 2)+(3 | 3)+(3 | 4)= 16**
> 对于 **i = 3** 所需的总和将是**(4 | 1)+(4 | 2)+(4 | 3)+(4 | 4)= 22**
> 
> **输入:** arr[] = {3，2，5，4，8}
> **输出:** 31 28 37 34 54

**朴素方法:**对于每个数组元素 **arr[i]** 最简单的方法是遍历数组，计算所有可能的 **(arr[i]，arr[j])** 的**按位 OR** 之和，并打印得到的**之和**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print required sum for
// every valid index i
void printORSumforEachElement(int arr[], int N)
{
    for (int i = 0; i < N; i++) {

        // Store the required sum
        // for current array element
        int req_sum = 0;

        // Generate all possible pairs (arr[i], arr[j])
        for (int j = 0; j < N; j++) {

            // Update the value of req_sum
            req_sum += (arr[i] | arr[j]);
        }

        // Print the required sum
        cout << req_sum << " ";
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 2, 3, 4 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    printORSumforEachElement(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to print required sum for
// every valid index i
static void printORSumforEachElement(int arr[], int N)
{
    for (int i = 0; i < N; i++)
    {

        // Store the required sum
        // for current array element
        int req_sum = 0;

        // Generate all possible pairs (arr[i], arr[j])
        for (int j = 0; j < N; j++)
        {

            // Update the value of req_sum
            req_sum += (arr[i] | arr[j]);
        }

        // Print the required sum
        System.out.print(req_sum+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 1, 2, 3, 4 };

    // Size of the array
    int N = arr.length;

    // Function Call
    printORSumforEachElement(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print required sum for
# every valid index i
def printORSumforEachElement(arr, N):

    for i in range(0, N):

        # Store the required sum
        # for current array element
        req_sum = 0

        # Generate all possible pairs(arr[i],arr[j])
        for j in range(0, N):

            # Update the value of req_sum
            req_sum += (arr[i] | arr[j])

        # Print required sum
        print(req_sum, end = " ")

# Driver code

# Given array
arr = [ 1, 2, 3, 4 ]

# Size of array
N = len(arr)

# Function call
printORSumforEachElement(arr, N)

# This code is contributed by Virusbuddah
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

// Function to print required sum for
// every valid index i
static void printORSumforEachElement(int []arr, int N)
{
    for (int i = 0; i < N; i++)
    {

        // Store the required sum
        // for current array element
        int req_sum = 0;

        // Generate all possible pairs (arr[i], arr[j])
        for (int j = 0; j < N; j++)
        {

            // Update the value of req_sum
            req_sum += (arr[i] | arr[j]);
        }

        // Print the required sum
        Console.Write(req_sum+ " ");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 1, 2, 3, 4 };

    // Size of the array
    int N = arr.Length;

    // Function Call
    printORSumforEachElement(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Function to print required sum for
// every valid index i
function prletORSumforEachElement(arr, N)
{
    for(let i = 0; i < N; i++)
    {

        // Store the required sum
        // for current array element
        let req_sum = 0;

        // Generate all possible pairs
        // (arr[i], arr[j])
        for(let j = 0; j < N; j++)
        {

            // Update the value of req_sum
            req_sum += (arr[i] | arr[j]);
        }

        // Print the required sum
        document.write(req_sum + " ");
    }
}

// Driver Code

// Given array
let arr = [ 1, 2, 3, 4 ];

// Size of the array
let N = arr.length;

// Function Call
prletORSumforEachElement(arr, N);

// This code is contributed by avijitmondal1998

</script>
```

**Output:** 

```
12 14 16 22
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**最佳思路是使用[位操作](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/)，假设整数使用**32**T6】位表示。按照以下步骤解决问题:

1.  考虑每第**k**位，使用频率数组 **freq[]** 存储第 k 位为**设置**的元素的**计数**。
2.  对于每个数组元素[，检查该元素的第 k 位是否置位](https://www.geeksforgeeks.org/check-whether-k-th-bit-set-not/)。如果**第 k**位被**置位**，那么只需增加**第 k**位的频率。
3.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素**arr【I】**检查**arr【I】**的**第 k 位**是否置位。
4.  为每个指标 **i** 将所需的**总和**初始化为 **0** 。
5.  如果设置了 **arr[i]** 的第 k 位**，则意味着每一个可能的 **(arr[i] | arr[j])** 的**第 k 位**也将被设置**。所以在这种情况下，将 **(1 < < k) * N** 加到所需的**和**上。****
6.  ****否则，如果未设置 **arr[i]** 的第 **k 位**，则意味着当且仅当 **arr[j]** 的第 **k 位**设置为**时，将设置 **(arr[i] | arr[j])** 的第 **k 位**。因此在这种情况下，将 **(1 < < k) * freq[k]** 添加到所需的和中，该和先前计算为 **freq[k]** 元素数量设置了**第 k 位**。******
7.  **最后，打印索引 **i** 所需的**和**的值。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print required sum for
// every valid index i
void printORSumforEachElement(int arr[], int N)
{
    // Frequency array to store frequency
    // of every k-th bit
    int freq[32];

    // Initialize frequency array
    memset(freq, 0, sizeof freq);

    for (int i = 0; i < N; i++) {
        for (int k = 0; k < 32; k++) {

            // If k-th bit is set, then update
            // the frequency of k-th bit
            if ((arr[i] & (1 << k)) != 0)
                freq[k]++;
        }
    }

    for (int i = 0; i < N; i++) {

        // Stores the required sum
        // for the current array element
        int req_sum = 0;

        for (int k = 0; k < 32; k++) {

            // If k-th bit is set
            if ((arr[i] & (1 << k)) != 0)
                req_sum += (1 << k) * N;

            // If k-th bit is not set
            else
                req_sum += (1 << k) * freq[k];
        }

        // Print the required sum
        cout << req_sum << " ";
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 2, 3, 4 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    printORSumforEachElement(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to print required sum for
// every valid index i
static void printORSumforEachElement(int arr[], int N)
{

    // Frequency array to store frequency
    // of every k-th bit
    int []freq = new int[32];
    for (int i = 0; i < N; i++)
    {
        for (int k = 0; k < 32; k++)
        {

            // If k-th bit is set, then update
            // the frequency of k-th bit
            if ((arr[i] & (1 << k)) != 0)
                freq[k]++;
        }
    }
    for (int i = 0; i < N; i++)
    {

        // Stores the required sum
        // for the current array element
        int req_sum = 0;
        for (int k = 0; k < 32; k++)
        {

            // If k-th bit is set
            if ((arr[i] & (1 << k)) != 0)
                req_sum += (1 << k) * N;

            // If k-th bit is not set
            else
                req_sum += (1 << k) * freq[k];
        }

        // Print the required sum
        System.out.print(req_sum+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 1, 2, 3, 4 };

    // Size of the array
    int N = arr.length;

    // Function Call
    printORSumforEachElement(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to print required sum for
# every valid index i
def printORSumforEachElement(arr, N):

    # Frequency array to store frequency
    # of every k-th bit
    freq = [0 for i in range(32)]

    for i in range(N):
        for k in  range(32):

            # If k-th bit is set, then update
            # the frequency of k-th bit
            if ((arr[i] & (1 << k)) != 0):
                freq[k] += 1

    for i in range(N):

        # Stores the required sum
        # for the current array element
        req_sum = 0

        for k in range(32):

            # If k-th bit is set
            if ((arr[i] & (1 << k)) != 0):
                req_sum += (1 << k) * N

            # If k-th bit is not set
            else:
                req_sum += (1 << k) * freq[k]

        # Print the required sum
        print(req_sum, end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 1, 2, 3, 4 ]

    # Size of the array
    N = len(arr)

    # Function Call
    printORSumforEachElement(arr, N)

# This code is contributed by SURENDRA_GANGWAR
```

## **C#**

```
// C# program for the above approach
using System;
class GFG
{

    // Function to print required sum for
    // every valid index i
    static void printORSumforEachElement(int[] arr, int N)
    {

        // Frequency array to store frequency
        // of every k-th bit
        int[] freq = new int[32];

        for (int i = 0; i < N; i++)
        {
            for (int k = 0; k < 32; k++)
            {

                // If k-th bit is set, then update
                // the frequency of k-th bit
                if ((arr[i] & (1 << k)) != 0)
                    freq[k]++;
            }
        }

        for (int i = 0; i < N; i++)
        {

            // Stores the required sum
            // for the current array element
            int req_sum = 0;
            for (int k = 0; k < 32; k++)
            {

                // If k-th bit is set
                if ((arr[i] & (1 << k)) != 0)
                    req_sum += (1 << k) * N;

                // If k-th bit is not set
                else
                    req_sum += (1 << k) * freq[k];
            }

            // Print the required sum
            Console.Write(req_sum + " ");
        }
    }

    // Driver Code
    public static void Main()
    {
        // Given array
        int[] arr = { 1, 2, 3, 4 };

        // Size of the array
        int N = arr.Length;

        // Function Call
        printORSumforEachElement(arr, N);
    }
}

// This code is contributed by chitranayal.
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to print required sum for
// every valid index i
function printORSumforEachElement(arr, N)
{

    // Frequency array to store frequency
    // of every k-th bit
    var freq = Array(32).fill(0);

    for(var i = 0; i < N; i++)
    {
        for(var k = 0; k < 32; k++)
        {

            // If k-th bit is set, then update
            // the frequency of k-th bit
            if ((arr[i] & (1 << k)) != 0)
                freq[k]++;
        }
    }

    for(var i = 0; i < N; i++)
    {

        // Stores the required sum
        // for the current array element
        var req_sum = 0;

        for(var k = 0; k < 32; k++)
        {

            // If k-th bit is set
            if ((arr[i] & (1 << k)) != 0)
                req_sum += (1 << k) * N;

            // If k-th bit is not set
            else
                req_sum += (1 << k) * freq[k];
        }

        // Print the required sum
        document.write(req_sum + " ");
    }
}

// Driver Code

// Given array
var arr = [ 1, 2, 3, 4 ];

// Size of the array
var N = arr.length;

// Function Call
printORSumforEachElement(arr, N);

// This code is contributed by rutvik_56

</script>
```

****Output:** 

```
12 14 16 22
```** 

*****时间复杂度:** O(32 * N)*
***辅助空间:** O(m)，其中 m = 32***