# 检查给定范围内所有数字的异或是偶数还是奇数

> 原文:[https://www . geesforgeks . org/check-给定范围内所有数字的异或是偶数还是奇数/](https://www.geeksforgeeks.org/check-whether-xor-of-all-numbers-in-a-given-range-is-even-or-odd/)

给定一个范围[ L，R ]，任务是找出范围 L 到 R(包括两者)内所有自然数的异或值是偶数还是奇数。如果范围内所有数字的异或为偶数，则打印“偶数”，否则打印奇数。
**例:**

```
Input: L = 1, R= 10 
Output: Odd

Input: L= 5, R=15
Output: Even
```

一个**简单的解决方案**是计算范围【L，R】内所有数字的异或，然后检查结果异或值是偶数还是奇数。
这种方法的时间复杂度为 O(n)。
一种**高效解决方案**基于以下事实:

```
odd ^ odd = even
odd ^ even = odd
even ^ odd = odd
even ^ even = even
```

所有偶数的异或将是偶数(与范围大小无关)，如果奇数的计数是奇数，那么最终的异或将是奇数，如果是偶数，那么最终的异或将是偶数。
现在可以得出结论，

> *   If the count of odd numbers is even,
>     XOR of all odd numbers = even numbers
>     XOR of all even numbers = even numbers
>     Final XOR = even numbers even numbers = even numbers
> *   If the count of odd numbers is odd,
>     XOR of all odd numbers = odd numbers
>     XOR of all even numbers = even numbers
>     Final xor = odd numbers even numbers = odd numbers.

因此，我们所要做的就是计算 L 到 r 范围内的奇数。
**方法:**

*   计算范围[ L，R ]内的奇数。
*   检查奇数的计数是偶数还是奇数。
*   如果计数为偶数，则打印“偶数”，否则打印“奇数”。

以下是上述方法的实现:

## C++

```
// C++ program to check if XOR of
// all numbers in range [L, R]
// is Even or odd

#include <bits/stdc++.h>
using namespace std;

// Function to check if XOR of all numbers
// in range [L, R] is Even or Odd

string isEvenOrOdd(int L, int R)
{
    // Count odd Numbers in range [L, R]
    int oddCount = (R - L) / 2;

    if (R % 2 == 1 || L % 2 == 1)
        oddCount++;

    // Check if count of odd Numbers
    // is even or odd

    if (oddCount % 2 == 0)
        return "Even";
    else
        return "Odd";
}

// Driver Code
int main()
{

    int L = 5, R = 15;

    cout << isEvenOrOdd(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if XOR of
// all numbers in range [L, R]
// is Even or odd

class GFG {

    // Function to check if XOR of all numbers
    // in range [L, R] is Even or Odd

    static String isEvenOrOdd(int L, int R)
    {
        // Count odd Numbers in range [L, R]
        int oddCount = (R - L) / 2;

        if (R % 2 == 1 || L % 2 == 1)
            oddCount++;

        // Check if count of odd Numbers
        // is even or odd

        if (oddCount % 2 == 0)
            return "Even";
        else
            return "Odd";
    }

    // Driver Code
    public static void main(String[] args)
    {

        int L = 5, R = 15;

        System.out.println(isEvenOrOdd(L, R));
    }
}
```

## C#

```
// C# program to check if XOR of
// all numbers in range [L, R]
// is Even or odd

using System;
class GFG {

    // Function to check if XOR of all numbers
    // in range [L, R] is Even or Odd

    static string isEvenOrOdd(int L, int R)
    {
        // Count odd Numbers in range [L, R]
        int oddCount = (R - L) / 2;

        if (R % 2 == 1 || L % 2 == 1)
            oddCount++;

        // Check if count of odd Numbers
        // is even or odd

        if (oddCount % 2 == 0)
            return "Even";
        else
            return "Odd";
    }

    // Driver Code
    public static void Main()
    {

        int L = 5, R = 15;

        Console.WriteLine(isEvenOrOdd(L, R));
    }
}
```

## 蟒蛇 3

```
# Python3 program to check if XOR of
# all numbers in range [L, R]
# is Even or odd

# Function to check if XOR of all numbers
# in range [L, R] is Even or Odd

def isEvenOrOdd( L, R ):

    # Count odd Numbers in range [L, R]
    oddCount = (R - L )/2

    if( R % 2 == 1 or L % 2 == 1):
        oddCount = oddCount + 1

    # Check if count of odd Numbers
    # is even or odd

    if(oddCount % 2 == 0 ):
        return "Even"
    else :
        return "Odd"

# Driver Code

L = 5
R = 15

print(isEvenOrOdd(L, R));
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if XOR of all
// numbers in range [L, R] is Even or odd

// Function to check if XOR of all numbers
// in range [L, R] is Even or Odd
function isEvenOrOdd($L, $R)
{
    // Count odd Numbers in range [L, R]
    $oddCount = floor(($R - $L) / 2);

    if ($R % 2 == 1 || $L % 2 == 1)
        $oddCount++;

    // Check if count of odd Numbers
    // is even or odd
    if ($oddCount % 2 == 0)
        return "Even";
    else
        return "Odd";
}

// Driver Code
$L = 5;
$R = 15;

echo isEvenOrOdd($L, $R);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// JavaScript program to check if XOR of
// all numbers in range [L, R]
// is Even or odd

// Function to check if XOR of all numbers
// in range [L, R] is Even or Odd

function isEvenOrOdd(L, R)
{
    // Count odd Numbers in range [L, R]
    let oddCount = Math.floor((R - L) / 2);

    if (R % 2 == 1 || L % 2 == 1)
        oddCount++;

    // Check if count of odd Numbers
    // is even or odd

    if (oddCount % 2 == 0)
        return "Even";
    else
        return "Odd";
}

// Driver Code

    let L = 5, R = 15;

    document.write(isEvenOrOdd(L, R));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
Even
```

时间复杂度:O(1)
辅助空间:O(1)