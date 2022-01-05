# 求最大子集的长度，使所有元素成对互素

> 原文:[https://www . geesforgeks . org/find-最大子集的长度-这样所有元素都成对互素/](https://www.geeksforgeeks.org/find-the-length-of-the-largest-subset-such-that-all-elements-are-pairwise-coprime/)

给定一个大小为 N 的**数组 A** ，我们的任务是找到最大子集的**长度，这样子集中的所有元素都是**成对互素**也就是说，对于 x 和 y 不相同的任意两个元素 x 和 y， **gcd(x，y)等于 1** 。
***注:**所有阵元均为< = 50。***

**示例:**

> **输入:**A =【2，5，2，5，2】
> **输出:** 2
> **说明:**
> 满足条件的最大子集为:{2，5}
> 
> **输入:**A =【2，3，13，5，14，6，7，11】
> **输出:** 6

**天真方法:**
为了解决上面提到的问题，我们必须生成所有子集，并针对每个子集检查给定的条件是否成立。但是这个方法需要 *O(N <sup>2</sup> * 2 <sup>N</sup> )* 的时间，可以进一步优化。

下面是上述方法的实现:

## C++

```
// C++ implementation to Find the length of the Largest
// subset such that all elements are Pairwise Coprime
#include <bits/stdc++.h>
using namespace std;

// Function to find the largest subset possible
int largestSubset(int a[], int n)
{
    int answer = 0;

    // Iterate through all the subsets
    for (int i = 1; i < (1 << n); i++) {
        vector<int> subset;

        /* Check if jth bit in the counter is set */
        for (int j = 0; j < n; j++) {
            if (i & (1 << j))
                subset.push_back(a[j]);
        }

        bool flag = true;

        for (int j = 0; j < subset.size(); j++) {
            for (int k = j + 1; k < subset.size(); k++) {
                // Check if the gcd is not equal to 1
                if (__gcd(subset[j], subset[k]) != 1)
                    flag = false;
            }
        }

        if (flag == true)
            // Update the answer with maximum value
            answer = max(answer, (int)subset.size());
    }

    // Return the final result
    return answer;
}

// Driver code
int main()
{

    int A[] = { 2, 3, 13, 5, 14, 6, 7, 11 };

    int N = sizeof(A) / sizeof(A[0]);

    cout << largestSubset(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the length
// of the largest subset such that all
// elements are Pairwise Coprime
import java.util.*;

class GFG{

static int gcd(int a, int b)
{

    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);

    return gcd(a, b - a);
}

// Function to find the largest subset possible
static int largestSubset(int a[], int n)
{
    int answer = 0;

    // Iterate through all the subsets
    for(int i = 1; i < (1 << n); i++)
    {
        Vector<Integer> subset = new Vector<Integer>();

        // Check if jth bit in the counter is set
        for(int j = 0; j < n; j++)
        {
            if ((i & (1 << j)) != 0)
                subset.add(a[j]);
        }

        boolean flag = true;

        for(int j = 0; j < subset.size(); j++)
        {
            for(int k = j + 1; k < subset.size(); k++)
            {

                // Check if the gcd is not equal to 1
                if (gcd((int)subset.get(j),
                       (int) subset.get(k)) != 1)
                    flag = false;
            }
        }

        if (flag == true)

            // Update the answer with maximum value
            answer = Math.max(answer,
                             (int)subset.size());
    }

    // Return the final result
    return answer;
}

// Driver code
public static void main(String args[])
{
    int A[] = { 2, 3, 13, 5, 14, 6, 7, 11 };

    int N = A.length;

    System.out.println(largestSubset(A, N));
}
}

// This code is contributed by Stream_Cipher
```

## 蟒蛇 3

```
# Python3 implementation to Find
# the length of the Largest subset
# such that all elements are Pairwise Coprime
import math

# Function to find the largest subset possible
def largestSubset(a, n):
    answer = 0

    # Iterate through all the subsets
    for i in range(1, (1 << n)):
        subset = []

        # Check if jth bit in the counter is set
        for j in range(0, n):
            if (i & (1 << j)):
                subset.insert(j, a[j])

        flag = True

        for j in range(0, len(subset)):
            for k in range(j + 1, len(subset)):

                # Check if the gcd is not equal to 1
                if (math.gcd(subset[j], subset[k]) != 1) :
                    flag = False

        if (flag == True):

            # Update the answer with maximum value
            answer = max(answer, len(subset))

    # Return the final result
    return answer

# Driver code
A = [ 2, 3, 13, 5, 14, 6, 7, 11 ]
N = len(A)
print(largestSubset(A, N))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# implementation to Find the length
// of the largest subset such that all
// elements are Pairwise Coprime
using System;
using System.Collections.Generic;

class GFG{

static int gcd(int a, int b)
{

    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);

    return gcd(a, b - a);
}

// Function to find the largest subset possible
static int largestSubset(int []a, int n)
{
    int answer = 0;

    // Iterate through all the subsets
    for(int i = 1; i < (1 << n); i++)
    {
        List<int> subset = new List<int>();

        // Check if jth bit in the counter is set
        for(int j = 0; j < n; j++)
        {
            if ((i & (1 << j)) != 0)
                subset.Add(a[j]);
        }

        int flag = 1;

        for(int j = 0; j < subset.Count; j++)
        {
            for(int k = j + 1; k < subset.Count; k++)
            {
                // Check if the gcd is not equal to 1
                if (gcd((int)subset[j],
                       (int) subset[k]) != 1)
                    flag = 0;
            }
        }

        if (flag == 1)

            // Update the answer with maximum value
            answer = Math.Max(answer,
                             (int)subset.Count);
    }

    // Return the final result
    return answer;
}

// Driver code
public static void Main()
{
    int []A = { 2, 3, 13, 5, 14, 6, 7, 11 };

    int N = A.Length;

    Console.WriteLine(largestSubset(A, N));
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>
    // Javascript implementation to Find the length
    // of the largest subset such that all
    // elements are Pairwise Coprime

    function gcd(a, b)
    {

        // Everything divides 0
        if (a == 0)
            return b;
        if (b == 0)
            return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return gcd(a - b, b);

        return gcd(a, b - a);
    }

    // Function to find the largest subset possible
    function largestSubset(a, n)
    {
        let answer = 0;

        // Iterate through all the subsets
        for(let i = 1; i < (1 << n); i++)
        {
            let subset = [];

            // Check if jth bit in the counter is set
            for(let j = 0; j < n; j++)
            {
                if ((i & (1 << j)) != 0)
                    subset.push(a[j]);
            }

            let flag = 1;

            for(let j = 0; j < subset.length; j++)
            {
                for(let k = j + 1; k < subset.length; k++)
                {
                    // Check if the gcd is not equal to 1
                    if (gcd(subset[j], subset[k]) != 1)
                        flag = 0;
                }
            }

            if (flag == 1)

                // Update the answer with maximum value
                answer = Math.max(answer, subset.length);
        }

        // Return the final result
        return answer;
    }

    let A = [ 2, 3, 13, 5, 14, 6, 7, 11 ];

    let N = A.length;

    document.write(largestSubset(A, N));

</script>
```

**Output:** 

```
6
```

**高效方法:**
上述方法可以优化，方法取决于前 50 个自然数中只有 15 个素数。所以数组中的所有数字都只有这 15 个数字中的质因数。我们将使用[位屏蔽和动态编程](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)来优化问题。

*   因为只有 15 个素数，所以考虑每个数的 **15 位表示**，其中如果素数的索引是该数的因子，则每个位为 1。我们将通过 0 索引来索引质数，这意味着 2 在索引 1 的第 0 个位置 3，以此类推。
*   整数变量“**”掩码**”表示子集中已经出现的质因数。如果在掩码中设置了第 I 位，则第 I 个质因数已经出现，否则不会出现。
*   在**递归关系**的每一步，元素可以包含在子集内，也可以不包含。如果元素不包含在子数组中，那么只需移动到下一个索引。如果包含，通过将掩码中对应于当前元素质因数的所有位设置为开来更改掩码。只有当前元素的所有主要因素以前都没有出现过，它才能被包括在内。
*   只有当掩码中对应于当前元素数字的位为“关”时，此条件才会得到满足。

如果我们画出完整的递归树，我们可以观察到许多子问题正在被解决，这些问题一次又一次地发生。所以我们使用一个表 dp[][]，这样对于每个索引 dp[i][j]，I 是数组中元素的位置，j 是掩码。

下面是上述方法的实现:

## C++

```
// C++ implementation to Find the length of the Largest
// subset such that all elements are Pairwise Coprime
#include <bits/stdc++.h>
using namespace std;

// Dynamic programming table
int dp[5000][(1 << 10) + 5];

// Function to obtain the mask for any integer
int getmask(int val)
{
    int mask = 0;

    // List of prime numbers till 50
    int prime[15] = { 2, 3, 5, 7, 11, 13, 17, 19,
                      23, 29, 31, 37, 41, 43, 47 };

    // Iterate through all prime numbers to obtain the mask
    for (int i = 0; i < 15; i++) {
        if (val % prime[i] == 0) {
            // Set this prime's bit ON in the mask
            mask = mask | (1 << i);
        }
    }

    // Return the mask value
    return mask;
}

// Function to count the number of ways
int calculate(int pos, int mask,
              int a[], int n)
{
    if (pos == n || mask == (1 << n - 1))
        return 0;

    // Check if subproblem has been solved
    if (dp[pos][mask] != -1)
        return dp[pos][mask];

    int size = 0;

    // Excluding current element in the subset
    size = max(size, calculate(pos + 1, mask, a, n));

    // Check if there are no common prime factors
    // then only this element can be included
    if ((getmask(a[pos]) & mask) == 0) {

        // Calculate the new mask if this element is included
        int new_mask = (mask | (getmask(a[pos])));

        size = max(size, 1 + calculate(pos + 1, new_mask, a, n));
    }

    // Store and return the answer
    return dp[pos][mask] = size;
}

// Function to find the count of
// subarray with all digits unique
int largestSubset(int a[], int n)
{
    // Initializing dp
    memset(dp, -1, sizeof(dp));

    return calculate(0, 0, a, n);
}

// Driver code
int main()
{

    int A[] = { 2, 3, 13, 5, 14, 6, 7, 11 };

    int N = sizeof(A) / sizeof(A[0]);

    cout << largestSubset(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the length
// of the largest subset such that all
// elements are Pairwise Coprime
import java.util.*;

class GFG{

// Dynamic programming table
static int dp[][] = new int [5000][1029];

// Function to obtain the mask for any integer
static int getmask(int val)
{
    int mask = 0;

    // List of prime numbers till 50
    int prime[] = { 2, 3, 5, 7, 11, 13, 17, 19,
                    23, 29, 31, 37, 41, 43, 47 };

    // Iterate through all prime numbers
    // to obtain the mask
    for(int i = 0; i < 15; i++)
    {
        if (val % prime[i] == 0)
        {

            // Set this prime's bit ON in the mask
            mask = mask | (1 << i);
        }
    }

    // Return the mask value
    return mask;
}

// Function to count the number of ways
static int calculate(int pos, int mask,
                     int a[], int n)
{
    if (pos == n ||
       mask == (int)(1 << n - 1))
        return 0;

    // Check if subproblem has been solved
    if (dp[pos][mask] != -1)
        return dp[pos][mask];

    int size = 0;

    // Excluding current element in the subset
    size = Math.max(size, calculate(pos + 1,
                                    mask, a, n));

    // Check if there are no common prime factors
    // then only this element can be included
    if ((getmask(a[pos]) & mask) == 0)
    {

        // Calculate the new mask if this
        // element is included
        int new_mask = (mask | (getmask(a[pos])));

        size = Math.max(size, 1 + calculate(pos + 1,
                                            new_mask,
                                            a, n));
    }

    // Store and return the answer
    return dp[pos][mask] = size;
}

// Function to find the count of
// subarray with all digits unique
static int largestSubset(int a[], int n)
{
    for(int i = 0; i < 5000; i++)
        Arrays.fill(dp[i], -1);

    return calculate(0, 0, a, n);
}

// Driver code
public static void main(String args[])
{
    int A[] = { 2, 3, 13, 5, 14, 6, 7, 11 };

    int N = A.length;

    System.out.println(largestSubset(A, N));
}
}

// This code is contributed by Stream_Cipher
```

## 计算机编程语言

```
# Python implementation to find the
# length of the Largest subset such
# that all elements are Pairwise Coprime

# Dynamic programming table
dp = [[-1] * ((1 << 10) + 5)] * 5000

# Function to obtain the mask for any integer
def getmask(val):

    mask = 0

    # List of prime numbers till 50
    prime = [ 2, 3, 5, 7, 11, 13, 17, 19,
              23, 29, 31, 37, 41, 43, 47 ]

    # Iterate through all prime numbers
    # to obtain the mask
    for i in range(1, 15):
        if val % prime[i] == 0:

            # Set this prime's bit ON in the mask
            mask = mask | (1 << i)

    # Return the mask value
    return mask

# Function to count the number of ways
def calculate(pos, mask, a, n):

    if ((pos == n) or (mask == (1 << n - 1))):
        return 0

    # Check if subproblem has been solved
    if dp[pos][mask] != -1:
        return dp[pos][mask]

    size = 0

    # Excluding current element in the subset
    size = max(size, calculate(pos + 1,
                               mask, a, n))

    # Check if there are no common prime factors
    # then only this element can be included
    if (getmask(a[pos]) & mask) == 0:

        # Calculate the new mask if this
        # element is included
        new_mask = (mask | (getmask(a[pos])))
        size = max(size, 1 + calculate(pos + 1,
                                       new_mask,
                                       a, n))
    # Store and return the answer
    dp[pos][mask] = size
    return dp[pos][mask]

# Function to find the count of
# subarray with all digits unique    
def largestSubset(A, n):

    return calculate(0, 0, A, n);

# Driver code
A = [ 2, 3, 13, 5, 14, 6, 7, 11 ]
N = len(A)

print(largestSubset(A, N))

# This code is contributed by Stream_Cipher
```

## C#

```
// C# implementation to find the length
// of the largest subset such that all
// elements are Pairwise Coprime
using System;

class GFG{

// Dynamic programming table
static int [,] dp = new int [5000, 1029];

// Function to obtain the mask for any integer
static int getmask(int val)
{
    int mask = 0;

    // List of prime numbers till 50
    int []prime = { 2, 3, 5, 7, 11, 13, 17, 19,
                    23, 29, 31, 37, 41, 43, 47 };

    // Iterate through all prime
    // numbers to obtain the mask
    for(int i = 0; i < 15; i++)
    {
        if (val % prime[i] == 0)
        {

            // Set this prime's bit ON in the mask
            mask = mask | (1 << i);
        }
    }

    // Return the mask value
    return mask;
}

// Function to count the number of ways
static int calculate(int pos, int mask,
                     int []a, int n)
{
    if (pos == n ||
       mask == (int)(1 << n - 1))
        return 0;

    // Check if subproblem has been solved
    if (dp[pos, mask] != -1)
        return dp[pos, mask];

    int size = 0;

    // Excluding current element in the subset
    size = Math.Max(size, calculate(pos + 1,
                                    mask, a, n));

    // Check if there are no common prime factors
    // then only this element can be included
    if ((getmask(a[pos]) & mask) == 0)
    {

        // Calculate the new mask if
        // this element is included
        int new_mask = (mask | (getmask(a[pos])));

        size = Math.Max(size, 1 + calculate(pos + 1,
                                            new_mask,
                                            a, n));
    }

    // Store and return the answer
    return dp[pos, mask] = size;
}

// Function to find the count of
// subarray with all digits unique
static int largestSubset(int []a, int n)
{
    for(int i = 0; i < 5000; i++)
    {
        for(int j = 0; j < 1029; j++)
            dp[i, j] = -1;
    }
    return calculate(0, 0, a, n);
}

// Driver code
public static void Main()
{
    int []A = { 2, 3, 13, 5, 14, 6, 7, 11 };

    int N = A.Length;

    Console.WriteLine(largestSubset(A, N));
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>

// JavaScript implementation to
// Find the length of the Largest
// subset such that all elements
// are Pairwise Coprime

// Dynamic programming table
var dp = Array.from(Array(5000), ()=>Array((1 << 10) + 5));

// Function to obtain the mask for any integer
function getmask( val)
{
    var mask = 0;

    // List of prime numbers till 50
    var prime = [2, 3, 5, 7, 11, 13, 17, 19,
                      23, 29, 31, 37, 41, 43, 47];

    // Iterate through all prime numbers to obtain the mask
    for (var i = 0; i < 15; i++) {
        if (val % prime[i] == 0) {
            // Set this prime's bit ON in the mask
            mask = mask | (1 << i);
        }
    }

    // Return the mask value
    return mask;
}

// Function to count the number of ways
function calculate(pos, mask, a, n)
{
    if (pos == n || mask == (1 << n - 1))
        return 0;

    // Check if subproblem has been solved
    if (dp[pos][mask] != -1)
        return dp[pos][mask];

    var size = 0;

    // Excluding current element in the subset
    size = Math.max(size, calculate(pos + 1, mask, a, n));

    // Check if there are no common prime factors
    // then only this element can be included
    if ((getmask(a[pos]) & mask) == 0) {

        // Calculate the new mask if this element is included
        var new_mask = (mask | (getmask(a[pos])));

        size = Math.max(size,
        1 + calculate(pos + 1, new_mask, a, n));
    }

    // Store and return the answer
    return dp[pos][mask] = size;
}

// Function to find the count of
// subarray with all digits unique
function largestSubset(a, n)
{
    // Initializing dp
    dp = Array.from(Array(5000),
    ()=>Array((1 << 10) + 5).fill(-1));

    return calculate(0, 0, a, n);
}

// Driver code
var A = [2, 3, 13, 5, 14, 6, 7, 11 ];
var N = A.length;
document.write( largestSubset(A, N));

</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(N * 15 * 2 <sup>15</sup> )