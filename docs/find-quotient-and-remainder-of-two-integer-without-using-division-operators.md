# 不使用除法运算符求两个整数的商和余数

> 原文:[https://www . geeksforgeeks . org/find-不使用除法运算符的二进制整数商和余数/](https://www.geeksforgeeks.org/find-quotient-and-remainder-of-two-integer-without-using-division-operators/)

给定**两个正整数被除数和除数**，我们的任务是求商和余数。不允许使用除法或 mod 运算符。

**示例:**

> **输入:**被除数= 10，除数= 3
> **输出:** 3，1
> **说明:**
> 10 除以 3 的商是 3，余数是 1。
> 
> **输入:**被除数= 11，除数= 5
> **输出:** 2，1
> **说明:**
> 11 除以 5 的商是 2，余数是 1。

**方法:**
为了解决上面提到的问题，我们将使用二分搜索法技术。我们可以在 1 到 N 的范围内实现搜索方法，其中 N 是被除数。这里我们将使用乘法来决定范围。一旦我们打破了二分搜索法的 while 循环，我们就得到商，余数可以用乘法和减法算符求出。处理特殊情况，当被除数小于或等于除数时，不使用二分搜索法。

下面是上述方法的实现:

## C++

```
// C++ implementation to Find Quotient
// and Remainder of two integer without
// using / and % operator using Binary search

#include <bits/stdc++.h>
using namespace std;

// Function to the quotient and remainder
pair<int, int> find(int dividend, int divisor,
                    int start, int end)
{

    // Check if start is greater than the end
    if (start > end)
        return { 0, dividend };

    // Calculate mid
    int mid = start + (end - start) / 2;

    int n = dividend - divisor * mid;

    // Check if n is greater than divisor
    // then increment the mid by 1
    if (n > divisor)
        start = mid + 1;

    // Check if n is less than 0
    // then decrement the mid by 1
    else if (n < 0)
        end = mid - 1;

    else {
        // Check if n equals to divisor
        if (n == divisor) {
            ++mid;
            n = 0;
        }

        // Return the final answer
        return { mid, n };
    }

    // Recursive calls
    return find(dividend, divisor, start, end);
}

pair<int, int> divide(int dividend, int divisor)
{
    return find(dividend, divisor, 1, dividend);
}

// Driver code
int main(int argc, char* argv[])
{
    int dividend = 10, divisor = 3;

    pair<int, int> ans;

    ans = divide(dividend, divisor);

    cout << ans.first << ", ";
    cout << ans.second << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA implementation to Find Quotient
// and Remainder of two integer without
// using / and % operator using Binary search

class GFG{

// Function to the quotient and remainder
static int[] find(int dividend, int divisor,
                    int start, int end)
{

    // Check if start is greater than the end
    if (start > end)
        return new int[] { 0, dividend };

    // Calculate mid
    int mid = start + (end - start) / 2;

    int n = dividend - divisor * mid;

    // Check if n is greater than divisor
    // then increment the mid by 1
    if (n > divisor)
        start = mid + 1;

    // Check if n is less than 0
    // then decrement the mid by 1
    else if (n < 0)
        end = mid - 1;

    else {
        // Check if n equals to divisor
        if (n == divisor) {
            ++mid;
            n = 0;
        }

        // Return the final answer
        return new int[] { mid, n };
    }

    // Recursive calls
    return find(dividend, divisor, start, end);
}

static int[]  divide(int dividend, int divisor)
{
    return find(dividend, divisor, 1, dividend);
}

// Driver code
public static void main(String[] args)
{
    int dividend = 10, divisor = 3;

    int []ans = divide(dividend, divisor);

    System.out.print(ans[0]+ ", ");
    System.out.print(ans[1] +"\n");

}
}

// This code contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to Find Quotient
# and Remainder of two integer without
# using / and % operator using Binary search

# Function to the quotient and remainder
def find(dividend, divisor,  start,  end) :

    # Check if start is greater than the end
    if (start > end) :
        return ( 0, dividend );

    # Calculate mid
    mid = start + (end - start) // 2;

    n = dividend - divisor * mid;

    # Check if n is greater than divisor
    # then increment the mid by 1
    if (n > divisor) :
        start = mid + 1;

    # Check if n is less than 0
    # then decrement the mid by 1
    elif (n < 0) :
        end = mid - 1;

    else :
        # Check if n equals to divisor
        if (n == divisor) :
            mid += 1;
            n = 0;

        # Return the final answer
        return ( mid, n );

    # Recursive calls
    return find(dividend, divisor, start, end);

def divide(dividend, divisor) :

    return find(dividend, divisor, 1, dividend);

# Driver code
if __name__ == "__main__" :

    dividend = 10; divisor = 3;

    ans = divide(dividend, divisor);

    print(ans[0],", ",ans[1])

# This code is contributed by Yash_R
```

## C#

```
// C# implementation to Find Quotient
// and Remainder of two integer without
// using / and % operator using Binary search

using System;

public class GFG{

// Function to the quotient and remainder
static int[] find(int dividend, int divisor,
                    int start, int end)
{

    // Check if start is greater than the end
    if (start > end)
        return new int[] { 0, dividend };

    // Calculate mid
    int mid = start + (end - start) / 2;

    int n = dividend - divisor * mid;

    // Check if n is greater than divisor
    // then increment the mid by 1
    if (n > divisor)
        start = mid + 1;

    // Check if n is less than 0
    // then decrement the mid by 1
    else if (n < 0)
        end = mid - 1;

    else {
        // Check if n equals to divisor
        if (n == divisor) {
            ++mid;
            n = 0;
        }

        // Return the readonly answer
        return new int[] { mid, n };
    }

    // Recursive calls
    return find(dividend, divisor, start, end);
}

static int[]  divide(int dividend, int divisor)
{
    return find(dividend, divisor, 1, dividend);
}

// Driver code
public static void Main(String[] args)
{
    int dividend = 10, divisor = 3;

    int []ans = divide(dividend, divisor);

    Console.Write(ans[0]+ ", ");
    Console.Write(ans[1] +"\n");

}
}
// This code contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation to Find Quotient
// and Remainder of two integer without
// using / and % operator using Binary search

// Function to the quotient and remainder
function find(dividend, divisor, start, end)
{

    // Check if start is greater than the end
    if (start > end)
        return [0, dividend];

    // Calculate mid
    var mid = start + parseInt((end - start) / 2);

    var n = dividend - divisor * mid;

    // Check if n is greater than divisor
    // then increment the mid by 1
    if (n > divisor)
        start = mid + 1;

    // Check if n is less than 0
    // then decrement the mid by 1
    else if (n < 0)
        end = mid - 1;

    else
    {

        // Check if n equals to divisor
        if (n == divisor)
        {
            ++mid;
            n = 0;
        }

        // Return the final answer
        return [ mid, n];
    }

    // Recursive calls
    return find(dividend, divisor, start, end);
}

function divide(dividend, divisor)
{
    return find(dividend, divisor, 1, dividend);
}

// Driver code
var dividend = 10, divisor = 3;
var ans = divide(dividend, divisor);

document.write(ans[0] + ", ");
document.write(ans[1] + "\n");

// This code is contributed by gauravrajput1

</script>
```

**Output:** 

```
3, 1
```

**时间复杂度:**O(logN)
T3】空间复杂度: O(n)
**类似文章:** [除两个整数不使用乘除和 mod 运算符](https://www.geeksforgeeks.org/divide-two-integers-without-using-multiplication-division-mod-operator/)