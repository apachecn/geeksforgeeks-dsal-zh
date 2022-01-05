# 计算第一半位和第二半位总和相同的偶数长度二进制序列

> 原文:[https://www . geesforgeks . org/count-偶数长度二进制序列-具有相同的第一和第二半位之和/](https://www.geeksforgeeks.org/count-even-length-binary-sequences-with-same-sum-of-first-and-second-half-bits/)

给定一个数 n，求长度为 2n 的所有二进制序列的计数，使得前 n 位的和与后 n 位的和相同。

**示例:**

```
Input:  n = 1
Output: 2
There are 2 sequences of length 2*n, the
sequences are 00 and 11

Input:  n = 2
Output: 6
There are 6 sequences of length 2*n, the
sequences are 0101, 0110, 1010, 1001, 0000
and 1111
```

其思想是固定第一个和最后一个位，然后重复 n-1 个位，即剩余的 2(n-1)个位。当我们修复第一位和最后一位时，有以下几种可能性。
1)第一位和最后一位相同，两边剩余的 n-1 位也应该有相同的**和。
2)第一位为 1，最后一位为 0，左侧剩余 n-1 位之和应比右侧 n-1 位之和少 1**。
2)第一位为 0，最后一位为 1，左侧剩余 n-1 位之和应比右侧 n-1 位之和多 1**。******

******基于以上事实，我们得到以下递推公式。
**diff** 是前半位数和后半位数之和的预期差值。初始差异为 0。******

```
 **// When first and last bits are same
                  // there are two cases, 00 and 11
count(n, diff) =  2*count(n-1, diff) +    

                 // When first bit is 1 and last bit is 0
                 count(n-1, diff-1) +

                 // When first bit is 0 and last bit is 1
                 count(n-1, diff+1)

What should be base cases?
// When n == 1 (2 bit sequences)
1) If n == 1 and diff == 0, return 2
2) If n == 1 and |diff| == 1, return 1 

// We can't cover difference of more than n with 2n bits
3) If |diff| > n, return 0**
```

****下面是基于以上**朴素递归解**的实现。****

## ****C++****

```
**// A Naive Recursive C++ program to count even
// length binary sequences such that the sum of
// first and second half bits is same
#include<bits/stdc++.h>
using namespace std;

// diff is difference between sums first n bits
// and last n bits respectively
int countSeq(int n, int diff)
{
    // We can't cover difference of more
    // than n with 2n bits
    if (abs(diff) > n)
        return 0;

    // n == 1, i.e., 2 bit long sequences
    if (n == 1 && diff == 0)
        return 2;
    if (n == 1 && abs(diff) == 1)
        return 1;

    int res = // First bit is 0 & last bit is 1
              countSeq(n-1, diff+1) +

              // First and last bits are same
              2*countSeq(n-1, diff) +

              // First bit is 1 & last bit is 0
              countSeq(n-1, diff-1);

    return res;
}

// Driver program
int main()
{
    int n = 2;
    cout << "Count of sequences is "
         << countSeq(2, 0);
    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// A Naive Recursive Java program to
// count even length binary sequences
// such that the sum of first and
// second half bits is same
import java.io.*;

class GFG {

// diff is difference between sums
// first n bits and last n bits respectively
static int countSeq(int n, int diff)
{
    // We can't cover difference of more
    // than n with 2n bits
    if (Math.abs(diff) > n)
        return 0;

    // n == 1, i.e., 2 bit long sequences
    if (n == 1 && diff == 0)
        return 2;
    if (n == 1 && Math.abs(diff) == 1)
        return 1;

    int res = // First bit is 0 & last bit is 1
            countSeq(n-1, diff+1) +

            // First and last bits are same
            2*countSeq(n-1, diff) +

            // First bit is 1 & last bit is 0
            countSeq(n-1, diff-1);

    return res;
}

// Driver program
public static void main(String[] args)
{
    int n = 2;
    System.out.println("Count of sequences is "
                       + countSeq(2, 0));
}
}

// This code is contributed by Prerna Saini**
```

## ****蟒蛇 3****

```
**# A Naive Recursive Python
# program to count even length
# binary sequences such that
# the sum of first and second
# half bits is same

# diff is difference between
# sums first n bits and last
# n bits respectively
def countSeq(n, diff):

    # We can't cover difference
    # of more than n with 2n bits
    if (abs(diff) > n):
        return 0

    # n == 1, i.e., 2
    # bit long sequences
    if (n == 1 and diff == 0):
        return 2
    if (n == 1 and abs(diff) == 1):
        return 1

    # First bit is 0 & last bit is 1
    # First and last bits are same
    # First bit is 1 & last bit is 0
    res = (countSeq(n - 1, diff + 1) +
           2 * countSeq(n - 1, diff) +
            countSeq(n - 1, diff - 1))    

    return res

# Driver Code
n = 2;
print("Count of sequences is %d " %
                  (countSeq(2, 0)))

# This code is contributed
# by Shivi_Aggarwal**
```

## ****C#****

```
**// A Naive Recursive C# program to
// count even length binary sequences
// such that the sum of first and
// second half bits is same
using System;

class GFG {

    // diff is difference between sums
    // first n bits and last n bits
    // respectively
    static int countSeq(int n, int diff)
    {
        // We can't cover difference
        // of more than n with 2n bits
        if (Math.Abs(diff) > n)
            return 0;

        // n == 1, i.e., 2 bit long
        // sequences
        if (n == 1 && diff == 0)
            return 2;
        if (n == 1 && Math.Abs(diff) == 1)
            return 1;

        // 1\. First bit is 0 & last bit is 1
        // 2\. First and last bits are same
        // 3\. First bit is 1 & last bit is 0
        int res = countSeq(n-1, diff+1) +
                2 * countSeq(n-1, diff) +
                   countSeq(n-1, diff-1);

        return res;
    }

    // Driver program
    public static void Main()
    {
        Console.Write("Count of sequences is "
                             + countSeq(2, 0));
    }
}

// This code is contributed by nitin mittal.**
```

## ****服务器端编程语言（Professional Hypertext Preprocessor 的缩写）****

```
**<?php
// A Naive Recursive PHP program
// to count even length binary
// sequences such that the sum of
// first and second half bits is same

// diff is difference between
// sums first n bits and last
// n bits respectively
function countSeq($n, $diff)
{
    // We can't cover difference of
    // more than n with 2n bits
    if (abs($diff) > $n)
        return 0;

    // n == 1, i.e., 2
    // bit long sequences
    if ($n == 1 && $diff == 0)
        return 2;

    if ($n == 1 && abs($diff) == 1)
        return 1;

    $res = // First bit is 0 & last bit is 1
            countSeq($n - 1, $diff + 1) +

            // First and last bits are same
            2 * countSeq($n - 1, $diff) +

            // First bit is 1 & last bit is 0
            countSeq($n - 1, $diff - 1);

    return $res;
}

// Driver Code
$n = 2;
echo "Count of sequences is ",
              countSeq($n, 0);

// This code is contributed
// by shiv_bhakt.
?>**
```

## ****java 描述语言****

```
**<script>
// A Naive Recursive Javascript program to
// count even length binary sequences
// such that the sum of first and
// second half bits is same

    // diff is difference between sums
    // first n bits and last n bits respectively
    function countSeq(n,diff)
    {

        // We can't cover difference of more
        // than n with 2n bits
        if (Math.abs(diff) > n)
            return 0;

        // n == 1, i.e., 2 bit long sequences
        if (n == 1 && diff == 0)
            return 2;
        if (n == 1 && Math.abs(diff) == 1)
            return 1;

        let res = // First bit is 0 & last bit is 1
                countSeq(n-1, diff+1) +

                // First and last bits are same
                2*countSeq(n-1, diff) +

                // First bit is 1 & last bit is 0
                countSeq(n-1, diff-1);

        return res;
    }

    // Driver program
    let n = 2;
    document.write("Count of sequences is "
                       + countSeq(2, 0));

    // This code is contributed by avanitrachhadiya2155
</script>**
```

******输出:******

```
**Count of sequences is 6**
```

****上述解的时间复杂度是指数的。如果我们画出完整的递归树，我们可以观察到许多子问题被一次又一次地解决。例如，当我们从 n = 4 和 diff = 0 开始时，我们可以通过多条路径到达(3，0)。由于相同的子问题被再次调用，这个问题具有重叠子问题的性质。所以最小二乘和问题具有一个**动态规划**问题的两个性质(见[这个](https://www.geeksforgeeks.org/dynamic-programming-set-1/)和[这个](https://www.geeksforgeeks.org/dynamic-programming-set-2-optimal-substructure-property/))。****

****下面是一个基于记忆的解决方案，使用查找表来计算结果。****

## ****C++****

```
**// A memoization based C++ program to count even
// length binary sequences such that the sum of
// first and second half bits is same
#include<bits/stdc++.h>
using namespace std;
#define MAX 1000

// A lookup table to store the results of subproblems
int lookup[MAX][MAX];

// dif is difference between sums of first n bits
// and last n bits i.e., dif = (Sum of first n bits) -
//                              (Sum of last n bits)
int countSeqUtil(int n, int dif)
{
    // We can't cover difference of more
    // than n with 2n bits
    if (abs(dif) > n)
        return 0;

    // n == 1, i.e., 2 bit long sequences
    if (n == 1 && dif == 0)
        return 2;
    if (n == 1 && abs(dif) == 1)
        return 1;

    // Check if this subproblem is already solved
    // n is added to dif to make sure index becomes
    // positive
    if (lookup[n][n+dif] != -1)
        return lookup[n][n+dif];

    int res = // First bit is 0 & last bit is 1
              countSeqUtil(n-1, dif+1) +

              // First and last bits are same
              2*countSeqUtil(n-1, dif) +

              // First bit is 1 & last bit is 0
              countSeqUtil(n-1, dif-1);

    // Store result in lookup table and return the result
    return lookup[n][n+dif] = res;
}

// A Wrapper over countSeqUtil().  It mainly initializes lookup
// table, then calls countSeqUtil()
int countSeq(int n)
{
    // Initialize all entries of lookup table as not filled
    memset(lookup, -1, sizeof(lookup));

    // call countSeqUtil()
    return countSeqUtil(n, 0);
}

// Driver program
int main()
{
    int n = 2;
    cout << "Count of sequences is "
         << countSeq(2);
    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// A memoization based Java program to
// count even length binary sequences
// such that the sum of first and
// second half bits is same
import java.io.*;

class GFG {

// A lookup table to store the results of
// subproblems
static int lookup[][] = new int[1000][1000];

// dif is difference between sums of first
// n bits and last n bits i.e.,
// dif = (Sum of first n bits) - (Sum of last n bits)
static int countSeqUtil(int n, int dif)
{
    // We can't cover difference of
    // more than n with 2n bits
    if (Math.abs(dif) > n)
        return 0;

    // n == 1, i.e., 2 bit long sequences
    if (n == 1 && dif == 0)
        return 2;
    if (n == 1 && Math.abs(dif) == 1)
        return 1;

    // Check if this subproblem is already
    // solved n is added to dif to make
    // sure index becomes positive
    if (lookup[n][n+dif] != -1)
        return lookup[n][n+dif];

    int res = // First bit is 0 & last bit is 1
            countSeqUtil(n-1, dif+1) +

            // First and last bits are same
            2*countSeqUtil(n-1, dif) +

            // First bit is 1 & last bit is 0
            countSeqUtil(n-1, dif-1);

    // Store result in lookup table
    // and return the result
    return lookup[n][n+dif] = res;
}

// A Wrapper over countSeqUtil(). It mainly
// initializes lookup table, then calls
// countSeqUtil()
static int countSeq(int n)
{
    // Initialize all entries of lookup
    // table as not filled
    // memset(lookup, -1, sizeof(lookup));
    for(int k = 0; k < lookup.length; k++)
    {
        for(int j = 0; j < lookup.length; j++)
        {
        lookup[k][j] = -1;
    }
    }

    // call countSeqUtil()
    return countSeqUtil(n, 0);
}

// Driver program
public static void main(String[] args)
{
    int n = 2;
    System.out.println("Count of sequences is "
                       + countSeq(2));
}
}

// This code is contributed by Prerna Saini**
```

## ****蟒蛇 3****

```
**#A memoization based python program to count even
#length binary sequences such that the sum of
#first and second half bits is same

MAX=1000

#A lookup table to store the results of subproblems
lookup=[[0 for i in range(MAX)] for i in range(MAX)]
#dif is difference between sums of first n bits
#and last n bits i.e., dif = (Sum of first n bits) -
#                             (Sum of last n bits)
def countSeqUtil(n,dif):

    #We can't cover difference of more
    #than n with 2n bits
    if abs(dif)>n:
        return 0
    #n == 1, i.e., 2 bit long sequences
    if n==1 and dif==0:
        return 2
    if n==1 and abs(dif)==1:
        return 1

    #Check if this subproblem is already solved
    #n is added to dif to make sure index becomes
    #positive
    if lookup[n][n+dif]!=-1:
        return lookup[n][n+dif]

    #First bit is 0 & last bit is 1
    #+First and last bits are same
    #+First bit is 1 & last bit is 0
    res= (countSeqUtil(n-1, dif+1)+
          2*countSeqUtil(n-1, dif)+
          countSeqUtil(n-1, dif-1))

    #Store result in lookup table and return the result
    lookup[n][n+dif]=res
    return res

#A Wrapper over countSeqUtil(). It mainly initializes lookup
#table, then calls countSeqUtil()
def countSeq(n):
    #Initialize all entries of lookup table as not filled
    global lookup
    lookup=[[-1 for i in range(MAX)] for i in range(MAX)]
    #call countSeqUtil()
    res=countSeqUtil(n,0)
    return res

#Driver Code
if __name__=='__main__':
    n=2
    print('Count of Sequences is ',countSeq(n))

#This Code is contributed by sahilshelangia**
```

## ****C#****

```
**// A memoization based C# program to
// count even length binary sequences
// such that the sum of first and
// second half bits is same

using System;
class GFG {

// A lookup table to store the results of
// subproblems
static int [,]lookup = new int[1000,1000];

// dif is difference between sums of first
// n bits and last n bits i.e.,
// dif = (Sum of first n bits) - (Sum of last n bits)
static int countSeqUtil(int n, int dif)
{
    // We can't cover difference of
    // more than n with 2n bits
    if (Math.Abs(dif) > n)
        return 0;

    // n == 1, i.e., 2 bit long sequences
    if (n == 1 && dif == 0)
        return 2;
    if (n == 1 && Math.Abs(dif) == 1)
        return 1;

    // Check if this subproblem is already
    // solved n is added to dif to make
    // sure index becomes positive
    if (lookup[n,n+dif] != -1)
        return lookup[n,n+dif];

    int res = // First bit is 0 & last bit is 1
            countSeqUtil(n-1, dif+1) +

            // First and last bits are same
            2*countSeqUtil(n-1, dif) +

            // First bit is 1 & last bit is 0
            countSeqUtil(n-1, dif-1);

    // Store result in lookup table
    // and return the result
    return lookup[n,n+dif] = res;
}

// A Wrapper over countSeqUtil(). It mainly
// initializes lookup table, then calls
// countSeqUtil()
static int countSeq(int n)
{
    // Initialize all entries of lookup
    // table as not filled
    // memset(lookup, -1, sizeof(lookup));
    for(int k = 0; k < lookup.GetLength(0); k++)
    {
        for(int j = 0; j < lookup.GetLength(1); j++)
        {
        lookup[k,j] = -1;
    }
    }

    // call countSeqUtil()
    return countSeqUtil(n, 0);
}

// Driver program
public static void Main()
{
    int n = 2;
    Console.WriteLine("Count of sequences is "
                    + countSeq(n));
}
}

// This code is contributed by Ryuga**
```

## ****服务器端编程语言（Professional Hypertext Preprocessor 的缩写）****

```
**<?php
// A memoization based PHP program to count even
// length binary sequences such that the sum of
// first and second half bits is same
$MAX = 1000;

// A lookup table to store the results
// of subproblems
$lookup = array_fill(0, $MAX,
          array_fill(0, $MAX, -1));

// dif is difference between sums of first n bits
// and last n bits i.e., dif = (Sum of first n bits) -
//                               (Sum of last n bits)
function countSeqUtil($n, $dif)
{
    global $lookup;

    // We can't cover difference of more
    // than n with 2n bits
    if (abs($dif) > $n)
        return 0;

    // n == 1, i.e., 2 bit long sequences
    if ($n == 1 && $dif == 0)
        return 2;
    if ($n == 1 && abs($dif) == 1)
        return 1;

    // Check if this subproblem is already solved
    // n is added to dif to make sure index becomes
    // positive
    if ($lookup[$n][$n + $dif] != -1)
        return $lookup[$n][$n + $dif];

    $res = // First bit is 0 & last bit is 1
            countSeqUtil($n - 1, $dif + 1) +

            // First and last bits are same
            2 * countSeqUtil($n - 1, $dif) +

            // First bit is 1 & last bit is 0
            countSeqUtil($n - 1, $dif - 1);

    // Store result in lookup table and return the result
    return $lookup[$n][$n + $dif] = $res;
}

// A Wrapper over countSeqUtil(). It mainly
// initializes lookup table, then calls countSeqUtil()
function countSeq($n)
{
    // Initialize all entries of
    // lookup table as not filled

    // call countSeqUtil()
    return countSeqUtil($n, 0);
}

// Driver Code
$n = 2;
echo "Count of sequences is " . countSeq($n);

// This code is contributed by mits
?>**
```

## ****java 描述语言****

```
**<script>
// A memoization based Javascript program to
// count even length binary sequences
// such that the sum of first and
// second half bits is same

    // A lookup table to store the results of
    // subproblems
    let lookup = new Array(1000);
    for(let i = 0; i < 1000; i++)
    {
        lookup[i] = new Array(1000);
    }

    // dif is difference between sums of first
    // n bits and last n bits i.e.,
    // dif = (Sum of first n bits) - (Sum of last n bits)
    function countSeqUtil(n, dif)
    {

        // We can't cover difference of
        // more than n with 2n bits
        if (Math.abs(dif) > n)
            return 0;

        // n == 1, i.e., 2 bit long sequences
        if (n == 1 && dif == 0)
            return 2;
        if (n == 1 && Math.abs(dif) == 1)
            return 1;

        // Check if this subproblem is already
        // solved n is added to dif to make
        // sure index becomes positive
        if (lookup[n][n + dif] != -1)
            return lookup[n][n + dif];

        let res = // First bit is 0 & last bit is 1
                countSeqUtil(n - 1, dif + 1) +

                // First and last bits are same
                2*countSeqUtil(n - 1, dif) +

                // First bit is 1 & last bit is 0
                countSeqUtil(n - 1, dif - 1);

        // Store result in lookup table
        // and return the result
        return lookup[n][n + dif] = res;
    }

    // A Wrapper over countSeqUtil(). It mainly
    // initializes lookup table, then calls
    // countSeqUtil()
    function countSeq(n)
    {

        // Initialize all entries of lookup
        // table as not filled
        // memset(lookup, -1, sizeof(lookup));
        for(let k = 0; k < lookup.length; k++)
        {
            for(let j = 0; j < lookup.length; j++)
            {
                lookup[k][j] = -1;
            }
        }

        // call countSeqUtil()
        return countSeqUtil(n, 0);
    }

    // Driver program
    let n = 2;
    document.write("Count of sequences is "
                       + countSeq(2));

    // This code is contributed by rag2127
</script>**
```

******输出:******

```
**Count of sequences is 6**
```

****该解决方案的最坏情况时间复杂度为 0(n<sup>2</sup>)，因为 diff 可以是最大 n。****

****下图为相同的 **O(n)溶液**。****

```
**Number of n-bit strings with 0 ones = nC0
Number of n-bit strings with 1 ones = nC1
...
Number of n-bit strings with k ones = nCk
...
Number of n-bit strings with n ones = nCn** 
```

****因此，我们可以使用以下内容获得所需的结果****

```
**No. of 2*n bit strings such that first n bits have 0 ones & 
last n bits have 0 ones = nC0 * nC0

No. of 2*n bit strings such that first n bits have 1 ones & 
last n bits have 1 ones = nC1 * nC1

....

and so on.

Result = nC0*nC0 + nC1*nC1 + ... + nCn*nCn
       = ∑(nCk)<sup>2</sup> 
        0 <= k <= n** 
```

****以下是基于上述思想的实现。****

## ****C++****

```
**// A O(n) C++ program to count even length binary sequences
// such that the sum of first and second half bits is same
#include<iostream>
using namespace std;

// Returns the count of even length sequences
int countSeq(int n)
{
    int nCr=1, res = 1;

    // Calculate SUM ((nCr)^2)
    for (int r = 1; r<=n ; r++)
    {
        // Compute nCr using nC(r-1)
        // nCr/nC(r-1) = (n+1-r)/r;
        nCr = (nCr * (n+1-r))/r;  

        res += nCr*nCr;
    }

    return res;
}

// Driver program
int main()
{
    int n = 2;
    cout << "Count of sequences is "
         << countSeq(n);
    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program to find remaining
// chocolates after k iterations
class GFG
{
// A O(n) C++ program to count
// even length binary sequences
// such that the sum of first
// and second half bits is same

// Returns the count of
// even length sequences
static int countSeq(int n)
{
    int nCr = 1, res = 1;

    // Calculate SUM ((nCr)^2)
    for (int r = 1; r <= n ; r++)
    {
        // Compute nCr using nC(r-1)
        // nCr/nC(r-1) = (n+1-r)/r;
        nCr = (nCr * (n + 1 - r)) / r;

        res += nCr * nCr;
    }

    return res;
}

// Driver code
public static void main(String args[])
{
    int n = 2;
    System.out.print("Count of sequences is ");
    System.out.println(countSeq(n));
}
}

// This code is contributed
// by Shivi_Aggarwal**
```

## ****计算机编程语言****

```
**# A Python program to count
# even length binary sequences
# such that the sum of first
# and second half bits is same

# Returns the count of
# even length sequences
def countSeq(n):

    nCr = 1
    res = 1

    # Calculate SUM ((nCr)^2)
    for r in range(1, n + 1):

        # Compute nCr using nC(r-1)
        # nCr/nC(r-1) = (n+1-r)/r;
        nCr = (nCr * (n + 1 - r)) / r;

        res += nCr * nCr;

    return res;

# Driver Code
n = 2
print("Count of sequences is"),
print (int(countSeq(n)))

# This code is contributed
# by Shivi_Aggarwal**
```

## ****C#****

```
**// C# program to find remaining
// chocolates after k iteration
using System;

class GFG {

// A O(n) C# program to count
// even length binary sequences
// such that the sum of first
// and second half bits is same

// Returns the count of
// even length sequences
static int countSeq(int n)
{
    int nCr = 1, res = 1;

    // Calculate SUM ((nCr)^2)
    for (int r = 1; r <= n ; r++)
    {
        // Compute nCr using nC(r-1)
        // nCr/nC(r-1) = (n+1-r)/r;
        nCr = (nCr * (n + 1 - r)) / r;

        res += nCr * nCr;
    }

    return res;
}

// Driver code
public static void Main()
{
    int n = 2;
    Console.Write("Count of sequences is ");
    Console.Write(countSeq(n));
}
}

// This code is contributed
// by ChitraNayal**
```

## ****服务器端编程语言（Professional Hypertext Preprocessor 的缩写）****

```
**<?php
// A Php program to count even
// length binary sequences
// such that the sum of first
// and second half bits is same

// Returns the count of
// even length sequences
function countSeq($n)
{
    $nCr = 1;
    $res = 1;

    // Calculate SUM ((nCr)^2)
    for ($r = 1; $r <= $n; $r++)
    {
        // Compute nCr using nC(r-1)
        // nCr/nC(r-1) = (n+1-r)/r;
        $nCr = ($nCr * ($n + 1 - $r)) / $r;

        $res = $res + ($nCr * $nCr);
    }

    return $res;
}

// Driver Code
$n = 2;
echo ("Count of sequences is ");
echo countSeq($n);

// This code is contributed
// by Shivi_Aggarwal
?>**
```

## ****java 描述语言****

```
**<script>
    // Javascript program to find remaining chocolates after k iteration

    // A O(n) C# program to count
    // even length binary sequences
    // such that the sum of first
    // and second half bits is same

    // Returns the count of
    // even length sequences
    function countSeq(n)
    {
        let nCr = 1, res = 1;

        // Calculate SUM ((nCr)^2)
        for (let r = 1; r <= n ; r++)
        {
            // Compute nCr using nC(r-1)
            // nCr/nC(r-1) = (n+1-r)/r;
            nCr = (nCr * (n + 1 - r)) / r;

            res += nCr * nCr;
        }

        return res;
    }

    let n = 2;
    document.write("Count of sequences is ");
    document.write(countSeq(n));

    // This code is contributed by mukesh07.
</script>**
```

******输出:******

```
**Count of sequences is 6**
```

****感谢 d_geeks，Saurabh Jain 和神秘心灵提出上述 O(n)解决方案。
本文由帕万供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息****