# 使用递归的 2 个数的乘积|集合 2

> 原文:[https://www . geesforgeks . org/2-numbers 乘积-使用递归-set-2/](https://www.geeksforgeeks.org/product-of-2-numbers-using-recursion-set-2/)

给定两个数字 N 和 m，任务是用递归求这两个数字的乘积。
**注**:数字可以是正数，也可以是负数。

**示例**:

```
Input : N = 5 ,  M = 3
Output : 15

Input : N = 5  ,  M = -3
Output : -15

Input : N = -5  ,  M = 3
Output : -15

Input : N = -5  ,  M = -3
Output:15
```

只有正数的上述问题的递归解决方案已经在[上一篇文章](https://www.geeksforgeeks.org/product-2-numbers-using-recursion/)中讨论过。在这篇文章中，讨论了求正数和负数乘积的递归解法。

下面是一步一步的方法:

1.  检查一个或两个数字是否为负数。
2.  如果在第二个参数中传递的数字是负数，交换参数并再次调用函数。
3.  如果两个参数都是负数，则再次调用该函数，并将数字的绝对值作为参数传递。
4.  如果 n>m，调用带有交换参数的函数，以减少函数的执行时间。
5.  只要 m 不为 0，就继续用子基 n，m-1 调用函数，并返回 n+multi recury(n，m-1)。

下面是上述方法的实现:

## C++

```
// C++ program to find product of two numbers
// using recursion
#include <iostream>
using namespace std;

// Recursive function to calculate the product
// of 2 integers
int multrecur(int n, int m)
{
    // case 1 : n<0 and m>0
    // swap the position of n and m to keep second
    // parameter positive
    if (n > 0 && m < 0) {
        return multrecur(m, n);
    }
    // case 2 : both n and m are less than 0
    // return the product of their absolute values
    else if (n < 0 && m < 0) {
        return multrecur((-1 * n), (-1 * m));
    }

    // if n>m , swap n and m so that recursion
    // takes less time
    if (n > m) {
        return multrecur(m, n);
    }

    // as long as m is not 0 recursively call multrecur for 
    // n and m-1 return sum of n and the product of n times m-1
    else if (m != 0) {
        return n + multrecur(n, m - 1);
    }

    // m=0 then return 0
    else {
        return 0;
    }
}
// Driver code
int main()
{
    cout << "5 * 3 = " << multrecur(5, 3) << endl;
    cout << "5 * (-3) = " << multrecur(5, -3) << endl;
    cout << "(-5) * 3 = " << multrecur(-5, 3) << endl;
    cout << "(-5) * (-3) = " << multrecur(-5, -3) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to find product of two numbers
//using recursion
public class GFG {

    //Recursive function to calculate the product
    //of 2 integers
    static int multrecur(int n, int m)
    {
    // case 1 : n<0 and m>0
    // swap the position of n and m to keep second
    // parameter positive
    if (n > 0 && m < 0) {
        return multrecur(m, n);
    }
    // case 2 : both n and m are less than 0
    // return the product of their absolute values
    else if (n < 0 && m < 0) {
        return multrecur((-1 * n), (-1 * m));
    }

    // if n>m , swap n and m so that recursion
    // takes less time
    if (n > m) {
        return multrecur(m, n);
    }

    // as long as m is not 0 recursively call multrecur for 
    // n and m-1 return sum of n and the product of n times m-1
    else if (m != 0) {
        return n + multrecur(n, m - 1);
    }

    // m=0 then return 0
    else {
        return 0;
    }
    }

    //Driver code
    public static void main(String[] args) {

        System.out.println("5 * 3 = " + multrecur(5, 3));
        System.out.println("5 * (-3) = " + multrecur(5, -3));
        System.out.println("(-5) * 3 = " + multrecur(-5, 3));
        System.out.println("(-5) * (-3) = " +multrecur(-5, -3));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find product of two numbers
# using recursion

# Recursive function to calculate the product
# of 2 integers
def multrecur(n, m) :

    # case 1 : n<0 and m>0
    # swap the position of n and m to keep second
    # parameter positive
    if n > 0 and m < 0 :
        return multrecur(m,n)

    # case 2 : both n and m are less than 0
    # return the product of their absolute values
    elif n < 0 and m < 0 :
        return multrecur((-1 * n),(-1 * m))

    # if n>m , swap n and m so that recursion
    # takes less time
    if n > m :
        return multrecur(m, n)

    # as long as m is not 0 recursively call multrecur for 
    # n and m-1 return sum of n and the product of n times m-1
    elif m != 0 :
        return n + multrecur(n, m-1)

    # m=0 then return 0
    else :
        return 0

# Driver Code
if __name__ == "__main__" :

    print("5 * 3 =",multrecur(5, 3))
    print("5 * (-3) =",multrecur(5, -3))
    print("(-5) * 3 =",multrecur(-5, 3))
    print("(-5) * (-3) =",multrecur(-5, -3))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find product of
// two numbers using recursion
using System;
class GFG
{

// Recursive function to calculate
// the product of 2 integers
static int multrecur(int n, int m)
{
// case 1 : n<0 and m>0
// swap the position of n and m
// to keep second parameter positive
if (n > 0 && m < 0)
{
    return multrecur(m, n);
}

// case 2 : both n and m are less than 0
// return the product of their absolute values
else if (n < 0 && m < 0)
{
    return multrecur((-1 * n), (-1 * m));
}

// if n>m , swap n and m so that
// recursion takes less time
if (n > m)
{
    return multrecur(m, n);
}

// as long as m is not 0 recursively
// call multrecur for n and m-1 return
// sum of n and the product of n times m-1
else if (m != 0)
{
    return n + multrecur(n, m - 1);
}

// m=0 then return 0
else
{
    return 0;
}
}

// Driver code
public static void Main()
{
    Console.WriteLine("5 * 3 = " +
                       multrecur(5, 3));
    Console.WriteLine("5 * (-3) = " +
                       multrecur(5, -3));
    Console.WriteLine("(-5) * 3 = " +
                      multrecur(-5, 3));
    Console.WriteLine("(-5) * (-3) = " +
                      multrecur(-5, -3));
}
}

// This code is contributed by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find product of
// two numbers using recursion

// Recursive function to calculate
// the product of 2 integers
function multrecur($n, $m)
{
    // case 1 : n<0 and m>0
    // swap the position of n and m to keep second
    // parameter positive
    if ($n > 0 && $m < 0)
    {
        return multrecur($m, $n);
    }

    // case 2 : both n and m are less than 0
    // return the product of their absolute values
    else if ($n < 0 && $m < 0)
    {
        return multrecur((-1 * $n),
                        (-1 * $m));
    }

    // if n>m , swap n and m so that
    // recursion takes less time
    if ($n > $m)
    {
        return multrecur($m, $n);
    }

    // as long as m is not 0 recursively call multrecur for 
    // n and m-1 return sum of n and the product of n times m-1
    else if ($m != 0)
    {
        return $n + multrecur($n, $m - 1);
    }

    // m=0 then return 0
    else
    {
        return 0;
    }
}

// Driver code
echo "5 * 3 = " . multrecur(5, 3) . "\n";
echo "5 * (-3) = " . multrecur(5, -3) . "\n";
echo "(-5) * 3 = " . multrecur(-5, 3) . "\n";
echo "(-5) * (-3) = " . multrecur(-5, -3) . "\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find product
// of two numbers using recursion

// Recursive function to calculate the
// product of 2 integers
function multrecur(n, m)
{

    // case 1 : n<0 and m>0
    // Swap the position of n and m to
    // keep second parameter positive
    if (n > 0 && m < 0)
    {
        return multrecur(m, n);
    }

    // case 2 : both n and m are less than 0
    // return the product of their absolute values
    else if (n < 0 && m < 0)
    {
        return multrecur((-1 * n), (-1 * m));
    }

    // If n>m , swap n and m so that recursion
    // takes less time
    if (n > m)
    {
        return multrecur(m, n);
    }

    // As long as m is not 0 recursively
    // call multrecur for n and m-1
    // return sum of n and the product
    // of n times m-1
    else if (m != 0)
    {
        return n + multrecur(n, m - 1);
    }

    // m=0 then return 0
    else
    {
        return 0;
    }
}

// Driver code
document.write("5 * 3 = " + multrecur(5, 3) + "<br>");
document.write("5 * (-3) = " + multrecur(5, -3) + "<br>");
document.write("(-5) * 3 = " + multrecur(-5, 3) + "<br>");
document.write("(-5) * (-3) = " + multrecur(-5, -3) + "<br>");

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
5 * 3 = 15
5 * (-3) = -15
(-5) * 3 = -15
(-5) * (-3) = 15
```

**时间复杂度:** O(max(N，M))
**辅助空间:** O(max(N，M))