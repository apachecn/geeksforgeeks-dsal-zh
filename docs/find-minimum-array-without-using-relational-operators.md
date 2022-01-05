# 在不使用关系运算符的情况下查找数组中的最小值

> 原文:[https://www . geesforgeks . org/find-最小数组-不使用关系运算符/](https://www.geeksforgeeks.org/find-minimum-array-without-using-relational-operators/)

给定一个非负整数的数组 A[]，在不使用[关系运算符](https://www.geeksforgeeks.org/operators-in-c-set-2-relational-and-logical-operators/)的情况下找到数组中的最小值。
**例:**

```
Input : A[] = {2, 3, 1, 4, 5}
Output : 1

Input : A[] = {23, 17, 93}
Output : 17
```

我们用重复减法找出最小值。为了找到两个数之间的最小值，我们取一个初始化为零的变量计数器。我们不断减小这两个值，直到其中任何一个等于零，同时增加计数器。最小值首先达到零，计数器增加到两者的最小值。我们首先找到前两个数字的最小值，然后逐一与数组的其余元素进行比较，以找到整体最小值。
以下是上述思路的实现。

## C++

```
// C++ program to find minimum in an
// array without using Relational Operators
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum between two non-negative
// numbers without using relational operator.
int minimum(int x, int y)
{
    int c = 0;

    // Continues till any element becomes zero.
    while (x && y)
    {
        x--;
        y--;
        c++;
    }
    return c;
}

// Function to find minimum in an array.
int arrayMinimum(int A[], int N)
{
    // calculating minimum of first two numbers
    int mn = A[0];

    // Iterating through each of the member of
    // the array to calculate the minimum
    for (int i = N-1; i; i--)

        // Finding the minimum between current
        // minimum and current value.
        mn = minimum(mn, A[i]);   

    return mn;
}

// Driver code
int main()
{
    int A[] = { 2, 3, 1, 4 };
    int N = sizeof(A) / sizeof(A[0]);
    cout << arrayMinimum(A, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum in an
// array without using Relational Operators

class GFG {

// Function to find minimum between two
// non-negative numbers without
// using relational operator.
static int minimum(int x, int y)
{
    int c = 0;

    // Continues till any element becomes zero.
    while (x > 0 && y > 0) {
    x--;
    y--;
    c++;
    }
    return c;
}

// Function to find minimum in an array.
static int arrayMinimum(int A[], int N) {

    // calculating minimum of first two numbers
    int mn = A[0];

    // Iterating through each of the member of
    // the array to calculate the minimum
    for (int i = N - 1; i > 0; i--)

    // Finding the minimum between current
    // minimum and current value.
    mn = minimum(mn, A[i]);

    return mn;
}

// Driver code
public static void main(String arg[])
{
    int A[] = {2, 3, 1, 4};
    int N = A.length;
    System.out.print(arrayMinimum(A, N));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Function to find minimum
# between two non-negative
# numbers without using
# relational operator.

def minimum(x,y):
    c = 0

    # Continues till any
    # element becomes zero.
    while (x>0 and y>0):

        x=x-1
        y=y-1
        c=c+1

    return c

# Function to find
# minimum in an array.
def arrayMinimum(A,N):

    # calculating minimum
    # of first two numbers
    mn = A[0]

    # Iterating through each
    # of the member of
    # the array to calculate
    # the minimum
    for i in range(N-1,0,-1):

        # Finding the minimum
        # between current
        # minimum and current value.
        mn = minimum(mn, A[i])   

    return mn

# Driver code

A = [ 2, 3, 1, 4]
N =len(A)

print(arrayMinimum(A, N))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find minimum in an
// array without using Relational Operators
using System;

class GFG
{

// Function to find minimum between two
// non-negative numbers without
// using relational operator.
static int minimum(int x, int y)
{
    int c = 0;

    // Continues till any
    // element becomes zero
    while (x > 0 && y > 0)
    {
        x--;
        y--;
        c++;
    }
    return c;
}

// Function to find minimum in an array.
static int arrayMinimum(int []A, int N)
{

    // calculating minimum of
    // first two numbers
    int mn = A[0];

    // Iterating through each of the
    // member of the array to
    // calculate the minimum
    for (int i = N - 1; i > 0; i--)

        // Finding the minimum between current
        // minimum and current value.
        mn = minimum(mn, A[i]);

    return mn;
}

// Driver code
public static void Main()
{
    int []A = {2, 3, 1, 4};
    int N = A.Length;
    Console.WriteLine(arrayMinimum(A, N));
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// in an array without using
// Relational Operators

// Function to find minimum
// between two non-negative
// numbers without using
// relational operator.
function minimum($x, $y)
{
    $c = 0;

    // Continues till any
    // element becomes zero.
    while ($x and $y)
    {
        $x--;
        $y--;
        $c++;
    }
    return $c;
}

// Function to find
// minimum in an array.
function arrayMinimum( $A, $N)
{
    // calculating minimum of
    // first two numbers
    $mn = $A[0];

    // Iterating through each
    // of the member of the
    // array to calculate
    // the minimum
    for ($i = $N - 1; $i; $i--)

        // Finding the minimum
        // between current minimum
        // and current value.
        $mn = minimum($mn, $A[$i]);

    return $mn;
}

// Driver code
$A = array(2, 3, 1, 4);
$N = count($A);
echo arrayMinimum($A, $N);

// This code is contributed
// by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find minimum in an
    // array without using Relational Operators

    // Function to find minimum between two
    // non-negative numbers without
    // using relational operator.
    function minimum(x, y)
    {
        let c = 0;

        // Continues till any
        // element becomes zero
        while (x > 0 && y > 0)
        {
            x--;
            y--;
            c++;
        }
        return c;
    }

    // Function to find minimum in an array.
    function arrayMinimum(A, N)
    {

        // calculating minimum of
        // first two numbers
        let mn = A[0];

        // Iterating through each of the
        // member of the array to
        // calculate the minimum
        for (let i = N - 1; i > 0; i--)

            // Finding the minimum between current
            // minimum and current value.
            mn = minimum(mn, A[i]);

        return mn;
    }

    let A = [2, 3, 1, 4];
    let N = A.length;
    document.write(arrayMinimum(A, N));

// This code is contributed by divyesh072019.
</script>
```

**输出:**

```
1
```

代码的时间复杂度将是 O(N*max)，其中 max 是数组元素的最大值。
**限制:**只有当数组包含所有非负整数时，这才会起作用。