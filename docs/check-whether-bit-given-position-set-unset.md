# 检查给定位置的位是置位还是未置位

> 原文:[https://www . geesforgeks . org/check-what-bit-given-position-set-unset/](https://www.geeksforgeeks.org/check-whether-bit-given-position-set-unset/)

给定两个正整数 **n** 和 **k** 。问题是检查在 **n** 的二进制表示中从右侧开始的位置 **k** 处的位是置位(' 1 ')还是未置位(' 0 ')。
**约束:** 1 < = k < =二进制表示的位数 **n** 。
示例:

```
Input : n = 10, k = 2
Output : Set
(10)<sub>10</sub> = (1010)2
The 2nd bit from the right is set.

Input : n = 21, k = 4
Output : Unset
```

**进场:**以下为步骤:

1.  计算**new _ num**=(n>>(k–1))。
2.  如果(new_num & 1) == 1，则该位为“置位”，否则为“未置位”。

## C++

```
// C++ implementation to check whether the bit
// at given position is set or unset
#include <bits/stdc++.h>
using namespace std;

// function to check whether the bit
// at given position is set or unset
bool bitAtGivenPosSetOrUnset(unsigned int n,
                             unsigned int k)
{
    int new_num = n >> (k - 1);

    // if it results to '1' then bit is set,
    // else it results to '0' bit is unset
    return (new_num & 1);
}

// Driver program to test above
int main()
{
    unsigned int n = 10, k = 2;
    if (bitAtGivenPosSetOrUnset(n, k))
        cout << "Set";
    else
        cout << "Unset";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to
// check the set bit
// at kth position
import java.io.*;

class GFG {

// function to check whether
// the bit at given position
// is set or unset
static int bitAtGivenPosSetOrUnset
                   ( int n, int k)
{

    // to shift the kth bit
    // at 1st position
    int new_num = n >> (k - 1);

    // Since, last bit is now
    // kth bit, so doing AND with 1
    // will give result.
    return (new_num & 1);
}
    public static void main (String[] args)
    {
         // K and n must be greater than 0
         int n = 10, k = 2;

    if (bitAtGivenPosSetOrUnset(n, k)==1)
        System.out.println("Set");
    else
        System.out.println("Unset");
    }
}

//This code is contributed by Gitanjali
```

## 蟒蛇 3

```
# python implementation to check
# whether the bit at given
# position is set or unset

import math
#function to check whether the bit
# at given position is set or unset
def bitAtGivenPosSetOrUnset(  n,  k):
     new_num = n >> (k - 1)

     #if it results to '1' then bit is set,
     #else it results to '0' bit is unset
     return (new_num & 1)

# Driver code
n = 10
k = 2
if (bitAtGivenPosSetOrUnset(n, k)):
     print("Set")
else:
    print("Unset")

#This code is contributed by Gitanjali
```

## C#

```
// C# program to check the set bit
// at kth position
using System;

class GFG {

    // function to check whether
    // the bit at given position
    // is set or unset
    static int bitAtGivenPosSetOrUnset(
                           int n, int k)
    {

        // to shift the kth bit
        // at 1st position
        int new_num = n >> (k - 1);

        // Since, last bit is now
        // kth bit, so doing AND with 1
        // will give result.
        return (new_num & 1);
    }

    // Driver code
    public static void Main ()
    {

        // K and n must be greater
        // than 0
        int n = 10, k = 2;

        if (bitAtGivenPosSetOrUnset(n, k)==1)
            Console.Write("Set");
        else
            Console.Write("Unset");
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check whether the bit
// at given position is set or unset

// function to check whether the bit
// at given position is set or unset
function bitAtGivenPosSetOrUnset($n, $k)
{
    $new_num = $n >> ($k - 1);

    // if it results to '1' then bit is set,
    // else it results to '0' bit is unset
    return ($new_num & 1);
}

    // Driver Code
    $n = 10;
    $k = 2;
    if (bitAtGivenPosSetOrUnset($n, $k))
        echo "Set";
    else
        echo "Unset";

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// javascript program to
// check the set bit
// at kth position

// function to check whether
// the bit at given position
// is set or unset
function bitAtGivenPosSetOrUnset
                   (n, k)
{

    // to shift the kth bit
    // at 1st position
    let new_num = n >> (k - 1);

    // Since, last bit is now
    // kth bit, so doing AND with 1
    // will give result.
    return (new_num & 1);
}

// Driver Function

         // K and n must be greater than 0
         let n = 10, k = 2;

    if (bitAtGivenPosSetOrUnset(n, k)==1)
        document.write("Set");
    else
        document.write("Unset");

    // This code is contributed by susmitakundugoaldanga.
</script>
```

输出:

```
Set
```

**时间复杂度:** O(1)。