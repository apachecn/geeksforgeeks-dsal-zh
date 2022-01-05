# 将一个数表示为 k 个斐波那契数之和的方法数

> 原文:[https://www . geesforgeks . org/将一个数表示为 k 个斐波那契数之和的方法数/](https://www.geeksforgeeks.org/number-of-ways-to-represent-a-number-as-sum-of-k-fibonacci-numbers/)

给定两个数字 N 和 K，找出将 N 表示为 K 个斐波那契数之和的方法。
**例** :

```
Input : n = 12, k = 1 
Output : 0

Input : n = 13, k = 3
Output : 2
Explanation : 2 + 3 + 8, 3 + 5 + 5\.  
```

**逼近:**斐波那契数列为 f(0)=1，f(1)=2，f(i)=f(i-1)+f(i-2)为 i > 1。让我们假设 F(x，k，n)是利用来自 f(0)，f(1)，…f(n-1)的恰好 k 个数形成和 x 的方法数。要找到 F(x，k，n)的一个递归，注意有两种情况:f(n-1)是否在和中。

*   **如果 f(n-1)不在和中，**则 x 是使用来自 f(0)、f(1)、…、f(n-2)的恰好 k 个数形成的和。
*   **如果 f(n-1)在和中，**则剩余的 x-f(n-1)是使用来自 f(0)、f(1)、…、f(n-1)的恰好 k-1 个数字形成的。(请注意，f(n-1)仍然包含在内，因为允许重复的数字。).

所以递推关系为:

> F(x，k，n)= F(x，k，n-1)+F(x-f(n-1)，k-1，n)

**基本情况:**

*   如果 k=0，那么数列中有零个数字，所以和只能是 0。因此，F(0，0，n)=1。
*   F(x，0，n)=0，如果 x 不等于 0。

此外，还有其他情况使 F(x，k，n)=0，如下所示:

*   如果 k>0 且 x=0，因为至少有一个正数必然导致正和。
*   如果 k>0 并且 n=0，因为没有可能选择剩下的数字。
*   如果 x<0，因为没有办法用有限数量的非负数形成负和。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// to store fibonacci numbers
// 42 second number in fibonacci series
// largest possible integer
int fib[43] = { 0 };

// Function to generate fibonacci series
void fibonacci()
{
    fib[0] = 1;
    fib[1] = 2;
    for (int i = 2; i < 43; i++)
        fib[i] = fib[i - 1] + fib[i - 2];
}

// Recursive function to return the
// number of ways
int rec(int x, int y, int last)
{
    // base condition
    if (y == 0) {
        if (x == 0)
            return 1;
        return 0;
    }
    int sum = 0;
    // for recursive function call
    for (int i = last; i >= 0 and fib[i] * y >= x; i--) {
        if (fib[i] > x)
            continue;
        sum += rec(x - fib[i], y - 1, i);
    }
    return sum;
}

// Driver code
int main()
{
    fibonacci();
    int n = 13, k = 3;
    cout << "Possible ways are: "
         << rec(n, k, 42);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of above approach
public class AQW {

    //to store fibonacci numbers
    //42 second number in fibonacci series
    //largest possible integer
    static int fib[] = new int[43];

    //Function to generate fibonacci series
    static void fibonacci()
    {
     fib[0] = 1;
     fib[1] = 2;
     for (int i = 2; i < 43; i++)
         fib[i] = fib[i - 1] + fib[i - 2];
    }

    //Recursive function to return the
    //number of ways
    static int rec(int x, int y, int last)
    {
     // base condition
     if (y == 0) {
         if (x == 0)
             return 1;
         return 0;
     }
     int sum = 0;
     // for recursive function call
     for (int i = last; i >= 0 && fib[i] * y >= x; i--) {
         if (fib[i] > x)
             continue;
         sum += rec(x - fib[i], y - 1, i);
     }
     return sum;
    }

    //Driver code
    public static void main(String[] args) {

        fibonacci();
         int n = 13, k = 3;
         System.out.println("Possible ways are: "+ rec(n, k, 42));

    }

}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# To store fibonacci numbers 42 second
# number in fibonacci series largest
# possible integer
fib = [0] * 43

# Function to generate fibonacci
# series
def fibonacci():

    fib[0] = 1
    fib[1] = 2
    for i in range(2, 43):
        fib[i] = fib[i - 1] + fib[i - 2]

# Recursive function to return the
# number of ways
def rec(x, y, last):

    # base condition
    if y == 0:
        if x == 0:
            return 1
        return 0

    Sum, i = 0, last

    # for recursive function call
    while i >= 0 and fib[i] * y >= x:
        if fib[i] > x:
            i -= 1
            continue
        Sum += rec(x - fib[i], y - 1, i)
        i -= 1

    return Sum

# Driver code
if __name__ == "__main__":

    fibonacci()
    n, k = 13, 3
    print("Possible ways are:", rec(n, k, 42))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
    // to store fibonacci numbers
    // 42 second number in fibonacci series
    // largest possible integer
    static int[] fib = new int[43];

    // Function to generate fibonacci series
    public static void fibonacci()
    {
        fib[0] = 1;
        fib[1] = 2;
        for (int i = 2; i < 43; i++)
            fib[i] = fib[i - 1] + fib[i - 2];
    }

    // Recursive function to return the 
    // number of ways 
    public static int rec(int x, int y, int last)
    {
        // base condition
        if (y == 0) {
            if (x == 0)
                return 1;
            return 0;
        }
        int sum = 0;
        // for recursive function call
        for (int i = last; i >= 0 && fib[i] * y >= x; i--) {
            if (fib[i] > x)
                continue;
            sum += rec(x - fib[i], y - 1, i);
        }
        return sum;
    }

    // Driver code
    static void Main()
    {
        for(int i = 0; i < 43; i++)
            fib[i] = 0;
        fibonacci();
        int n = 13, k = 3;
        Console.Write("Possible ways are: " + rec(n, k, 42));
    }
    //This code is contributed by DrRoot_
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// To store fibonacci numbers
// 42 second number in fibonacci series
// largest possible integer
$fib = array_fill(0, 43, 0);

// Function to generate
// fibonacci series
function fibonacci()
{
    global $fib;
    $fib[0] = 1;
    $fib[1] = 2;
    for ($i = 2; $i < 43; $i++)
        $fib[$i] = $fib[$i - 1] +
                   $fib[$i - 2];
}

// Recursive function to return
// the number of ways
function rec($x, $y, $last)
{
    global $fib;

    // base condition
    if ($y == 0)
    {
        if ($x == 0)
            return 1;
        return 0;
    }
    $sum = 0;

    // for recursive function call
    for ($i = $last; $i >= 0 and
         $fib[$i] * $y >= $x; $i--)
    {
        if ($fib[$i] > $x)
            continue;
        $sum += rec($x - $fib[$i],
                    $y - 1, $i);
    }
    return $sum;
}

// Driver code
fibonacci();
$n = 13;
$k = 3;
echo "Possible ways are: " .
            rec($n, $k, 42);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
//Javascript implementation of above approach

    //to store fibonacci numbers
    //42 second number in fibonacci series
    //largest possible integer
    let fib=new Array(43);

    //Function to generate fibonacci series
    function fibonacci()
    {
        fib[0] = 1;
     fib[1] = 2;
     for (let i = 2; i < 43; i++)
         fib[i] = fib[i - 1] + fib[i - 2];
    }

    //Recursive function to return the
    //number of ways
    function rec(x,y,last)
    {
        // base condition
     if (y == 0) {
         if (x == 0)
             return 1;
         return 0;
      }
     let sum = 0;
     // for recursive function call
     for (let i = last; i >= 0 && fib[i] * y >= x; i--) {
         if (fib[i] > x)
             continue;
         sum += rec(x - fib[i], y - 1, i);
     }
     return sum;
    }

    //Driver code
    fibonacci();
     let n = 13, k = 3;
     document.write("Possible ways are: "+ rec(n, k, 42));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Possible ways are: 2
```