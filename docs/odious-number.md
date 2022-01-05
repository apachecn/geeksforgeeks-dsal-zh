# 恶号

> 原文:[https://www.geeksforgeeks.org/odious-number/](https://www.geeksforgeeks.org/odious-number/)

[恶数](https://en.wikipedia.org/wiki/Odious_number)是一个非负数，其二进制展开式中有奇数个 1。因此，前几个令人讨厌的数字是 1、2、4、7、8、11、13、14、16、19……
给定一个数字，检查它是否是令人讨厌的数字。
**示例:**

```
Input : 16
Output : Odious Number
Explanation: Binary expansion of 16 = 10000, 
having number of 1s =1 i.e odd.

Input : 23
Output :  Not odious number
Explanation: Binary expansion of 23 is 10111,
the number of 1s in this is 4 i.e even. 
```

1) [以给定数量](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)计数设定位。
2)如果计数为奇数，则返回真，否则返回假。

## C++

```
// C/C++ program to check if a number is
// Odious Number or not
#include <iostream>
using namespace std;
#include <math.h>

/* Function to get no of set bits in binary
   representation of passed binary no.
   Please refer below for details of this
   function :
   https://www.geeksforgeeks.org/count-set-bits-in-an-integer/ */
int countSetBits(int n)
{
    unsigned int count = 0;
    while (n)
    {
      n &= (n-1) ;
      count++;
    }
    return count;
}

// Check if number is odious or not
int checkOdious(int n)
{
    return (countSetBits(n) % 2 == 1);
}

// Driver Code
int main()
{
    int num = 32;
    if (checkOdious(num))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number is
// Odious Number or not
import java.io.*;
import java.math.*;

class GFG {

    /* Function to get no of set bits in binary
       representation of passed binary no.
       Please refer below for details of this
       function :
       https://www.geeksforgeeks.org/count-set-bits-in-an-integer/ */
    static int countSetBits(int n)
    {
        int count = 0;
        while (n!=0)
        {
          n &= (n-1) ;
          count++;
        }
        return count;
    }

    // Check if number is odious or not
    static boolean checkOdious(int n)
    {
        return (countSetBits(n) % 2 == 1);
    }

    // Driver Code
    public static void main(String args[])
    {
        int num = 32;
        if (checkOdious(num))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program to check if a number is
# Odious Number or not

# Function to get no of set bits in binary
# representation of passed binary no.
# Please refer below for details of this function :
# https://www.geeksforgeeks.org/count-set-bits-in-an-integer
def countSetBits(n) :
    count = 0

    while (n) :
        n = n & (n-1)
        count = count + 1

    return count

# Check if number is odious or not
def checkOdious(n) :
    return (countSetBits(n) % 2 == 1)

# Driver Code
num = 32

if (checkOdious(num)) :
    print("Yes")
else :
    print("No")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to check if a number
// is Odious Number or not
using System;

class GFG {

    /* Function to get no of set bits in
    binary representation of passed binary
    no. Please refer below for details
    of this function :
    https://www.geeksforgeeks.org/count-set-bits-in-an-integer/ */
    static int countSetBits(int n)
    {
        int count = 0;
        while (n != 0)
        {
        n &= (n - 1) ;
        count++;
        }

        return count;
    }

    // Check if number is odious or not
    static bool checkOdious(int n)
    {
        return (countSetBits(n) % 2 == 1);
    }

    // Driver Code
    public static void Main()
    {
        int num = 32;
        if (checkOdious(num))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a number
// is Odious Number or not

// Function to get no of
// set bits in binary
function countSetBits($n)
{
    $count = 0;
    while ($n)
    {
        $n &= ($n - 1) ;
        $count++;
    }
    return $count;
}

// Check if number is odious or not
function checkOdious($n)
{
    return (countSetBits($n) % 2 == 1);
}

// Driver Code
$num = 32;
if (checkOdious($num))
    echo "Yes";
else
    echo "No";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to check if a number is
// Odious Number or not

    /* Function to get no of set bits in binary
       representation of passed binary no.
       Please refer below for details of this
       function :
       https://www.geeksforgeeks.org/count-set-bits-in-an-integer/ */
    function countSetBits(n)
    {
        let count = 0;
        while (n!=0)
        {
          n &= (n-1) ;
          count++;
        }
        return count;
    }

    // Check if number is odious or not
    function checkOdious(n)
    {
        return (countSetBits(n) % 2 == 1);
    }

// Driver code

        let num = 32;
        if (checkOdious(num))
            document.write("Yes");
        else
            document.write("No");

</script>
```

**输出:**

```
Yes
```