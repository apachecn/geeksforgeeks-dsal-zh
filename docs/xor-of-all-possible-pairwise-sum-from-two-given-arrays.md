# 两个给定数组中所有可能的成对和的异或运算

> 原文:[https://www . geeksforgeeks . org/两个给定数组的所有可能成对和的异或/](https://www.geeksforgeeks.org/xor-of-all-possible-pairwise-sum-from-two-given-arrays/)

给定两个长度相等的数组 **A[]** 和 **B[]** ，任务是找到给定两个数组成对和的 [**按位异或**](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 。

**示例:**

> **输入:** A[] = {1，2}，B[] = {3，4}
> **输出:** 2
> **解释:**
> 所有可能对的和是{4(1 + 3)、5(1 + 4)、5(2 + 3)、6(2 + 4)}
> 所有对和的异或= 4 ^ 5 ^ 5 ^ 6 = 2
> 
> **输入:** A[] = {4，6，0，0，3，3}，B[] = {0，5，6，5，0，3}
> **输出:** 8

**天真方法:**解决问题最简单的方法是[从两个给定的数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，并计算它们各自的和，然后用对的和更新**异或**。最后，打印得到的异或。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum of
// XOR of the sum of every pair
int XorSum(int A[], int B[], int N)
{

    // Stores the XOR of sums
    // of every pair
    int ans = 0;

    // Iterate to generate all possible pairs
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {

            // Update XOR
            ans = ans ^ (A[i] + B[j]);
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{

    int A[] = { 4, 6, 0, 0, 3, 3 };

    int B[] = { 0, 5, 6, 5, 0, 3 };
    int N = sizeof A / sizeof A[0];

    cout << XorSum(A, B, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to calculate the sum of
// XOR of the sum of every pair
static int XorSum(int A[], int B[], int N)
{

    // Stores the XOR of sums
    // of every pair
    int ans = 0;

    // Iterate to generate all possible pairs
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // Update XOR
            ans = ans ^ (A[i] + B[j]);
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void main (String[] args)
{
    int A[] = { 4, 6, 0, 0, 3, 3 };
    int B[] = { 0, 5, 6, 5, 0, 3 };

    int N = A.length;

    System.out.println(XorSum(A, B, N));
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate the sum of
# XOR of the sum of every pair
def XorSum(A, B, N):

    # Stores the XOR of sums
    # of every pair
    ans = 0

    # Iterate to generate all
    # possible pairs
    for i in range(N):
        for j in range(N):

            # Update XOR
            ans = ans ^ (A[i] + B[j])

    # Return the answer
    return ans

# Driver Code
if __name__ == "__main__":

    A = [ 4, 6, 0, 0, 3, 3 ]
    B = [ 0, 5, 6, 5, 0, 3 ]
    N = len(A)

    print (XorSum(A, B, N))

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to calculate the sum of
// XOR of the sum of every pair
static int XorSum(int []A, int []B, int N)
{   
    // Stores the XOR of sums
    // of every pair
    int ans = 0;

    // Iterate to generate all possible pairs
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < N; j++)
        {           
            // Update XOR
            ans = ans ^ (A[i] + B[j]);
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int []A = {4, 6, 0, 0, 3, 3};
    int []B = {0, 5, 6, 5, 0, 3};
    int N = A.Length;   
    Console.WriteLine(XorSum(A, B, N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

    // Function to calculate the sum of
    // XOR of the sum of every pair
    function XorSum(A , B , N) {

        // Stores the XOR of sums
        // of every pair
        var ans = 0;

        // Iterate to generate all possible pairs
        for (i = 0; i < N; i++) {
            for (j = 0; j < N; j++) {

                // Update XOR
                ans = ans ^ (A[i] + B[j]);
            }
        }

        // Return the answer
        return ans;
    }

    // Driver Code

        var A = [ 4, 6, 0, 0, 3, 3 ];
        var B = [ 0, 5, 6, 5, 0, 3 ];

        var N = A.length;

        document.write(XorSum(A, B, N));

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以使用[位操作](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/)技术进行优化。按照以下步骤解决问题:

*   仅考虑第 **K <sup>个</sup>位**，任务是统计对( **i，j** )的数量，使得(A <sub>i</sub> + B <sub>j</sub> )的第 **K <sup>个</sup>位**被设置为**。**
*   **如果这个数字是奇数，在答案中加上 **X = 2 <sup>k</sup>** 。我们只对模 **2X** 中的(a <sub>i</sub> ，b <sub>j</sub> 的值感兴趣。**
*   **因此，将 a <sub>i</sub> 替换为 **a <sub>i</sub> % (2X)** 并将 b <sub>j</sub> 替换为 **b <sub>j</sub> % (2X)** ，并假设 **a <sub>i</sub>** 和 **b <sub>j</sub> < 2X** 。**
*   **设置(a <sub>i</sub> + b <sub>j)</sub> 的 k <sup>第</sup>位时有两种情况:

    *   x ≤ ai + bj < 2x
    *   3x ≤ ai + bj < 4x** 
*   **因此，**按照递增的顺序对** b[]进行排序。对于一个固定的 I，满足**X≤(a<sub>I</sub>+b<sub>j</sub>)<2X**的 j 的集合形成一个区间。**
*   **因此，通过[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来计算这样的 j 的数量。同样，处理第二种情况。**

**下面是上述方法的实现:**

## **C++**

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the
// XOR of the sum of every pair
int XorSum(int A[], int B[], int N)
{

    // Stores the maximum bit
    const int maxBit = 29;

    int ans = 0;

    // Look for all the k-th bit
    for (int k = 0; k < maxBit; k++) {

        // Stores the modulo of
        // elements B[] with (2^(k+1))
        int C[N];

        for (int i = 0; i < N; i++) {

            // Calculate modulo of
            // array B[] with (2^(k+1))
            C[i] = B[i] % (1 << (k + 1));
        }

        // Sort the array C[]
        sort(C, C + N);

        // Stores the total number
        // whose k-th bit is set
        long long count = 0;
        long long l, r;

        for (int i = 0; i < N; i++) {

            // Calculate and store the modulo
            // of array A[] with (2^(k+1))
            int x = A[i] % (1 << (k + 1));

            // Lower bound to count the number
            // of elements having k-th bit in
            // the range (2^k - x, 2* 2^(k) - x)
            l = lower_bound(C,
                            C + N,
                            (1 << k) - x)
                - C;

            r = lower_bound(C,
                            C + N,
                            (1 << k) * 2 - x)
                - C;

            // Add total number i.e (r - l)
            // whose k-th bit is one
            count += (r - l);

            // Lower bound to count the number
            // of elements having k-th bit in
            // range (3 * 2^k - x, 4*2^(k) - x)
            l = lower_bound(C,
                            C + N,
                            (1 << k) * 3 - x)
                - C;
            r = lower_bound(C,
                            C + N,
                            (1 << k) * 4 - x)
                - C;

            count += (r - l);
        }

        // If count is even, Xor of
        // k-th bit becomes zero, no
        // need to add to the answer.
        // If count is odd, only then,
        // add to the final answer
        if (count & 1)
            ans += (1 << k);
    }

    // Return answer
    return ans;
}

// Driver code
int main()
{
    int A[] = { 4, 6, 0, 0, 3, 3 };
    int B[] = { 0, 5, 6, 5, 0, 3 };
    int N = sizeof A / sizeof A[0];

    // Function call
    cout << XorSum(A, B, N) << endl;

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Lower bound
static int lower_bound(int[] a, int low,
                       int high, int element)
{
    while(low < high)
    {
        int middle = low + (high - low) / 2;
        if(element > a[middle])
            low = middle + 1;
        else
            high = middle;
    }
    return low;
}

// Function to calculate the
// XOR of the sum of every pair
static int XorSum(int A[],
                  int B[], int N)
{
    // Stores the maximum bit
    final int maxBit = 29;

    int ans = 0;

    // Look for all the k-th bit
    for (int k = 0; k < maxBit; k++)
    {
        // Stores the modulo of
        // elements B[] with (2^(k+1))
        int []C = new int[N];

    for (int i = 0; i < N; i++)
    {
        // Calculate modulo of
        // array B[] with (2^(k+1))
        C[i] = B[i] % (1 << (k + 1));
    }

    // Sort the array C[]
    Arrays.sort(C);

    // Stores the total number
    // whose k-th bit is set
    long count = 0;
    long l, r;

    for (int i = 0; i < N; i++)
    {
        // Calculate and store the modulo
        // of array A[] with (2^(k+1))
        int x = A[i] % (1 << (k + 1));

        // Lower bound to count
        // the number of elements
        // having k-th bit in
        // the range (2^k - x,
        // 2* 2^(k) - x)
        l = lower_bound(C, 0, N,
                       (1 << k) - x);

        r = lower_bound(C, 0, N,
                       (1 << k) *
                        2 - x);

        // Add total number i.e
        // (r - l) whose k-th bit is one
        count += (r - l);

        // Lower bound to count
        // the number of elements
        // having k-th bit in
        // range (3 * 2^k - x,
        // 4*2^(k) - x)
        l = lower_bound(C, 0, N,
                       (1 << k) *
                        3 - x);
        r = lower_bound(C, 0, N,
                       (1 << k) *
                        4 - x);

        count += (r - l);
    }

    // If count is even, Xor of
    // k-th bit becomes zero, no
    // need to add to the answer.
    // If count is odd, only then,
    // add to the final answer
    if ((count & 1) != 0)
        ans += (1 << k);
}

// Return answer
return ans;
}

// Driver code
public static void main(String[] args)
{
    int A[] = {4, 6, 0, 0, 3, 3};
    int B[] = {0, 5, 6, 5, 0, 3};
    int N = A.length;

    // Function call
    System.out.print(XorSum(A, B,
                            N) + "\n");
}
}

// This code is contributed by gauravrajput1
```

## **蟒蛇 3**

```
# Python3 program to implement
# the above approach
from bisect import bisect, bisect_left, bisect_right

# Function to calculate the
# XOR of the sum of every pair
def XorSum(A, B, N):

    # Stores the maximum bit
    maxBit = 29

    ans = 0

    # Look for all the k-th bit
    for k in range(maxBit):

        # Stores the modulo of
        # elements B[] with (2^(k+1))
        C = [0] * N

        for i in range(N):

            # Calculate modulo of
            # array B[] with (2^(k+1))
            C[i] = B[i] % (1 << (k + 1))

        # Sort the array C[]
        C = sorted(C)

        # Stores the total number
        # whose k-th bit is set
        count = 0
        l, r = 0, 0

        for i in range(N):

            # Calculate and store the modulo
            # of array A[] with (2^(k+1))
            x = A[i] % (1 << (k + 1))

            # Lower bound to count the number
            # of elements having k-th bit in
            # the range (2^k - x, 2* 2^(k) - x)
            l = bisect_left(C, (1 << k) - x)

            r = bisect_left(C, (1 << k) * 2 - x)

            # Add total number i.e (r - l)
            # whose k-th bit is one
            count += (r - l)

            # Lower bound to count the number
            # of elements having k-th bit in
            # range (3 * 2^k - x, 4*2^(k) - x)
            l = bisect_left(C, (1 << k) * 3 - x)
            r = bisect_left(C, (1 << k) * 4 - x)

            count += (r - l)

        # If count is even, Xor of
        # k-th bit becomes zero, no
        # need to add to the answer.
        # If count is odd, only then,
        # add to the final answer
        if (count & 1):
            ans += (1 << k)

    # Return answer
    return ans

# Driver code
if __name__ == '__main__':

    A = [ 4, 6, 0, 0, 3, 3 ]
    B = [ 0, 5, 6, 5, 0, 3 ]
    N = len(A)

    # Function call
    print(XorSum(A, B, N))

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program to implement
// the above approach
using System;

class GFG{

// Lower bound
static int lower_bound(int[] a, int low,
                       int high, int element)
{
    while (low < high)
    {
        int middle = low + (high - low) / 2;
        if (element > a[middle])
            low = middle + 1;
        else
            high = middle;
    }
    return low;
}

// Function to calculate the
// XOR of the sum of every pair
static int XorSum(int[] A, int[] B, int N)
{

    // Stores the maximum bit
    int maxBit = 29;

    int ans = 0;

    // Look for all the k-th bit
    for(int k = 0; k < maxBit; k++)
    {

        // Stores the modulo of
        // elements B[] with (2^(k+1))
        int[] C = new int[N];

        for(int i = 0; i < N; i++)
        {

            // Calculate modulo of
            // array B[] with (2^(k+1))
            C[i] = B[i] % (1 << (k + 1));
        }

        // Sort the array C[]
        Array.Sort(C);

        // Stores the total number
        // whose k-th bit is set
        long count = 0;
        long l, r;

        for(int i = 0; i < N; i++)
        {

            // Calculate and store the modulo
            // of array A[] with (2^(k+1))
            int x = A[i] % (1 << (k + 1));

            // Lower bound to count
            // the number of elements
            // having k-th bit in
            // the range (2^k - x,
            // 2* 2^(k) - x)
            l = lower_bound(C, 0, N,
                            (1 << k) - x);

            r = lower_bound(C, 0, N,
                            (1 << k) * 2 - x);

            // Add total number i.e
            // (r - l) whose k-th bit is one
            count += (r - l);

            // Lower bound to count
            // the number of elements
            // having k-th bit in
            // range (3 * 2^k - x,
            // 4*2^(k) - x)
            l = lower_bound(C, 0, N,
                            (1 << k) * 3 - x);
            r = lower_bound(C, 0, N,
                            (1 << k) * 4 - x);

            count += (r - l);
        }

        // If count is even, Xor of
        // k-th bit becomes zero, no
        // need to add to the answer.
        // If count is odd, only then,
        // add to the final answer
        if ((count & 1) != 0)
            ans += (1 << k);
    }

    // Return answer
    return ans;
}

// Driver code
public static void Main(string[] args)
{
    int[] A = { 4, 6, 0, 0, 3, 3 };
    int[] B = { 0, 5, 6, 5, 0, 3 };
    int N = A.Length;

    // Function call
    Console.Write(XorSum(A, B, N) + "\n");
}
}

// This code is contributed by grand_master
```

## **java 描述语言**

```
<script>
// Javascript Program to implement
// the above approach

// Lower bound
function lower_bound(a,low,high,element)
{
    while(low < high)
    {
        let middle = low + Math.floor((high - low) / 2);
        if(element > a[middle])
            low = middle + 1;
        else
            high = middle;
    }
    return low;
}

// Function to calculate the
// XOR of the sum of every pair
function XorSum(A,B,N)
{
    // Stores the maximum bit
    let maxBit = 29;

    let ans = 0;

    // Look for all the k-th bit
    for (let k = 0; k < maxBit; k++)
    {
        // Stores the modulo of
        // elements B[] with (2^(k+1))
        let C = new Array(N);

    for (let i = 0; i < N; i++)
    {
        // Calculate modulo of
        // array B[] with (2^(k+1))
        C[i] = B[i] % (1 << (k + 1));
    }

    // Sort the array C[]
    C.sort(function(x,y){return x-y;});

    // Stores the total number
    // whose k-th bit is set
    let count = 0;
    let l, r;

    for (let i = 0; i < N; i++)
    {
        // Calculate and store the modulo
        // of array A[] with (2^(k+1))
        let x = A[i] % (1 << (k + 1));

        // Lower bound to count
        // the number of elements
        // having k-th bit in
        // the range (2^k - x,
        // 2* 2^(k) - x)
        l = lower_bound(C, 0, N,
                       (1 << k) - x);

        r = lower_bound(C, 0, N,
                       (1 << k) *
                        2 - x);

        // Add total number i.e
        // (r - l) whose k-th bit is one
        count += (r - l);

        // Lower bound to count
        // the number of elements
        // having k-th bit in
        // range (3 * 2^k - x,
        // 4*2^(k) - x)
        l = lower_bound(C, 0, N,
                       (1 << k) *
                        3 - x);
        r = lower_bound(C, 0, N,
                       (1 << k) *
                        4 - x);

        count += (r - l);
    }

    // If count is even, Xor of
    // k-th bit becomes zero, no
    // need to add to the answer.
    // If count is odd, only then,
    // add to the final answer
    if ((count & 1) != 0)
        ans += (1 << k);
}

// Return answer
return ans;
}

// Driver code
let A=[4, 6, 0, 0, 3, 3];
let B=[0, 5, 6, 5, 0, 3];
let N = A.length;
// Function call
    document.write(XorSum(A, B,
                            N) + "\n");

// This code is contributed by avanitrachhadiya2155
</script>
```

****Output:** 

```
8
```** 

*****时间复杂度:** O(NlogN)*
***辅助空间:** O(N)***