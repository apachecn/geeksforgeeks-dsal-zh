# 小于或等于可被 K 整除的 N 的最大数值

> 原文:[https://www . geesforgeks . org/最大数-小于或等于 n-可被 k 整除/](https://www.geeksforgeeks.org/largest-number-smaller-than-or-equal-to-n-divisible-by-k/)

给定一个数 N 和一个数 K，任务是找出小于或等于 N 的最大的可被 K 整除的数
**例:**

```
Input: N = 45, K = 6
Output: 42
42 is the largest number smaller than 
or equal to 45 which is divisible by 6.

Input: N = 11, K = 3
Output: 9
```

**方法:**思路是 N 除以 k，如果余数为 0，则打印 **N** 否则打印**N–余数**。
以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the largest number
// smaller than or equal to N
// that is divisible by k
int findNum(int N, int K)
{
    int rem = N % K;

    if (rem == 0)
        return N;
    else
        return N - rem;
}

// Driver code
int main()
{
    int N = 45, K = 6;

    cout << "Largest number smaller than or equal to "<< N
         << "\nthat is divisible by "<< K  << " is " << findNum(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.lang.*;
import java.util.*;

class GFG
{
// Function to find the largest number
// smaller than or equal to N
// that is divisible by k
static int findNum(int N, int K)
{
    int rem = N % K;

    if (rem == 0)
        return N;
    else
        return N - rem;
}

// Driver code
public static void main(String args[])
{
    int N = 45, K = 6;

    System.out.print("Largest number smaller " +
                       "than or equal to " + N +
                 "\nthat is divisible by " + K +
                        " is " + findNum(N, K));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find the largest number smaller
# than or equal to N that is divisible by k
def findNum(N, K):

    rem = N % K
    if(rem == 0):
        return N
    else:
        return N - rem

# Driver code
if __name__=='__main__':

    N = 45
    K = 6
    print("Largest number smaller than or equal to" +
           str(N) + "that is divisible by" + str(K) +
                                "is", findNum(N, K))

# This code is contributed by
# Kirti_Mangal
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
// Function to find the largest number
// smaller than or equal to N
// that is divisible by k
static int findNum(int N, int K)
{
    int rem = N % K;

    if (rem == 0)
        return N;
    else
        return N - rem;
}

// Driver code
public static void Main()
{
    int N = 45, K = 6;

    Console.Write("Largest number smaller " +
                     "than or equal to "+ N +
               "\nthat is divisible by "+ K +
                     " is " + findNum(N, K));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// Function to find the largest
// number smaller than or equal
// to N that is divisible by k
function findNum($N, $K)
{
    $rem = $N % $K;

    if ($rem == 0)
        return $N;
    else
        return $N - $rem;
}

// Driver code
$N = 45 ;
$K = 6 ;

echo"Largest number smaller than or equal to ", $N,
    "\nthat is divisible by ", $K, " is ",
    findNum($N, $K);

// This code is contributed by ANKITRAI1
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find the largest number
// smaller than or equal to N
// that is divisible by k
function findNum(N, K)
{
    var rem = N % K;

    if (rem == 0)
        return N;
    else
        return N - rem;
}

// Driver code
var N = 45, K = 6;
document.write( "Largest number smaller than or equal to " + N
     + "<br>that is divisible by " + K + " is " + findNum(N, K));

</script>
```

**Output:** 

```
Largest number smaller than or equal to 45
that is divisible by 6 is 42
```

**时间复杂度:** O(1)

**辅助空间:** O(1)