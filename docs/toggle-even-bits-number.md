# 切换数字的所有偶数位

> 原文:[https://www.geeksforgeeks.org/toggle-even-bits-number/](https://www.geeksforgeeks.org/toggle-even-bits-number/)

给定一个数字，任务是切换一个数字的所有偶数位
示例:

```
Input : 10
Output : 0
binary representation 1 0 1 0
after toggle          0 0 0 0 

Input : 20
Output : 30
binary representation 1 0 1 0 0
after toggle          1 1 1 1 0
```

1.首先生成一个包含偶数位置位的数字。
2。与原数进行异或运算。注意，1 ^ 1 = 0，1 ^ 0 = 1。
让我们用下面的代码来理解这种方法。

## C++

```
// CPP code to Toggle all even
// bit of a number
#include <iostream>
using namespace std;

// Returns a number which has all even
// bits of n toggled.
int evenbittogglenumber(int n)
{
    // Generate number form of 101010
    // ..till of same order as n
    int res = 0, count = 0;
    for (int temp = n; temp > 0; temp >>= 1) {

        // if bit is even then generate
        // number and or with res
        if (count % 2 == 1)
            res |= (1 << count);     

        count++;
    }

    // return toggled number
    return n ^ res;
}

// Driver code
int main()
{
    int n = 11;
    cout << evenbittogglenumber(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to Toggle all
// even bit of a number
import java.io.*;

class GFG {

    // Returns a number which has
    // all even bits of n toggled.
    static int evenbittogglenumber(int n)
    {
        // Generate number form of 101010
        // ..till of same order as n
        int res = 0, count = 0;
        for (int temp = n; temp > 0;
                               temp >>= 1)
        {
            // if bit is even then generate
            // number and or with res
            if (count % 2 == 1)
                res |= (1 << count);     

            count++;
        }

        // return toggled number
        return n ^ res;
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 11;
        System.out.println(evenbittogglenumber(n));
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python code to Toggle all
# even bit of a number

# Returns a number which has all even
# bits of n toggled.
def evenbittogglenumber(n) :

    # Generate number form of 101010
    # ..till of same order as n
    res = 0
    count = 0
    temp = n

    while (temp > 0) :

        # if bit is even then generate
        # number and or with res
        if (count % 2 == 1) :
            res = res | (1 << count)    

        count = count + 1
        temp >>= 1

    # return toggled number
    return n ^ res

# Driver code
n = 11
print(evenbittogglenumber(n))

#This code is contributed by Nikita Tiwari.
```

## C#

```
// C# code to Toggle all
// even bit of a number
using System;

class GFG {

    // Returns a number which has
    // all even bits of n toggled.
    static int evenbittogglenumber(int n)
    {
        // Generate number form of 101010
        // ..till of same order as n
        int res = 0, count = 0;

        for (int temp = n; temp > 0;
                               temp >>= 1)
        {
            // if bit is even then generate
            // number and or with res
            if (count % 2 == 1)
                res |= (1 << count);     

            count++;
        }

        // return toggled number
        return n ^ res;
    }

    // Driver code
    public static void Main()
    {

        int n = 11;

        Console.WriteLine(evenbittogglenumber(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php code to Toggle all
// even bit of a number

// Returns a number which has
// all even bits of n toggled.
function evenbittogglenumber($n)
{

    // Generate number form of 101010
    // ..till of same order as n
    $res = 0;
    $count = 0;
    for ($temp = $n; $temp > 0; $temp >>= 1)
    {

        // if bit is even then generate
        // number and or with res
        if ($count % 2 == 1)
            $res |= (1 << $count);    

        $count++;
    }

    // return toggled number
    return $n ^ $res;
}

    // Driver code
    $n = 11;
    echo evenbittogglenumber($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to Toggle all
// even bit of a number

    // Returns a number which has
    // all even bits of n toggled.
    function evenbittogglenumber(n)
    {
        // Generate number form of 101010
        // ..till of same order as n
        let res = 0, count = 0;

        for (let temp = n; temp > 0;
                               temp >>= 1)
        {
            // if bit is even then generate
            // number and or with res
            if (count % 2 == 1)
                res |= (1 << count);     

            count++;
        }

        // return toggled number
        return n ^ res;
    }

// Driver code

    let n = 11;

        document.write(evenbittogglenumber(n));

</script>
```

**输出:**

```
1
```