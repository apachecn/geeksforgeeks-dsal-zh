# 使用加法/减法检查完美平方

> 原文:[https://www . geesforgeks . org/check-number-is-perfect-square-using-additionsubtraction/](https://www.geeksforgeeks.org/check-number-is-perfect-square-using-additionsubtraction/)

给定一个正整数 n，检查它是否是完美平方，或者是否仅使用加法/减法运算，并且时间复杂度最小。
**我们强烈建议你尽量减少浏览器，先自己试试这个。**
我们可以利用奇数的性质来达到这个目的:

```
Addition of first n odd numbers is always perfect square 
1 + 3 = 4,      
1 + 3 + 5 = 9,     
1 + 3 + 5 + 7 + 9 + 11 = 36 ...
```

以下是上述想法的实现:

## C++

```
// C++ program to check if n is perfect square
// or not
#include <bits/stdc++.h>

using namespace std;

// This function returns true if n is
// perfect square, else false
bool isPerfectSquare(int n)
{
    // sum is sum of all odd numbers. i is
    // used one by one hold odd numbers
    for (int sum = 0, i = 1; sum < n; i += 2) {
        sum += i;
        if (sum == n)
            return true;
    }
    return false;
}

// Driver code
int main()
{
    isPerfectSquare(35) ? cout << "Yes\n" : cout << "No\n";
    isPerfectSquare(49) ? cout << "Yes\n" : cout << "No\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if n
// is perfect square or not

public class GFG {

    // This function returns true if n
    // is perfect square, else false
    static boolean isPerfectSquare(int n)
    {
        // sum is sum of all odd numbers. i is
        // used one by one hold odd numbers
        for (int sum = 0, i = 1; sum < n; i += 2) {
            sum += i;
            if (sum == n)
                return true;
        }
        return false;
    }

    // Driver Code
    public static void main(String args[])
    {

        if (isPerfectSquare(35))
            System.out.println("Yes");
        else
            System.out.println("NO");

        if (isPerfectSquare(49))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# This function returns true if n is
# perfect square, else false
def isPerfectSquare(n):

    # the_sum is sum of all odd numbers. i is
    # used one by one hold odd numbers
    i = 1
    the_sum = 0
    while the_sum < n:
        the_sum += i
        if the_sum == n:
            return True
        i += 2
    return False

# Driver code
if __name__ == "__main__":
    print('Yes') if isPerfectSquare(35) else print('NO')
    print('Yes') if isPerfectSquare(49) else print('NO')

# This code works only in Python 3
```

## C#

```
// C# program to check if n
// is perfect square or not
using System;

public class GFG {

    // This function returns true if n
    // is perfect square, else false
    static bool isPerfectSquare(int n)
    {
        // sum is sum of all odd numbers. i is
        // used one by one hold odd numbers
        for (int sum = 0, i = 1; sum < n; i += 2) {
            sum += i;
            if (sum == n)
                return true;
        }
        return false;
    }

    // Driver Code
    public static void Main(String[] args)
    {

        if (isPerfectSquare(35))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");

        if (isPerfectSquare(49))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if n is
// perfect square or not

// This function returns true if n is
// perfect square, else false
function isPerfectSquare($n)
{
    // sum is sum of all odd numbers.
    // i is used one by one hold odd
    // numbers
    for ( $sum = 0, $i = 1; $sum < $n;
                              $i += 2)
    {
        $sum += $i;
        if ($sum == $n)
            return true;
    }

    return false;
}

// Driver code
if(isPerfectSquare(35))
    echo "Yes\n";
else
    echo "No\n";

if(isPerfectSquare(49))
    echo "Yes\n";
else
    echo "No\n";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to check if n
// is perfect square or not

    // This function returns true if n
    // is perfect square, else false
    function isPerfectSquare(n)
    {
        // sum is sum of all odd numbers. i is
        // used one by one hold odd numbers
        for (let sum = 0, i = 1; sum < n; i += 2) {
            sum += i;
            if (sum == n)
                return true;
        }
        return false;
    }

// Driver Code

        if (isPerfectSquare(35))
           document.write("Yes" + "<br/>");
        else
            document.write("NO" + "<br/>");

        if (isPerfectSquare(49))
            document.write("Yes" + "<br/>");
        else
            document.write("No" + "<br/>");

    // This code is contributed by target_2.
</script>
```

输出:

```
No
Yes
```

***时间复杂度:** O(n)*

***辅助空间:**O(1)*
T5】这是怎么工作的？
以下是上述方法的说明。

```
1 + 3 + 5 + ...  (2n-1) = ∑(2*i - 1) where 1<=i<=n
                        = 2*∑i - ∑1  where 1<=i<=n
                        = 2n(n+1)/2 - n
                        = n(n+1) - n
                        = n2
```

**参考:**
[https://www . geesforgeks . org/sum-first-n-奇数-numbers-O1-complexity/](https://www.geeksforgeeks.org/sum-first-n-odd-numbers-o1-complexity/)
[http://blog . jgc . org/2008/02/sum-first-n-奇数-is-always.html](http://blog.jgc.org/2008/02/sum-of-first-n-odd-numbers-is-always.html)
本文由 Utkarsh Trivedi 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。