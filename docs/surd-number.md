# 姓氏

> 原文:[https://www.geeksforgeeks.org/surd-number/](https://www.geeksforgeeks.org/surd-number/)

如果一个数的平方根、立方根等不是整数，则称它为 Surd。比如 9 不是 Surd，因为 9 的平方根是 3，但是 5 是 Surd，因为 5 的平方根不是整数。同样，8 不是 Surd(8 的立方根是整数)，但 7 是。
给定一个范围，找出是不是 Surds
T2【例:T4】

```
Input : 4
Output : No
4 is not a Surd number as its square root is
an integer.

Input : 5
Output : Yes
5 is a Surd number as its square root is not an integer.

Input : 8
Output : No
8 is not a Surd number as cube root of 8
is an integer.
```

想法是尝试从 2 到√n 的所有数字的每一次幂，并检查任何幂是否等于 n。

## C++

```
// CPP program to find if a number is
// Surds or not
#include <bits/stdc++.h>
using namespace std;

// Returns true if x is Surd number
bool isSurd(int n)
{ 
    for (int i=2; i*i<=n; i++)
    {
       // Try all powers of i
       int j = i;
       while (j < n)             
          j = j * i;

       if (j == n)
          return false;
    }

    return true;
}

// driver code
int main()
{ 
    int n = 15;
    if (isSurd(n))
       cout << "Yes";
    else
       cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a
// number is Surds or not

class GFG
{

// Returns true if x
// is Surd number
static boolean isSurd(int n)
{
    for (int i = 2;
             i * i <= n; i++)
    {
        // Try all powers of i
        int j = i;
        while (j < n)            
            j = j * i;

        if (j == n)
            return false;
    }

    return true;
}

// Driver Code
public static void main(String args[])
{
    int n = 15;
    if (isSurd(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed
// by Ankita_Saini
```

## 蟒蛇 3

```
# Python3 program to find
# if a number is Surd or not.

# define a isSurd function which
# Returns true if x is Surd number.
def isSurd(n) :

    i = 2
    for i in range(2, (i * i) + 1) :

        # Try all powers of i
        j = i
        while (j < n) :
            j = j * i

        if (j == n) :
            return False

    return True

# Driver code
if __name__ == "__main__" :

    n = 15

    if (isSurd(n)) :
        print("Yes")

    else :
        print("No")

# This code is contributed
# by Ankit Rai1
```

## C#

```
// C# program to find if a
// number is Surds or not
using System;

class GFG
{

// Returns true if x
// is Surd number
static bool isSurd(int n)
{
    for (int i = 2;
             i * i <= n; i++)
    {
        // Try all powers of i
        int j = i;
        while (j < n)            
            j = j * i;

        if (j == n)
            return false;
    }

    return true;
}

// Driver Code
public static void Main()
{
    int n = 15;
    if (isSurd(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if
// a number is Surds or not

// Returns true if
// x is Surd number
function isSurd($n)
{
    for ($i = 2;
         $i * $i <= $n; $i++)
    {
    // Try all powers of i
    $j = $i;
    while ($j < $n)            
        $j = $j * $i;

    if ($j == $n)
        return false;
    }

    return true;
}

// Driver code
$n = 15;
if (isSurd($n))
    echo ("Yes");
else
    echo ("No");

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to find if a
// number is Surds or not

    // Returns true if x
// is Surd number
    function isSurd(n)
    {
        for (let i = 2;
             i * i <= n; i++)
    {
        // Try all powers of i
        let j = i;
        while (j < n)            
            j = j * i;

        if (j == n)
            return false;
    }

    return true;
    }

    // Driver Code
    let n = 15;
    if (isSurd(n))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Yes
```