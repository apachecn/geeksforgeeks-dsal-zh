# 检查一个数字在交替模式中是否有位|设置 1

> 原文:[https://www . geesforgeks . org/check-if-a-number-with-bit-in-alternate-pattern/](https://www.geeksforgeeks.org/check-if-a-number-has-bits-in-alternate-pattern/)

给定一个整数 n > 0，任务是找出这个整数在其位表示中是否有替换模式。例如- 5 具有交替模式，即 101。
如果有备用图案，则打印“是”，否则打印“否”。这里交替模式可以像 0101 或 1010。

示例:

```
Input :  15
Output :  No
Explanation: Binary representation of 15 is 1111.

Input :  10
Output :  Yes
Explanation: Binary representation of 10 is 1010.
```

一个简单的方法是找到它的二进制等价物，然后检查它的位。

## C++

```
// C++ program to find if a number has alternate
// bit pattern
#include<bits/stdc++.h>
using namespace std;

// Returns true if n has alternate bit pattern
// else false
bool findPattern(int n)
{
    // Store last bit
    int prev = n % 2;
    n = n/2;

    // Traverse through remaining bits
    while (n > 0)
    {
        int curr = n % 2;

        // If current bit is same as previous
        if (curr == prev)
           return false;

        prev = curr;
        n = n / 2;
    }

    return true;
}

// Driver code
int main()
{
    int n = 10;
    if (findPattern(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a number has alternate
// bit pattern

class Test
{
    // Returns true if n has alternate bit pattern
    // else false
    static boolean findPattern(int n)
    {
        // Store last bit
        int prev = n % 2;
        n = n/2;

        // Traverse through remaining bits
        while (n > 0)
        {
            int curr = n % 2;

            // If current bit is same as previous
            if (curr == prev)
               return false;

            prev = curr;
            n = n / 2;
        }

        return true;
    }

    // Driver method
    public static void main(String args[])
    {
        int n = 10;
        System.out.println(findPattern(n) ? "Yes" : "No");

    }
}
```

## 蟒蛇 3

```
# Python3 program to find if a number
# has alternate bit pattern

# Returns true if n has alternate
# bit pattern else false
def findPattern(n):

    # Store last bit
    prev = n % 2
    n = n // 2

    # Traverse through remaining bits
    while (n > 0):

        curr = n % 2

        # If current bit is same as previous
        if (curr == prev):
            return False

        prev = curr
        n = n // 2

    return True

# Driver code
n = 10
print("Yes") if(findPattern(n)) else print("No")

# This code is contributed by Anant Agarwal.
```

## C#

```
// Program to find if a number
// has alternate bit pattern
using System;

class Test {

    // Returns true if n has alternate
    // bit pattern else returns false
    static bool findPattern(int n)
    {
        // Store last bit
        int prev = n % 2;
        n = n / 2;

        // Traverse through remaining bits
        while (n > 0) {
            int curr = n % 2;

            // If current bit is same as previous
            if (curr == prev)
                return false;

            prev = curr;
            n = n / 2;
        }

        return true;
    }

    // Driver method
    public static void Main()
    {
        int n = 10;
        Console.WriteLine(findPattern(n) ? "Yes" : "No");
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if a
// number has alternate
// bit pattern

// Returns true if n has
// alternate bit pattern
// else false
function findPattern($n)
{

    // Store last bit
    $prev = $n % 2;
    $n = $n / 2;

    // Traverse through
    // remaining bits
    while ($n > 0)
    {
        $curr = $n % 2;

        // If current bit is
        // same as previous
        if ($curr == $prev)
        return false;

        $prev = $curr;
        $n = floor($n / 2);
    }

    return true;
}

    // Driver code
    $n = 10;
    if (findPattern($n))
        echo "Yes";
    else
        echo "No";

    return 0;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to find if a number
// has alternate bit pattern

// Returns true if n has alternate
// bit pattern else false
function findPattern(n)
{

    // Store last bit
    let prev = n % 2;
    n = Math.floor(n / 2);

    // Traverse through remaining bits
    while (n > 0)
    {
        let curr = n % 2;

        // If current bit is
        // same as previous
        if (curr == prev)
            return false;

        prev = curr;
        n = Math.floor(n / 2);
    }
    return true;
}

// Driver code
let n = 10;
if (findPattern(n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by gfgking

</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(log <sub>2</sub> n)

**辅助空间:** O(1)

**参考:**
[http://stackoverflow . com/questions/38690278/program-to-check-给定整数是否有替代模式](http://stackoverflow.com/questions/38690278/program-to-check-whether-the-given-integer-has-an-alternate-pattern)

本文由 [**萨希尔·查布拉(akku)**](https://practice.geeksforgeeks.org/user-profile.php?user=sahil_coder) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。