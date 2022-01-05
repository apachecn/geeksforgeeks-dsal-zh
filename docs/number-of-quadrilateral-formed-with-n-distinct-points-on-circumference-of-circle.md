# 圆周上由 N 个不同点形成的四边形的数目

> 原文:[https://www . geeksforgeeks . org/圆周上有 n 个不同点的四边形数量/](https://www.geeksforgeeks.org/number-of-quadrilateral-formed-with-n-distinct-points-on-circumference-of-circle/)

给定一个整数 **N** ，它表示圆圆周上的点，任务是找出用这些点形成的四边形的数量。
**例:**

> **输入:** N = 5
> **输出:** 5
> **输入:** N = 10
> **输出:** 210

**方法:**思路是利用[排列组合](https://www.geeksforgeeks.org/permutation-and-combination/)利用圆圆周上的 N 个点找到可能的四边形的个数。可能的四边形数量将是![^{N}C_4  ](img/6824b08fae05aefe631268f6b36bd28d.png "Rendered by QuickLaTeX.com")。
以下是上述方法的实施:

## C++

```
// C++ implementation to find the
// number of quadrilaterals formed
// with N distinct points
#include<bits/stdc++.h>
using namespace std;

// Function to find the factorial
// of the given number N
int fact(int n)
{
    int res = 1;

    // Loop to find the factorial
    // of the given number
    for(int i = 2; i < n + 1; i++)
       res = res * i;

    return res;
}

// Function to find the number of
// combinations in the N
int nCr(int n, int r)
{
    return (fact(n) / (fact(r) *
                       fact(n - r)));
}

// Driver Code
int main()
{
    int n = 5;

    // Function Call
    cout << (nCr(n, 4));
}

// This code is contributed by rock_cool
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// number of quadrilaterals formed
// with N distinct points
class GFG{

// Function to find the number of
// combinations in the N
static int nCr(int n, int r)
{
    return (fact(n) / (fact(r) *
                       fact(n - r)));
}

// Function to find the factorial
// of the given number N
static int fact(int n)
{
    int res = 1;

    // Loop to find the factorial
    // of the given number
    for(int i = 2; i < n + 1; i++)
        res = res * i;
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;

    // Function Call
    System.out.println(nCr(n, 4));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to find the
# number of quadrilaterals formed
# with N distinct points

# Function to find the number of
# combinations in the N
def nCr(n, r):
    return (fact(n) / (fact(r)
                * fact(n - r)))

# Function to find the factorial
# of the given number N
def fact(n):
    res = 1

    # Loop to find the factorial
    # of the given number
    for i in range(2, n + 1):
        res = res * i    
    return res

# Driver Code
if __name__ == "__main__":
    n = 5

    # Function Call
    print(int(nCr(n, 4)))
```

## C#

```
// C# implementation to find the
// number of quadrilaterals formed
// with N distinct points
using System;
class GFG{

// Function to find the number of
// combinations in the N
static int nCr(int n, int r)
{
    return (fact(n) / (fact(r) *
                       fact(n - r)));
}

// Function to find the factorial
// of the given number N
static int fact(int n)
{
    int res = 1;

    // Loop to find the factorial
    // of the given number
    for(int i = 2; i < n + 1; i++)
        res = res * i;
    return res;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;

    // Function Call
    Console.Write(nCr(n, 4));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript implementation to find the
// number of quadrilaterals formed
// with N distinct points

// Function to find the factorial
// of the given number N
function fact(n)
{
    let res = 1;

    // Loop to find the factorial
    // of the given number
    for(let i = 2; i < n + 1; i++)
    res = res * i;

    return res;
}

// Function to find the number of
// combinations in the N
function nCr(n, r)
{
    return (fact(n) / (fact(r) *
                    fact(n - r)));
}

// Driver Code

    let n = 5;

    // Function Call
    document.write(nCr(n, 4));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
5
```