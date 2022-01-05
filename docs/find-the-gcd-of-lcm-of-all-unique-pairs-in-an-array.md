# 求数组中所有唯一对的 LCM 的 GCD

> 原文:[https://www . geeksforgeeks . org/find-the-gcd-of-LCM-of-all-unique-in-a-array 对/](https://www.geeksforgeeks.org/find-the-gcd-of-lcm-of-all-unique-pairs-in-an-array/)

给定一个大小为 **N** 的整数数组 **arr[]** ，任务是找到数组中所有唯一对 **(i，j)** 的 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) ，使得 **i < j** 。
**示例:**

> **输入:** arr[] = {10，24，40，80}
> **输出:** 40
> **解释:**
> 所有唯一对的 LCM 以下给定条件为:
> LCM(10，24) = 120
> LCM(10，40) = 40
> LCM(10，80) = 80
> LCM(24，40) = 120
> 
> **输入:** arr[] = {1，1 }
> T3】输出: 1

**天真方法:**最简单的方法是找出数组中所有唯一的对。然后找到他们的 LCM。然后找到所有 LCM 的 GCD。

**高效方法:**上述幼稚方法可以借助[后缀数组](https://www.geeksforgeeks.org/suffix-array-set-1-introduction/)进行优化。我们可以使用后缀数组来高效地找到与其他元素配对的每个元素的 LCM。然后我们可以简单地找到并返回这个 LCM 数组的 GCD。

*   对于每个元素 A[i]，我们需要计算 **LCM(a[i]，a[j])** ，其中 j 属于[i+1，N-1]。
*   起始元素为 A[i]的所有对的 LCM 可以写成

> LCM(A[i]，GCD(I+1 到 n-1 范围内的所有 j))

*   为此，我们构建了一个[后缀数组](https://www.geeksforgeeks.org/suffix-array-set-1-introduction/)。假设**后缀[]** 存储属于范围**【I+1，N-1】**的元素的 gcd。
*   然后创建一个 LCM 数组来存储 A[i]的 LCM 和其后所有元素的 GCD，即

> LCM[i] = LCM(A[i]，后缀[i+1])
> 其中后缀[i+1]存储元素[i+1，n-1]
> 的 GCD

*   最后计算 LCM 阵列中所有元素的 GCD。

## C++

```
// C++ code to find the GCD of LCM
// of all unique pairs in an Array
#include <bits/stdc++.h>
using namespace std;

// Find lcm of element x and y
int LCM(int x, int y)
{
    return x * y / __gcd(x, y);
}

// Function that finds gcd of lcm
// of all pairs of elements.
void gcd_of_lcm(int n, int arr[])
{

    // n is the size of the array.
    // arr is the array.

    // Suffix array that stores
    // the gcd of the array elements.
    int suff[n];

    // Initialize suffix array.
    for(int x = 0; x < n; x++)
    {
       suff[x] = 1;
    }

    // Loop that make the suffix gcd array
    suff[n - 1] = arr[n - 1];
    for(int i = n - 2; i >= 0; i--)
    {
       suff[i] = __gcd(arr[i], suff[i + 1]);
    }

    // lcm array that store the lcm
    // of ith elements for all j
    // that satisfy given condition.
    vector<int> lcm;
    for(int i = 0; i < n - 1; i++)
    {

       // we find lcm[i] for lcm
       // of ith elements for all j
       // using bellow formula.
       int y = LCM(arr[i], suff[i + 1]);

       // Add lcm of ith elements
       // for all j in lcm array.
       lcm.push_back(y);
    }

    // Now we find gcd of all ith elements.
    // where i = 0, 1, 2, 3.....n-2.
    int ans = lcm[0];

    for(int i = 1; i < n - 1; i++)
    {
       ans = __gcd(ans, lcm[i]);
    }
    cout << ans << endl;
}

// Driver code
int main()
{
    int n = 4;
    int a[] = { 10, 24, 40, 80 };

    // Function call for input 1
    gcd_of_lcm(n, a);

    n = 10;
    int b[] = { 540, 648, 810, 648, 720,
                540, 594, 864, 972, 648 };

    // Function call for input 2
    gcd_of_lcm(n, b);
}

// This code is contributed by shobhitgupta907
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the GCD of LCM
// of all unique pairs in an array
class GFG{

// Function to evaluate GCD of x and y
static int gcd(int x, int y)
{
    if (y == 0)
        return x;
    else
        return gcd(y, x % y);
}

// Function that finds gcd of lcm
// of all pairs of elements.
static void gcd_of_lcm(int n, int arr[])
{

    // n = size of array i.e. arr[]

    // Suffix array that stores
    // the GCD of the array elements.
    int suff[] = new int[n];

    // Initialise the suffix array
    for(int i = 0; i < n; i++)
        suff[i] = 1;

    // Loop that make suffix GCD array
    suff[n - 1] = arr[n - 1];

    for(int i = n - 2; i >= 0; i--)
        suff[i] = gcd(arr[i], suff[i + 1]);

    // lcm array that store lcm for pairwise
    // consecutive elements
    int lcm[] = new int[n - 1];
    for(int i = 0; i < n - 1; i++)

        // Find LCM using standard known formula
        lcm[i] = (arr[i] * suff[i + 1]) /
               gcd(arr[i], suff[i + 1]);

    // Now we find gcd of all ith elements.
    // where i = 0, 1, 2, 3.....n-2.
    int ans = lcm[0];

    for(int i = 1; i < n - 1; i++)
    {
        ans = gcd(ans, lcm[i]);
    }

    // Print the answer
    System.out.println(ans);
}

// Driver code
public static void main(String[] args)
{

    // 1st input case
    int n = 4;
    int a[] = { 10, 24, 40, 80 };

    // Function call for input 1
    gcd_of_lcm(n, a);

    // 2nd input case
    n = 10;
    int b[] = { 540, 648, 810, 648, 720,
                540, 594, 864, 972, 648 };

    // Function call for input 2
    gcd_of_lcm(n, b);
}
}

// This code is contributed by Soumitri Chattopadhyay
```

## 蟒蛇 3

```
# Python3 code to find the GCD of LCM
# of all unique pairs in an Array

from math import gcd

# find lcm of element x and y
def LCM(x, y):

    return (x * y)//gcd(x, y)

# Function that finds gcd of lcm
# of all pairs of elements.
def gcd_of_lcm(n, arr):

    # n is the size of the array.
    # arr is the array.

    # suffix array that stores
    # the gcd of the array elements.
    suff = [1]*n

    # initialize suffix array.

    # loop that make the suffix gcd array.
    suff[n-1] = arr[n-1]
    for i in range(n-2, -1, -1):

        suff[i] = gcd(arr[i], suff[i + 1])

    # lcm array that store the lcm
    # of ith elements for all j
    # that satisfy given condition.
    lcm = []

    for i in range(n-1):

        # we find lcm[i] for lcm
        # of ith elements for all j
        # using bellow formula.
        y = LCM( arr[i], suff[i + 1])

        # add lcm of ith elements
        # for all j in lcm array.
        lcm.append(y)

    # now we find gcd of all ith elements.
    # where i = 0, 1, 2, 3.....n-2.
    ans = lcm[0]
    for i in range(1, n-1):
        ans = gcd(ans, lcm[i])

    print(ans)

if __name__== "__main__":

    n = 4
    a =[10, 24, 40, 80]

    # function call for input 1
    gcd_of_lcm(n, a)

    n = 10
    a =[540, 648, 810, 648, 720,
        540, 594, 864, 972, 648]

    # function call for input 2
    gcd_of_lcm(n, a)
```

## C#

```
// C# code to find the GCD of LCM
// of all unique pairs in an array
using System;

class GFG{

// Function to evaluate GCD of x and y
static int gcd(int x, int y)
{
    if (y == 0)
        return x;
    else
        return gcd(y, x % y);
}

// Function that finds gcd of lcm
// of all pairs of elements.
static void gcd_of_lcm(int n, int[] arr)
{

    // n = size of array i.e. arr[]

    // Suffix array that stores
    // the GCD of the array elements.
    int[] suff = new int[n];

    // Initialise the suffix array
    for(int i = 0; i < n; i++)
        suff[i] = 1;

    // Loop that make suffix GCD array
    suff[n - 1] = arr[n - 1];

    for(int i = n - 2; i >= 0; i--)
        suff[i] = gcd(arr[i], suff[i + 1]);

    // lcm array that store lcm for pairwise
    // consecutive elements
    int[] lcm = new int[n - 1];

    for(int i = 0; i < n - 1; i++)

        // Find LCM using standard known formula
        lcm[i] = (arr[i] * suff[i + 1]) /
               gcd(arr[i], suff[i + 1]);

    // Now we find gcd of all ith elements.
    // where i = 0, 1, 2, 3.....n-2.
    int ans = lcm[0];

    for(int i = 1; i < n - 1; i++)
    {
        ans = gcd(ans, lcm[i]);
    }

    // Print the answer
    Console.WriteLine(ans);
}

// Driver code
public static void Main()
{

    // 1st input case
    int n = 4;
    int[] a = { 10, 24, 40, 80 };

    // Function call for input 1
    gcd_of_lcm(n, a);

    // 2nd input case
    n = 10;
    int[] b = { 540, 648, 810, 648, 720,
                540, 594, 864, 972, 648 };

    // Function call for input 2
    gcd_of_lcm(n, b);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript code to find the GCD of LCM
// of all unique pairs in an array

// Function to evaluate GCD of x and y
function gcd(x, y)
{
    if (y == 0)
        return x;
    else
        return gcd(y, x % y);
}

// Function that finds gcd of lcm
// of all pairs of elements.
function gcd_of_lcm(n, arr)
{

    // n = size of array i.e. arr[]

    // Suffix array that stores
    // the GCD of the array elements.
    let suff = new Array(n);

    // Initialise the suffix array
    for(let i = 0; i < n; i++)
        suff[i] = 1;

    // Loop that make suffix GCD array
    suff[n - 1] = arr[n - 1];

    for(let i = n - 2; i >= 0; i--)
        suff[i] = gcd(arr[i], suff[i + 1]);

    // lcm array that store lcm for pairwise
    // consecutive elements
    let lcm = new Array(n - 1);

    for(let i = 0; i < n - 1; i++)

        // Find LCM using standard known formula
        lcm[i] = parseInt((arr[i] * suff[i + 1]) /
                        gcd(arr[i], suff[i + 1]), 10);

    // Now we find gcd of all ith elements.
    // where i = 0, 1, 2, 3.....n-2.
    let ans = lcm[0];

    for(let i = 1; i < n - 1; i++)
    {
        ans = gcd(ans, lcm[i]);
    }

    // Print the answer
    document.write(ans + "</br>");
}

// Driver code

// 1st input case
let n = 4;
let a = [ 10, 24, 40, 80 ];

// Function call for input 1
gcd_of_lcm(n, a);

// 2nd input case
n = 10;
let b = [ 540, 648, 810, 648, 720,
          540, 594, 864, 972, 648 ];

// Function call for input 2
gcd_of_lcm(n, b);

// This code is contributed by rameshtravel07

</script>
```

**Output:** 

```
40
54
```

***时间复杂度:** O(N * log M)* ，其中 M 是数组中最大的元素。
***空间复杂度:** O(N)*