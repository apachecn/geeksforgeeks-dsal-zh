# 切换数字的所有奇数位

> 原文:[https://www.geeksforgeeks.org/toggle-odd-bits-number/](https://www.geeksforgeeks.org/toggle-odd-bits-number/)

给定 n 个数字，任务是切换数字的奇数位。
示例:

```
Input : 10
Output : 15
binary representation 1 0 1 0
after toggle          1 1 1 1 

Input : 20
Output : 1
binary representation 1 0 1 0 0
after toggle          0 0 0 0 1
```

1.首先生成一个包含奇数位的数字。
2。与原数进行异或运算。注意，1 ^ 1 = 0，1 ^ 0 = 1。
让我们用下面的代码来理解这种方法。

## C++

```
// Toggle all odd bit of a number
#include <iostream>
using namespace std;

// Returns a number which has all odd
// bits of n toggled.
int evenbittogglenumber(int n)
{
    // Generate number form of 101010...
    // ..till of same order as n
    int res = 0, count = 0;
    for (int temp = n; temp > 0; temp >>= 1) {

        // if bit is odd, then generate
        // number and or with res
        if (count % 2 == 0)
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
// Toggle all odd bit of a number

import java.io.*;

class GFG {
    // Returns a number which has all odd
    // bits of n toggled.
    static int evenbittogglenumber(int n)
    {
        // Generate number form of 101010...
        // ..till of same order as n
        int res = 0, count = 0;
        for (int temp = n; temp > 0; temp >>= 1) {

            // if bit is odd, then generate
            // number and or with res
            if (count % 2 == 0)
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

/*This code is contributed by Nikita tiwari.*/

```

## 蟒蛇 3

```
# Python3 code for Toggle all odd bit of a number

# Returns a number which has all odd
# bits of n toggled.
def evenbittogglenumber(n) :

    # Generate number form of 101010...
    # ..till of same order as n
    res = 0; count = 0; temp = n

    while(temp > 0 ) :

        # If bit is odd, then generate
        # number and or with res
        if (count % 2 == 0) :
            res = res | (1 << count)    

        count = count + 1
        temp >>= 1

    # Return toggled number
    return n ^ res

# Driver code
if __name__ == '__main__' :

    n = 11
    print(evenbittogglenumber(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# code for Toggle all odd bit of a number
using System;

class GFG {

    // Returns a number which has all odd
    // bits of n toggled.
    static int evenbittogglenumber(int n)
    {

        // Generate number form of 101010...
        // ..till of same order as n
        int res = 0, count = 0;

        for (int temp = n; temp > 0; temp >>= 1)
        {

            // if bit is odd, then generate
            // number and or with res
            if (count % 2 == 0)
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
// php implementation of Toggle
// all odd bit of a number

// Returns a number which has
// all odd bits of n toggled.
function evenbittogglenumber($n)
{

    // Generate number form of 101010...
    // ..till of same order as n
    $res = 0;
    $count = 0;
    for ($temp = $n; $temp > 0; $temp >>= 1)
    {

        // if bit is odd, then generate
        // number and or with res
        if ($count % 2 == 0)
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

// JavaScript program Toggle all odd bit of a number

    // Returns a number which has all odd
    // bits of n toggled.
    function evenbittogglenumber(n)
    {
        // Generate number form of 101010...
        // ..till of same order as n
        let res = 0, count = 0;
        for (let temp = n; temp > 0; temp >>= 1) {

            // if bit is odd, then generate
            // number and or with res
            if (count % 2 == 0)
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
14
```