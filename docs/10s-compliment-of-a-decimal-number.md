# 十进制数的 10 的补码

> 原文:[https://www . geeksforgeeks . org/10s-十进制数字补语/](https://www.geeksforgeeks.org/10s-compliment-of-a-decimal-number/)

给定一个十进制数 n .任务是找出数 n 的 10 的补码.
**例:**

```
Input : 25
Output : 10's complement is : 75

Input : 456
Output : 10's complement is : 544
```

十进制数的 10 补码可以通过在该十进制数的 9 补码[上加 1 得到。它就像二进制数表示中的 2s 补码。
数学上，](https://www.geeksforgeeks.org/9s-complement-decimal-number/) 

> **10 的补码= 9 的补码+ 1**

例如，让我们取一个十进制数 456，这个数的 9 的补码是 999-456，也就是 543。现在 10s 补码将是 543+1=544。
因此，

> **10 的补码= 10<sup>len</sup>–num**T4】
> 
> ```
> Where, len = total number of digits in num.
> ```

下面是寻找给定数字的 10 补码的程序:

## C++

```
// C++ program to find 10's complement

#include<iostream>
#include<cmath>

using namespace std;

// Function to find 10's complement
int complement(int num)
{
    int i,len=0,temp,comp;

    // Calculating total digits
    // in num
    temp = num;
    while(1)
    {
        len++;
        num=num/10;
        if(abs(num)==0)
            break;       
    }

    // restore num
    num = temp;

    // calculate 10's complement
    comp = pow(10,len) - num;

    return comp;
}

// Driver code
int main()
{
    cout<<complement(25)<<endl;

    cout<<complement(456);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find 10's complement
import java.io.*;

class GFG
{
// Function to find 10's complement
static int complement(int num)
{
    int i, len = 0, temp, comp;

    // Calculating total
    // digits in num
    temp = num;
    while(true)
    {
        len++;
        num = num / 10;
        if(Math.abs(num) == 0)
            break;
    }

    // restore num
    num = temp;

    // calculate 10's complement
    comp = (int)Math.pow(10,len) - num;

    return comp;
}

// Driver code
public static void main (String[] args)
{
    System.out.println(complement(25));

    System.out.println(complement(456));
}
}

// This code is contributed
// by chandan_jnu.
```

## 蟒蛇 3

```
# Python3 program to find
# 10's complement
import math

# Function to find 10's complement
def complement(num):
    i = 0;
    len = 0;
    comp = 0;

    # Calculating total
    # digits in num
    temp = num;
    while(1):
        len += 1;
        num = int(num / 10);
        if(abs(num) == 0):
            break;

    # restore num
    num = temp;

    # calculate 10's complement
    comp = math.pow(10, len) - num;

    return int(comp);

# Driver code
print(complement(25));
print(complement(456));

# This code is contributed by mits
```

## C#

```
// C# program to find
// 10's complement
using System;

class GFG
{
// Function to find 10's complement
static int complement(int num)
{
    int len = 0, temp, comp;

    // Calculating total
    // digits in num
    temp = num;
    while(true)
    {
        len++;
        num = num / 10;
        if(Math.Abs(num) == 0)
            break;
    }

    // restore num
    num = temp;

    // calculate 10's complement
    comp = (int)Math.Pow(10, len) - num;

    return comp;
}

// Driver code
public static void Main ()
{
    Console.WriteLine(complement(25));

    Console.WriteLine(complement(456));
}
}

// This code is contributed
// by chandan_jnu.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find 10's complement

// Function to find 10's complement
function complement($num)
{
    $i;
    $len = 0;
    $comp;

    // Calculating total
    // digits in num
    $temp = $num;
    while(1)
    {
        $len++;
        $num = (int)($num / 10);
        if(abs($num) == 0)
            break;
    }

    // restore num
    $num = $temp;

    // calculate 10's complement
    $comp = pow(10, $len) - $num;

    return $comp;
}

// Driver code
echo complement(25) . "\n";
echo complement(456);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to find 10's complement
    // Function to find 10's complement
    function complement(num) {
        var i, len = 0, temp, comp;

        // Calculating total
        // digits in num
        temp = num;
        while (true) {
            len++;
            num = parseInt(num / 10);
            if (Math.abs(num) == 0)
                break;
        }

        // restore num
        num = temp;

        // calculate 10's complement
        comp = parseInt( Math.pow(10, len) - num);

        return comp;
    }

    // Driver code

        document.write(complement(25)+"<br/>");

        document.write(complement(456));

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
75
544
```