# 用基数变化法

检查一个数是否为 k 的幂

> 原文:[https://www . geesforgeks . org/check-number-power-k-use-base-changing-method/](https://www.geeksforgeeks.org/check-number-power-k-using-base-changing-method/)

这个程序检查一个数 n 是否可以表示为 k 的幂，如果可以，那么 k 应该升到什么幂才能成为 n。下面的例子将阐明:
**例子:**

```
Input :   n = 16, k = 2 
Output :  yes : 4
Explanation : Answer is yes because 16 can 
be expressed as power of 2\. 

Input :   n = 27, k = 3 
Output :  yes : 3
Explanation : Answer is yes as 27 can be
expressed as power of 3.

Input :  n = 20, k = 5
Output : No
Explanation : Answer is No as 20 cannot 
be expressed as power of 5\.  
```

我们在下面的帖子
中讨论了两种方法:[检查一个数是否是另一个数的幂](https://www.geeksforgeeks.org/check-if-a-number-is-power-of-another-number/)
在这篇帖子中，讨论了一种新的基数变化方法。
在**基数变化法**中，我们简单的把数字 n 的基数改为 k，检查变化数的第一位数字是否为 1，其余全部为零。
**这个例子**:我们取 n = 16，k = 2。
将 16 改为基数 2。即(10000) <sub>2</sub> 。因为第一个数字是 1，其余的是零。因此 16 可以表示为 2 的幂。数一数(10000) <sub>2</sub> 的长度，然后减去 1，那就是 2 必须加到的数，等于 16。在这种情况下，5–1 = 4。
**再举一个例子**:我们取 n = 20，k = 3。
20 在基数 3 是(202) <sub>3</sub> 。由于有两个非零数字，因此 20 不能表示为 3 的幂。

## C++

```
// CPP program to check if a number can be
// raised to k
#include <iostream>
#include <algorithm>
using namespace std;

bool isPowerOfK(unsigned int n, unsigned int k)
{
    // loop to change base n to base = k
    bool oneSeen = false;
    while (n > 0) {

        // Find current digit in base k
        int digit = n % k;

        // If digit is neither 0 nor 1
        if (digit > 1)
            return false;

        // Make sure that only one 1
        // is present.
        if (digit == 1)
        {
            if (oneSeen)
            return false;
            oneSeen = true;
        }    

        n /= k;
    }

    return true;
}

// Driver code
int main()
{
    int n = 64, k = 4;

    if (isPowerOfK(n ,k))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number can be
// raised to k

class GFG
{
    static boolean isPowerOfK(int n,int k)
    {
        // loop to change base n to base = k
        boolean oneSeen = false;
        while (n > 0)
        {

            // Find current digit in base k
            int digit = n % k;

            // If digit is neither 0 nor 1
            if (digit > 1)
                return false;

            // Make sure that only one 1
            // is present.
            if (digit == 1)
            {
                if (oneSeen)
                return false;
                oneSeen = true;
            }    

            n /= k;
        }

        return true;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 64, k = 4;

        if (isPowerOfK(n ,k))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to
# check if a number can be
# raised to k

def isPowerOfK(n, k):

    # loop to change base
    # n to base = k
    oneSeen = False
    while (n > 0):

        # Find current digit in base k
        digit = n % k

        # If digit is neither 0 nor 1
        if (digit > 1):
            return False

        # Make sure that only one 1
        # is present.
        if (digit == 1):

            if (oneSeen):
                return False
            oneSeen = True

        n //= k

    return True

# Driver code

n = 64
k = 4

if (isPowerOfK(n , k)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to check if a number can be
// raised to k
using System;

class GFG {

    static bool isPowerOfK(int n, int k)
    {

        // loop to change base n to base = k
        bool oneSeen = false;
        while (n > 0)
        {

            // Find current digit in base k
            int digit = n % k;

            // If digit is neither 0 nor 1
            if (digit > 1)
                return false;

            // Make sure that only one 1
            // is present.
            if (digit == 1)
            {
                if (oneSeen)
                    return false;

                oneSeen = true;
            }

            n /= k;
        }

        return true;
    }

    // Driver code
    public static void Main ()
    {
        int n = 64, k = 4;

        if (isPowerOfK(n ,k))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// if a number can be
// raised to k

function isPowerOfK($n, $k)
{
    // loop to change base
    // n to base = k
    $oneSeen = false;
    while ($n > 0)
    {

        // Find current
        // digit in base k
        $digit = $n % $k;

        // If digit is
        // neither 0 nor 1
        if ($digit > 1)
            return false;

        // Make sure that
        // only one 1
        // is present.
        if ($digit == 1)
        {
            if ($oneSeen)
            return false;
            $oneSeen = true;
        }

        $n = (int)$n / $k;
    }

    return true;
}

// Driver code
$n = 64;
$k = 4;

if (isPowerOfK($n, $k))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by ajit
?>
```

## java 描述语言

```
<script>
// JavaScript program to check if a number can be
// raised to k

    function isPowerOfK(n,k)
    {
        // loop to change base n to base = k
        let oneSeen = false;
        while (n > 0)
        {

            // Find current digit in base k
            let digit = n % k;

            // If digit is neither 0 nor 1
            if (digit > 1)
                return false;

            // Make sure that only one 1
            // is present.
            if (digit == 1)
            {
                if (oneSeen)
                return false;
                oneSeen = true;
            }    

            n = Math.floor(n / k);
        }

        return true;
    }

// Driver Code

        let n = 64, k = 4;

        if (isPowerOfK(n ,k))
            document.write("Yes");
        else
            document.write("No");

</script>
```

**输出:**

```
Yes
```

本文由**舒巴姆拉纳**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。