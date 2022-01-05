# 使用按位运算符

将任意数字乘以 4

> 原文:[https://www . geeksforgeeks . org/乘法-number-4-use-bitwise-operator/](https://www.geeksforgeeks.org/multiply-number-4-using-bitwise-operator/)

我们是一个数字 n，我们的任务是使用逐位运算符将数字乘以 4。
示例:

```
Input : 4
Output :16

Input :5
Output :20
```

**解释**情况 1:-n = 4 4 的二进制数是 100，现在向右移动两位，然后是 10000，现在数字是 16 乘以 4*4=16 ans。
**接近** :- (n < < 2)向右移动两位

## C++

```
// C++ program to multiply a number with
// 4 using Bitwise Operator
#include <bits/stdc++.h>
using namespace std;

// function the return multiply a number
//  with 4 using bitwise operator
int multiplyWith4(int n)
{
    // returning a number with multiply
    // with 4 using2 bit shifring right
    return (n << 2);
}

// derive function
int main()
{
    int n = 4;
    cout << multiplyWith4(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to multiply a number
// with 4 using Bitwise Operator

class GFG {

// function the return
// multiply a number
// with 4 using bitwise
// operator
static int multiplyWith4(int n)
{

    // returning a number
    // with multiply with
    // 4 using 2 bit shifting
    // right
    return (n << 2);
}

// Driver Code
public static void main(String[] args)
{
    int n = 4;
    System.out.print(multiplyWith4(n));
}
}

// This code is contributed by Smitha.
```

## 蟒蛇 3

```
# Python 3 program to multiply
# a number with 4 using Bitwise
# Operator

# function the return multiply
# a number with 4 using bitwise
# operator
def multiplyWith4(n):

    # returning a number with
    # multiply with 4 using2
    # bit shifring right
    return (n << 2)

# derive function
n = 4
print(multiplyWith4(n))

# This code is contributed
# by Smitha
```

## C#

```
// C# program to multiply a number
// with 4 using Bitwise Operator
using System;

class GFG {

// function the return
// multiply a number
// with 4 using bitwise
// operator
static int multiplyWith4(int n)
{

    // returning a number
    // with multiply with
    // 4 using 2 bit shifting
    // right
    return (n << 2);
}

// Driver Code
public static void Main(String[] args)
{
    int n = 4;
    Console.Write(multiplyWith4(n));
}
}

// This code is contributed by Smitha.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to multiply
// a number with 4 using
// Bitwise Operator

// function the return
// multiply a number
// with 4 using bitwise
// operator
function multiplyWith4($n)
{

    // returning a number
    // with multiply with
    // 4 using2 bit
    // shifting right
    return ($n << 2);
}

    // Driver Code
    $n = 4;
    echo multiplyWith4($n),"\n";

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// javascript program to multiply a number
// with 4 using Bitwise Operator  
// function the return
// multiply a number
// with 4 using bitwise
// operator
function multiplyWith4(n)
{

    // returning a number
    // with multiply with
    // 4 using 2 bit shifting
    // right
    return (n << 2);
}

// Driver Code
var n = 4;
document.write(multiplyWith4(n));

// This code is contributed by Amit Katiyar
</script>
```

输出:-

```
16
```

**推广:**一般来说，我们可以使用按位运算符乘以 2 的幂。例如，假设我们希望与 16 相乘(这是 2 <sup>4</sup> ，我们可以通过向左移动 4 来实现。