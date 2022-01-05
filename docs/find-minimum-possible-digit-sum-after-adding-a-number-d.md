# 加一个数字 d 后求最小可能数字和

> 原文:[https://www . geeksforgeeks . org/find-最小可能数字-相加后的总和-a-number-d/](https://www.geeksforgeeks.org/find-minimum-possible-digit-sum-after-adding-a-number-d/)

给定一个数 n 和一个数 d，我们可以把 d 加到 n 上任意多次(甚至可以是 0)。任务是找到我们通过执行上述操作可以实现的最小可能数字和。
**数字总和**被定义为一个数字的数字总和递归直到它小于 10。
**示例:**

```
Input: n = 2546, d = 124
Output: 1
2546 + 8*124 = 3538 
DigitSum(3538)=1

Input: n = 123, d = 3
Output: 3
```

**进场:**

1.  这里的第一个观察是使用%9 方法来寻找数字 n 的最小可能数字和。如果与 9 的模是 0，返回 9，否则返回余数。
2.  第二个观察结果是，a+d*(9k+l)模 9 等价于 a+d*l 模 9，因此，查询的答案将在 d 的无加法或前 8 次加法中可用，之后数字和将重复。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function To find digitsum for a number
int digitsum(int n)
{
    // Logic for digitsum
    int r = n % 9;
    if (r == 0)
        return 9;
    else
        return r;
}

// Function to find minimum digit sum
int find(int n, int d)
{
    // Variable to store answer
    // Initialise by 10 as the answer
    // will always be less than 10
    int minimum = 10;

    // Values of digitsum will repeat after
    // i=8, due to modulo taken with 9
    for (int i = 0; i < 9; i++) {
        int current = (n + i * d);
        minimum = min(minimum, digitsum(current));
    }

    return minimum;
}

// Driver Code
int main()
{
    int n = 2546, d = 124;
    cout << "Minimum possible digitsum is :"
         << find(n, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;
public class gfg
{
    // Function To find digitsum for a number
public int digitsum(int n)
{
    // Logic for digitsum
    int r = n % 9;
    if (r == 0)
        return 9;
    else
        return r;
}

// Function to find minimum digit sum
public int find(int n, int d)
{
    // Variable to store answer
    // Initialise by 10 as the answer
    // will always be less than 10
    int minimum = 10;

    // Values of digitsum will repeat after
    // i=8, due to modulo taken with 9
    for (int i = 0; i < 9; i++) {
        int current = (n + i * d);
        minimum = Math.min(minimum, digitsum(current));
    }

    return minimum;
}
}

class geek
{
// Driver Code
public static void main(String[]args)
{
    gfg g = new gfg();
    int n = 2546, d = 124;
    System.out.println("Minimum possible digitsum is : "+ (g.find(n, d)));
}
}
//This code is contributed by shs..
```

## 蟒蛇 3

```
# Python3 implementation of
# above approach

# Function To find digitsum
# for a number
def digitsum(n):

    # Logic for digitsum
    r = n % 9;
    if (r == 0):
        return 9;
    else:
        return r;

# Function to find minimum digit sum
def find(n, d):

    # Variable to store answer
    # Initialise by 10 as the answer
    # will always be less than 10
    minimum = 10;

    # Values of digitsum will
    # repeat after i=8, due to
    # modulo taken with 9
    for i in range(9):

        current = (n + i * d);
        minimum = min(minimum,
                      digitsum(current));

    return minimum;

# Driver Code
n = 2546;
d = 124;
print("Minimum possible digitsum is :",
                           find(n, d));

# This code is contributed by mits
```

## C#

```
// C# implementation of above approach
using System;
public class gfg
{
    // Function To find digitsum for a number
 public int digitsum(int n)
 {
    // Logic for digitsum
    int r = n % 9;
    if (r == 0)
        return 9;
    else
        return r;
 }

// Function to find minimum digit sum
 public int find(int n, int d)
 {
    // Variable to store answer
    // Initialise by 10 as the answer
    // will always be less than 10
    int minimum = 10;

    // Values of digitsum will repeat after
    // i=8, due to modulo taken with 9
    for (int i = 0; i < 9; i++) {
        int current = (n + i * d);
        minimum = Math.Min(minimum, digitsum(current));
    }

    return minimum;
 }
}

class geek
{
// Driver Code
 public static void Main()
 {
    gfg g = new gfg();
    int n = 2546, d = 124;
    Console.WriteLine("Minimum possible digitsum is : {0}", (g.find(n, d)));
    Console.Read();
 }
}
//This code is contributed by SoumikMondal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of
// above approach

// Function To find digitsum
// for a number
function digitsum($n)
{
    // Logic for digitsum
    $r = $n % 9;
    if ($r == 0)
        return 9;
    else
        return $r;
}

// Function to find minimum digit sum
function find($n, $d)
{
    // Variable to store answer
    // Initialise by 10 as the answer
    // will always be less than 10
    $minimum = 10;

    // Values of digitsum will
    // repeat after i=8, due to
    // modulo taken with 9
    for ($i = 0; $i < 9; $i++)
    {
        $current = ($n + $i * $d);
        $minimum = min($minimum,
                   digitsum($current));
    }

    return $minimum;
}

// Driver Code
$n = 2546; $d = 124;
echo "Minimum possible digitsum is :",
                         find($n, $d);

// This code is contributed
// by Shashank
?>
```

## java 描述语言

```
<script>

// javascript implementation of above approach
 // Function To find digitsum for a number
 function digitsum( n)
 {
    // Logic for digitsum
    var r = n % 9;
    if (r == 0)
        return 9;
    else
        return r;
 }

// Function to find minimum digit sum
 function find( n,  d)
 {
    // Variable to store answer
    // Initialise by 10 as the answer
    // will always be less than 10
    var minimum = 10;

    // Values of digitsum will repeat after
    // i=8, due to modulo taken with 9
    for (var i = 0; i < 9; i++) {
        var current = (n + i * d);
        minimum = Math.min(minimum, digitsum(current));
    }

    return minimum;
 }

 var n = 2546, d = 124;
 document.write("Minimum possible digitsum is :" + find(n, d));

</script>
```

**Output:** 

```
Minimum possible digitsum is :1
```