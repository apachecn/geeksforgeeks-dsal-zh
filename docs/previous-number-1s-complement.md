# 前一个数字与 1 的补码相同

> 原文:[https://www . geesforgeks . org/previous-number-1s-complete/](https://www.geeksforgeeks.org/previous-number-1s-complement/)

给定一个数，检查它的前身和它的 1 的补码的二进制表示是否相同。
**例:**

> 输入:14
> 输出:否
> 将 14 存储为 4 位数字，14 (1110)，其前身 13 (1101)，其 1 的补码 1 (0001)，13 和 1 的二进制表示不相同，因此输出为否
> 输入:8
> 输出:是
> 将 8 存储为 4 位数字，8 (1000)，其前身 7 (0111)，其 1 的补码 7 (0111)，包括其前身和其 1

**简单方法:**在这种方法中，我们实际上计算了数的补数。
1。使用简单的十进制到二进制表示技术，找到数字的前身及其 1 的补码的二进制表示。
2。一点一点比较，看它们是否相等。
3。如果所有位都相等，则打印是，否则打印否
**时间复杂度:**0(对数 n)，因为数字的二进制表示正在被计算。
**辅助空间:** O (1)，虽然辅助空间是 O (1)，但仍有一些内存空间正在得到
用来存储数字的二进制表示。
**有效方法:**只有 2 的幂的数才有它们的前身的二进制表示和它们的 1 的补码相同。
1。检查一个数是否是 2 的幂。
2。如果数字是 2 的幂，则打印是，否则打印否

## C++

```
// An efficient C++ program to check if binary
// representations of n's predecessor and its
// 1's complement are same.
#include <bits/stdc++.h>
#define ull unsigned long long int
using namespace std;

// Returns true if binary representations of
// n's predecessor and it's 1's complement are same.
bool bit_check(ull n)
{
    if ((n & (n - 1)) == 0)
        return true;
    return false;
}

int main()
{
    ull n = 14;
    cout << bit_check(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An efficient java program to check if binary
// representations of n's predecessor and its
// 1's complement are same.
public class GFG {

    // Returns true if binary representations of
    // n's predecessor and it's 1's complement
    // are same.
    static boolean bit_check(int n)
    {
        if ((n & (n - 1)) == 0)
            return true;
        return false;
    }

    // Driver code   
    public static void main(String args[]) {

         int n = 14;
         if(bit_check(n))
            System.out.println ('1');
         else
            System.out.println('0');

    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# An efficient Python 3 program to check
# if binary representations of n's predecessor
# and its 1's complement are same.

# Returns true if binary representations
# of n's predecessor and it's 1's
# complement are same.
def bit_check(n):
    if ((n & (n - 1)) == 0):
        return True
    return False

# Driver Code
if __name__ == '__main__':
    n = 14
    if(bit_check(n)):
        print('1')
    else:
        print('0')

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// An efficient C# program to check if binary
// representations of n's predecessor and its
// 1's complement are same.
using System;
using System.Collections.Generic;

class GFG {

    // Returns true if binary representations of
    // n's predecessor and it's 1's complement
    // are same.
    static bool bit_check(int n)
    {
        if ((n & (n - 1)) == 0)
            return true;
        return false;
    }

    public static void Main()
    {
         int n = 14;
         if(bit_check(n))
            Console.WriteLine ('1');
         else
            Console.WriteLine ('0');
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// An efficient PHP program to check
// if binary representations of n's
// predecessor and its 1's complement
// are same.

// Returns true if binary
// representations of n's
// predecessor and it's 1's
// complement are same.
function bit_check($n)
{
    if (($n & ($n - 1)) == 0)
        return 1;
    return 0;
}

    // Driver code
    $n = 14;
    echo bit_check($n);

// This code is contributed by Sam007.
?>
```

## java 描述语言

```
<script>
    // An efficient Javascript program to check if binary
    // representations of n's predecessor and its
    // 1's complement are same.

    // Returns true if binary representations of
    // n's predecessor and it's 1's complement
    // are same.
    function bit_check(n)
    {
        if ((n & (n - 1)) == 0)
            return true;
        return false;
    }

    let n = 14;
    if(bit_check(n))
      document.write('1');
    else
      document.write('0');

</script>
```

**Output:** 

```
0
```

**时间复杂度:**O(1)
T3】辅助空间: O (1)没有多余的空间被使用。