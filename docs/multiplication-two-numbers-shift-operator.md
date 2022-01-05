# 用移位运算符将两个数相乘

> 原文:[https://www . geeksforgeeks . org/乘法-两位数-移位-运算符/](https://www.geeksforgeeks.org/multiplication-two-numbers-shift-operator/)

对于任何给定的两个数字 n 和 m，你必须在不使用任何乘法运算符的情况下找到 n*m。
**例:**

```
Input: n = 25 , m = 13
Output: 325

Input: n = 50 , m = 16
Output: 800
```

我们可以用移位运算符解决这个问题。这个想法是基于这样一个事实，即每个数字都可以用二进制形式表示。和一个数相乘相当于和 2 的幂相乘。使用左移运算符可以获得 2 的幂。
检查 m 的二进制表示中的每个设置位以及每个设置位的左移位 n，计算 m 的设置位的置位值的计数次数，并将该值相加得到答案。

## C++

```
// CPP program to find multiplication
// of two number without use of
// multiplication operator
#include<bits/stdc++.h>
using namespace std;

// Function for multiplication
int multiply(int n, int m)
{ 
    int ans = 0, count = 0;
    while (m)
    {
        // check for set bit and left
        // shift n, count times
        if (m % 2 == 1)             
            ans += n << count;

        // increment of place value (count)
        count++;
        m /= 2;
    }
    return ans;
}

// Driver code
int main()
{
    int n = 20 , m = 13;
    cout << multiply(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find multiplication
// of two number without use of
// multiplication operator
class GFG
{

    // Function for multiplication
    static int multiply(int n, int m)
    {
        int ans = 0, count = 0;
        while (m > 0)
        {
            // check for set bit and left
            // shift n, count times
            if (m % 2 == 1)            
                ans += n << count;

            // increment of place
            // value (count)
            count++;
            m /= 2;
        }

        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 20, m = 13;

        System.out.print( multiply(n, m) );
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# python 3 program to find multiplication
# of two number without use of
# multiplication operator

# Function for multiplication
def multiply(n, m):
    ans = 0
    count = 0
    while (m):
        # check for set bit and left
        # shift n, count times
        if (m % 2 == 1):
            ans += n << count

        # increment of place value (count)
        count += 1
        m = int(m/2)

    return ans

# Driver code
if __name__ == '__main__':
    n = 20
    m = 13
    print(multiply(n, m))

# This code is contributed by
# Ssanjit_Prasad
```

## C#

```
// C# program to find multiplication
// of two number without use of
// multiplication operator
using System;

class GFG
{

    // Function for multiplication
    static int multiply(int n, int m)
    {
        int ans = 0, count = 0;
        while (m > 0)
        {
            // check for set bit and left
            // shift n, count times
            if (m % 2 == 1)        
                ans += n << count;

            // increment of place
            // value (count)
            count++;
            m /= 2;
        }

        return ans;
    }

    // Driver Code
    public static void Main ()
    {
        int n = 20, m = 13;

        Console.WriteLine( multiply(n, m) );
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find multiplication
// of two number without use of
// multiplication operator

// Function for multiplication
function multiply( $n, $m)
{
    $ans = 0; $count = 0;
    while ($m)
    {
        // check for set bit and left
        // shift n, count times
        if ($m % 2 == 1)            
            $ans += $n << $count;

        // increment of place value (count)
        $count++;
        $m /= 2;
    }
    return $ans;
}

// Driver code
$n = 20 ; $m = 13;
echo multiply($n, $m);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find multiplication
// of two number without use of
// multiplication operator

// Function for multiplication
function multiply(n, m)
{
    let ans = 0, count = 0;
    while (m)
    {
        // check for set bit and left
        // shift n, count times
        if (m % 2 == 1)            
            ans += n << count;

        // increment of place value (count)
        count++;
        m = Math.floor(m / 2);
    }
    return ans;
}

// Driver code

    let n = 20 , m = 13;
    document.write(multiply(n, m));

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
260
```

**时间复杂度:** O(log n)
**相关文章:**
[俄罗斯农民(使用按位运算符乘以两个数字)](https://www.geeksforgeeks.org/russian-peasant-multiply-two-numbers-using-bitwise-operators/)
本文由[**Shivam prad Han(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。