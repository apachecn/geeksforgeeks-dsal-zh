# 检查一个数字的所有位是否都已设置

> 原文:[https://www.geeksforgeeks.org/check-bits-number-set/](https://www.geeksforgeeks.org/check-bits-number-set/)

给定一个数字 **n** 。问题是检查给定数字的二进制表示中的每一位是否都被设置。这里 0 < = **n** 。
**例:**

```
Input : 7
Output : Yes
(7)<sub>10</sub> = (111)2

Input : 14
Output : No
```

**方法 1:** 如果 **n** = 0，则回答为‘否’。否则执行这两个操作，直到 **n** 变为 0。

```
While (n > 0)
 If n & 1 == 0, 
     return 'No'
 n >> 1
```

如果循环终止而没有返回“否”，那么所有的位都被设置为二进制表示 **n** 。

## C++

```
// C++ implementation to check whether every
// digit in the binary representation of the
// given number is set or not
#include <bits/stdc++.h>
using namespace std;

// function to check if all the bits are set
// or not in the binary representation of 'n'
string areAllBitsSet(int n)
{
    // all bits are not set
    if (n == 0)
        return "No";

    // loop till n becomes '0'
    while (n > 0)
    {
        // if the last bit is not set
        if ((n & 1) == 0)
            return "No";

        // right shift 'n' by 1
        n = n >> 1;
    }

    // all bits are set
    return "Yes";
}

// Driver program to test above
int main()
{
    int n = 7;
    cout << areAllBitsSet(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java implementation to check
// whether every digit in the
// binary representation of the
// given number is set or not
import java.io.*;

class GFG {

    // function to check if all the bits
    // are setthe bits are set or not
    // in the binary representation of 'n'
    static String areAllBitsSet(int n)
    {
        // all bits are not set
        if (n == 0)
            return "No";

        // loop till n becomes '0'
        while (n > 0)
        {
            // if the last bit is not set
            if ((n & 1) == 0)
                return "No";

            // right shift 'n' by 1
            n = n >> 1;
        }

            // all bits are set
            return "Yes";
    }

    // Driver program to test above
    public static void main (String[] args) {
    int n = 7;

    System.out.println(areAllBitsSet(n));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python implementation
# to check whether every
# digit in the binary
# representation of the
# given number is set or not

# function to check if
# all the bits are set
# or not in the binary
# representation of 'n'
def areAllBitsSet(n):

    # all bits are not set
    if (n == 0):
        return "No"

    # loop till n becomes '0'
    while (n > 0):

        # if the last bit is not set
        if ((n & 1) == 0):
            return "No"

        # right shift 'n' by 1
        n = n >> 1

    # all bits are set
    return "Yes"

# Driver program to test above

n = 7
print(areAllBitsSet(n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# implementation to check
// whether every digit in the
// binary representation of the
// given number is set or not
using System;

class GFG
{

    // function to check if 
    // all the bits are set
    // or not in the binary
    // representation of 'n'
    static String areAllBitsSet(int n)
    {
        // all bits are not set
        if (n == 0)
            return "No";

        // loop till n becomes '0'
        while (n > 0)
        {
            // if the last bit
            // is not set
            if ((n & 1) == 0)
                return "No";

            // right shift 'n' by 1
            n = n >> 1;
        }

            // all bits are set
            return "Yes";
    }

    // Driver Code
    static public void Main ()
    {
        int n = 7;
        Console.WriteLine(areAllBitsSet(n));
    }
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check
// whether every digit in the
// binary representation of the
// given number is set or not

// function to check if all the
// bits are set or not in the
// binary representation of 'n'
function areAllBitsSet($n)
{
    // all bits are not set
    if ($n == 0)
        return "No";

    // loop till n becomes '0'
    while ($n > 0)
    {
        // if the last bit is not set
        if (($n & 1) == 0)
            return "No";

        // right shift 'n' by 1
        $n = $n >> 1;
    }

    // all bits are set
    return "Yes";
}

// Driver Code
$n = 7;
echo areAllBitsSet($n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// javascript implementation to check
// whether every digit in the
// binary representation of the
// given number is set or not

// function to check if all the bits
// are setthe bits are set or not
// in the binary representation of 'n'
function areAllBitsSet(n)
{
    // all bits are not set
    if (n == 0)
        return "No";

    // loop till n becomes '0'
    while (n > 0)
    {
        // if the last bit is not set
        if ((n & 1) == 0)
            return "No";

        // right shift 'n' by 1
        n = n >> 1;
    }

        // all bits are set
        return "Yes";
}

// Driver program to test above
var n = 7;
document.write(areAllBitsSet(n));

// This code contributed by Princi Singh

</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(d)，其中‘d’是 **n** 二进制表示中的位数。

**方法二:**如果 **n** = 0，则回答为‘否’。否则在 **n** 上加 1。让它成为 **num** = n + 1。如果 num&(num–1)= = 0，则所有位都被置位，否则所有位都不被置位。
**说明:**如果 **n** 的二进制表示中的所有位都被置位，那么加上“1”将产生一个数字，该数字将是 2 的完美幂。现在，检查新数字是否是 2 的完美幂。

## C++

```
// C++ implementation to check whether every
// digit in the binary representation of the
// given number is set or not
#include <bits/stdc++.h>
using namespace std;

// function to check if all the bits are set
// or not in the binary representation of 'n'
string areAllBitsSet(int n)
{
    // all bits are not set
    if (n == 0)
        return "No";

    // if true, then all bits are set
    if (((n + 1) & n) == 0)
        return "Yes";

    // else all bits are not set
    return "No";
}

// Driver program to test above
int main()
{
    int n = 7;
    cout << areAllBitsSet(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA implementation to check whether
// every digit in the binary representation
// of the given number is set or not
import java.io.*;

class GFG {

    // function to check if all the
    // bits are set or not in the
    // binary representation of 'n'
    static String areAllBitsSet(int n)
    {
        // all bits are not set
        if (n == 0)
            return "No";

        // if true, then all bits are set
        if (((n + 1) & n) == 0)
            return "Yes";

        // else all bits are not set
        return "No";
    }

    // Driver program to test above
    public static void main (String[] args) {
    int n = 7;
    System.out.println(areAllBitsSet(n));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python implementation to
# check whether every
# digit in the binary
# representation of the
# given number is set or not

# function to check if
# all the bits are set
# or not in the binary
# representation of 'n'
def areAllBitsSet(n):

    # all bits are not set
    if (n == 0):
        return "No"

    # if true, then all bits are set
    if (((n + 1) & n) == 0):
        return "Yes"

    # else all bits are not set
    return "No"

# Driver program to test above

n = 7
print(areAllBitsSet(n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# implementation to check
// whether every digit in the
// binary representation of
// the given number is set or not
using System;

class GFG
{

    // function to check if all the
    // bits are set or not in the
    // binary representation of 'n'
    static String areAllBitsSet(int n)
    {
        // all bits are not set
        if (n == 0)
            return "No";

        // if true, then all
        // bits are set
        if (((n + 1) & n) == 0)
            return "Yes";

        // else all bits are not set
        return "No";
    }

    // Driver Code
    static public void Main ()
    {
        int n = 7;
        Console.WriteLine(areAllBitsSet(n));
    }
}

// This code is contributed by m_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check
// whether every digit in the
// binary representation of the
// given number is set or not

// function to check if all
// the bits are set or not in
// the binary representation of 'n'
function areAllBitsSet($n)
{
    // all bits are not set
    if ($n == 0)
        return "No";

    // if true, then all
    // bits are set
    if ((($n + 1) & $n) == 0)
        return "Yes";

    // else all bits
    // are not set
    return "No";
}

// Driver Code
$n = 7;
echo areAllBitsSet($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript implementation to check whether
// every digit in the binary representation
// of the given number is set or not

// function to check if all the
// bits are set or not in the
// binary representation of 'n'
function areAllBitsSet(n)
{
    // all bits are not set
    if (n == 0)
        return "No";

    // if true, then all bits are set
    if (((n + 1) & n) == 0)
        return "Yes";

    // else all bits are not set
    return "No";
}

// Driver program to test above
var n = 7;
document.write(areAllBitsSet(n));

// This code contributed by Princi Singh
</script>
```

**Output**

```
Yes
```

**方法 3** :我们可以简单地对数字的二进制表示中存在的总集合位进行计数，基于此，我们可以检查该数字是否等于幂(2，__builtin_popcount(n))。如果恰好相等，那么我们返回 1，否则返回 0；

## C++

```
#include <bits/stdc++.h>
using namespace std;

void isBitSet(int N)
{
    if (N == pow(2, __builtin_popcount(N)) - 1)
        cout << "Yes\n";
    else cout << "No\n";
}

int main()
{
    int N = 7;
    isBitSet(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{

static void isBitSet(int N)
{
    if (N == Math.pow(2, Integer.bitCount(N)) - 1)
        System.out.print("Yes\n");
    else System.out.print("No\n");
}

public static void main(String[] args)
{
    int N = 7;
    isBitSet(N);
}
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
def bitCount(n):
    n = n - ((n >> 1) & 0x55555555);
    n = (n & 0x33333333) + ((n >> 2) & 0x33333333);
    return ((n + (n >> 4) & 0xF0F0F0F) * 0x1010101) >> 24;

def isBitSet(N):
    if (N == pow(2, bitCount(N)) - 1):
        print("Yes");
    else:
        print("No");

if __name__ == '__main__':
    N = 7;
    isBitSet(N);

# This code is contributed by gauravrajput1
```

## C#

```
using System;

public class GFG{
     static int bitCount (int n) {
          n = n - ((n >> 1) & 0x55555555);
          n = (n & 0x33333333) + ((n >> 2) & 0x33333333);
          return ((n + (n >> 4) & 0xF0F0F0F) * 0x1010101) >> 24;
        }

static void isBitSet(int N)
{
    if (N == Math.Pow(2, bitCount(N)) - 1)
        Console.Write("Yes\n");
    else Console.Write("No\n");
}

public static void Main(String[] args)
{
    int N = 7;
    isBitSet(N);
}
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>
   function bitCount (n) {
        n = n - ((n >> 1) & 0x55555555);
        n = (n & 0x33333333) + ((n >> 2) & 0x33333333);
        return ((n + (n >> 4) & 0xF0F0F0F) * 0x1010101) >> 24;
      }
    function isBitSet(N) {
        if (N == Math.pow(2, bitCount(N)) - 1)
            document.write("Yes\n");
        else
            document.write("No\n");
    }

        var N = 7;
        isBitSet(N);

// This code is contributed by umadevi9616
</script>
```

**输出:**

```
Yes
```

**参考文献:**
https://www.careercup.com/question?id=9503107
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。