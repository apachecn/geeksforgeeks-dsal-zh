# 设置最左侧未设置位

> 原文:[https://www.geeksforgeeks.org/set-left-unset-bit/](https://www.geeksforgeeks.org/set-left-unset-bit/)

给定一个整数，设置最左边的未设置位。最左边的未设置位是最高有效设置位之后的第一个未设置位。如果所有位(最高有效设置位之后)都已设置，则返回数字。

示例:

```
Input : 10
Output : 14
10 = 1 0 1 0    // 10 binary
14 = 1 1 1 0    // after set left most unset bit

Input : 15      
Output : 15
15 = 1 1 1 1    // 15 binary
15 = 1 1 1 1    // because all bits are set
```

**进场:-**
1。如果所有位都已设置，则返回数字。
2。遍历所有位以获得最后一个未设置的位。
3。用原始数字和未设置的位取或。

下面是该方法的实现。

## C++

```
// C++ program to set the leftmost unset bit
#include <iostream>
using namespace std;

// set left most unset bit
int setleftmostunsetbit(int n)
{
    // if number contain all
    // 1 then return n
    if ((n & (n + 1)) == 0)
        return n;

    // Find position of leftmost unset bit.
    int pos = 0;
    for (int temp=n, count=0; temp>0;
                        temp>>=1, count++)

        // if temp L.S.B is zero
        // then unset bit pos is
        // change
        if ((temp & 1) == 0)
            pos = count;  

    // return OR of number and
    // unset bit pos
    return (n | (1 << (pos)));
}

// Driver Function
int main()
{
    int n = 10;
    cout << setleftmostunsetbit(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to set
// the leftmost unset bit
import java.io.*;

class GFG
{
    // set left most unset bit
    static int setleftmostunsetbit(int n)
    {
        // if number contain all
        // 1 then return n
        if ((n & (n + 1)) == 0)
            return n;

        // Find position of leftmost unset bit.
        int pos = 0;
        for (int temp = n, count = 0; temp > 0;
                           temp >>= 1, count++)

            // if temp L.S.B is zero
            // then unset bit pos is
            // change
            if ((temp & 1) == 0)
                pos = count;

        // return OR of number and
        // unset bit pos
        return (n | (1 << (pos)));
    }

    // Driver Function
    public static void main (String[] args)
    {
        int n = 10;
        System.out.println(setleftmostunsetbit(n));
    }
}

// This code is contributed by Ansu Kumari
```

## 蟒蛇 3

```
# Python program to set the leftmost unset bit

# Set left most unset bit
def setleftmostunsetbit(n):
    # if number contain all
    # 1 then return n
    if not (n & (n + 1)):
        return n

    # Find position of leftmost unset bit
    pos, temp, count = 0, n, 0

    while temp:
        # if temp L.S.B is zero
        # then unset bit pos is
        # change
        if not (temp & 1):
            pos = count

        count += 1; temp>>=1

    # return OR of number and
    # unset bit pos
    return (n | (1 << (pos)))

# Driver Function
n = 10
print(setleftmostunsetbit(n))

# This code is contributed by Ansu Kumari
```

## C#

```
// C# program to set
// the leftmost unset bit
using System;

class GFG
{
    // set left most unset bit
    static int setleftmostunsetbit(int n)
    {
        // if number contain all
        // 1 then return n
        if ((n & (n + 1)) == 0)
            return n;

        // Find position of leftmost unset bit.
        int pos = 0;
        for (int temp = n, count = 0; temp > 0;
                            temp >>= 1, count++)

            // if temp L.S.B is zero
            // then unset bit pos is
            // change
            if ((temp & 1) == 0)
                pos = count;

        // return OR of number and
        // unset bit pos
        return (n | (1 << (pos)));
    }

    // Driver Function
    public static void Main ()
    {
        int n = 10;
        Console.WriteLine(setleftmostunsetbit(n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to set the
// leftmost unset bit

// set left most unset bit
function setleftmostunsetbit($n)
{

    // if number contain all
    // 1 then return n
    if (($n & ($n + 1)) == 0)
        return $n;

    // Find position of leftmost
    // unset bit.
    $pos = 0;
    for ($temp = $n, $count = 0; $temp > 0;
                     $temp >>= 1, $count++)

        // if temp L.S.B is zero
        // then unset bit pos is
        // change
        if (($temp & 1) == 0)
            $pos = $count;

    // return OR of number
    // and unset bit pos
    return ($n | (1 << ($pos)));
}

    // Driver code
    $n = 10;
    echo setleftmostunsetbit($n);

//This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to set the
// leftmost unset bit

// Set left most unset bit
function setleftmostunsetbit(n)
{

    // If number contain all
    // 1 then return n
    if ((n & (n + 1)) == 0)
        return n;

    // Find position of leftmost unset bit.
    let pos = 0;
    for(let temp = n, count = 0; temp > 0;
            temp >>= 1, count++)

        // If temp L.S.B is zero
        // then unset bit pos is
        // change
        if ((temp & 1) == 0)
            pos = count;

    // Return OR of number and
    // unset bit pos
    return (n | (1 << (pos)));
}

// Driver Code
let n = 10;

document.write(setleftmostunsetbit(n));

// This code is contributed by Manoj.

</script>
```

**输出:**

```
14
```