# 如何打开数字中的特定位？

> 原文:[https://www.geeksforgeeks.org/turn-particular-bit-number-2/](https://www.geeksforgeeks.org/turn-particular-bit-number-2/)

给定一个数字 n 和值 k，打开 n 中的第 k 位
示例:

```
Input:  n = 4, k = 2
Output: 6

Input:  n = 3, k = 3
Output: 7

Input:  n = 64, k = 4
Output: 72

Input:  n = 64, k = 5
Output: 80
```

思路是用按位<< and | operators. Using expression “(1 << (k – 1))“, we get a number which has all bits unset, except the k’th bit. If we do bitwise | of this expression with n, we get a number which has all bits same as n except the k’th bit which is 1.
下面是上面思路的实现。

## C++

```
// CPP program to turn on a particular bit
#include <iostream>
using namespace std;

// Returns a number that has all bits same as n
// except the k'th bit which is made 1
int turnOnK(int n, int k)
{
    // k must be greater than 0
    if (k <= 0)
        return n;

    // Do | of n with a number with all
    // unset bits except the k'th bit
    return (n | (1 << (k - 1)));
}

// Driver program to test above function
int main()
{
    int n = 4;
    int k = 2;
    cout << turnOnK(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to turn on a particular
// bit
class GFG {

    // Returns a number that has all
    // bits same as n except the k'th
    // bit which is made 1
    static int turnOnK(int n, int k)
    {

        // k must be greater than 0
        if (k <= 0)
            return n;

        // Do | of n with a number with
        // all unset bits except the
        // k'th bit
        return (n | (1 << (k - 1)));
    }

    // Driver program to test above
    // function
    public static void main(String [] args)
    {
        int n = 4;
        int k = 2;
        System.out.print(turnOnK(n, k));
    }
}

// This code is contributed by Smitha
```

## 蟒蛇 3

```
# Python 3 program to turn on a
# particular bit

# Returns a number that has all
# bits same as n except the k'th
# bit which is made 1
def turnOnK(n, k):

    # k must be greater than 0
    if (k <= 0):
        return n

    # Do | of n with a number
    # with all unset bits except
    # the k'th bit
    return (n | (1 << (k - 1)))

# Driver program to test above
# function
n = 4
k = 2
print(turnOnK(n, k))

# This code is contributed by
# Smitha
```

## C#

```
// C# program to turn on a particular
// bit
using System;

class GFG {

    // Returns a number that has all
    // bits same as n except the k'th
    // bit which is made 1
    static int turnOnK(int n, int k)
    {

        // k must be greater than 0
        if (k <= 0)
            return n;

        // Do | of n with a number
        // with all unset bits except
        // the k'th bit
        return (n | (1 << (k - 1)));
    }

    // Driver program to test above
    // function
    public static void Main()
    {
        int n = 4;
        int k = 2;
        Console.Write(turnOnK(n, k));
    }
}

// This code is contributed by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to turn on a particular bit

// Returns a number that has
// all bits same as n except
// the k'th bit which is made 1
function turnOnK($n, $k)
{

    // k must be greater than 0
    if ($k <= 0)
        return $n;

    // Do | of n with a number with all
    // unset bits except the k'th bit
    return ($n | (1 << ($k - 1)));
}

    // Driver Code
    $n = 4;
    $k = 2;
    echo turnOnK($n, $k);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>
    // Javascript program to turn on a particular bit

    // Returns a number that has all
    // bits same as n except the k'th
    // bit which is made 1
    function turnOnK(n, k)
    {

        // k must be greater than 0
        if (k <= 0)
            return n;

        // Do | of n with a number
        // with all unset bits except
        // the k'th bit
        return (n | (1 << (k - 1)));
    }

    let n = 4;
    let k = 2;
    document.write(turnOnK(n, k));

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
6
```