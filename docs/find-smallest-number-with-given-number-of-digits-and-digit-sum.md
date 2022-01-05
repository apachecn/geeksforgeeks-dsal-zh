# 找到给定位数和位数总和的最小数

> 原文:[https://www . geesforgeks . org/find-给定位数和位数相加的最小数/](https://www.geeksforgeeks.org/find-smallest-number-with-given-number-of-digits-and-digit-sum/)

给定位数和 **s** 和位数 **d** 如何求最小数？
**例:**

```
Input  : s = 9, d = 2
Output : 18
There are many other possible numbers 
like 45, 54, 90, etc with sum of digits
as 9 and number of digits as 2\. The 
smallest of them is 18.

Input  : s = 20, d = 3
Output : 299
```

一个**简单解**是考虑所有 m 个数字，以数字和为 s 跟踪最小数，这个解的时间复杂度的一个接近的上界是 O(10 <sup>m</sup> )。
有一个**贪婪的方法**来解决问题。其思想是从最右边到最左边(或从最低有效位到最高有效位)逐一填充所有数字。
我们最初从总和 s 中扣除 1，这样我们在末尾有最小的数字。扣除 1 后，我们应用贪婪方法。我们把余数和 9 进行比较，如果余数大于 9，我们把 9 放在当前位置，否则我们把余数放进去。因为我们从右向左填充数字，所以我们把最高的数字放在右边。下面是这个想法的实现。

## C++

```
// C++ program to find the smallest number that can be
// formed from given sum of digits and number of digits.
#include <iostream>
using namespace std;

// Prints the smallest possible number with digit sum 's'
// and 'm' number of digits.
void findSmallest(int m, int s)
{
    // If sum of digits is 0, then a number is possible
    // only if number of digits is 1.
    if (s == 0)
    {
        (m == 1)? cout << "Smallest number is " << 0
                : cout << "Not possible";
        return ;
    }

    // Sum greater than the maximum possible sum.
    if (s > 9*m)
    {
        cout << "Not possible";
        return ;
    }

    // Create an array to store digits of result
    int res[m];

    // deduct sum by one to account for cases later
    // (There must be 1 left for the most significant
    //  digit)
    s -= 1;

    // Fill last m-1 digits (from right to left)
    for (int i=m-1; i>0; i--)
    {
        // If sum is still greater than 9,
        // digit must be 9.
        if (s > 9)
        {
            res[i] = 9;
            s -= 9;
        }
        else
        {
            res[i] = s;
            s = 0;
        }
    }

    // Whatever is left should be the most significant
    // digit.
    res[0] = s + 1;  // The initially subtracted 1 is
                     // incorporated here.

    cout << "Smallest number is ";
    for (int i=0; i<m; i++)
        cout << res[i];
}

// Driver code
int main()
{
    int s = 9, m = 2;
    findSmallest(m, s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest number that can be
// formed from given sum of digits and number of digits

class GFG
{
    // Function to print the smallest possible number with digit sum 's'
    // and 'm' number of digits
    static void findSmallest(int m, int s)
    {
        // If sum of digits is 0, then a number is possible
        // only if number of digits is 1
        if (s == 0)
        {
            System.out.print(m == 1 ? "Smallest number is 0" : "Not possible");

            return ;
        }

        // Sum greater than the maximum possible sum
        if (s > 9*m)
        {
            System.out.println("Not possible");
            return ;
        }

        // Create an array to store digits of result
        int[] res = new int[m];

        // deduct sum by one to account for cases later
        // (There must be 1 left for the most significant
        //  digit)
        s -= 1;

        // Fill last m-1 digits (from right to left)
        for (int i=m-1; i>0; i--)
        {
            // If sum is still greater than 9,
            // digit must be 9
            if (s > 9)
            {
                res[i] = 9;
                s -= 9;
            }
            else
            {
                res[i] = s;
                s = 0;
            }
        }

        // Whatever is left should be the most significant
        // digit
        res[0] = s + 1;  // The initially subtracted 1 is
                        // incorporated here

        System.out.print("Smallest number is ");
        for (int i=0; i<m; i++)
            System.out.print(res[i]);
    }

    // driver program
    public static void main (String[] args)
    {
        int s = 9, m = 2;
        findSmallest(m, s);
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Prints the smallest possible
# number with digit sum 's'
# and 'm' number of digits.

def findSmallest(m,s):

    # If sum of digits is 0,
    # then a number is possible
    # only if number of digits is 1.
    if (s == 0):

        if(m == 1) :
              print("Smallest number is 0")
        else :
              print("Not possible")
        return

    # Sum greater than the
    # maximum possible sum.
    if (s > 9*m):

        print("Not possible")
        return

    # Create an array to
    # store digits of result
    res=[0 for i in range(m+1)]

    # deduct sum by one to
    # account for cases later
    # (There must be 1 left
    # for the most significant
    #  digit)
    s -= 1

    # Fill last m-1 digits
    # (from right to left)
    for i in range(m-1,0,-1):

        # If sum is still greater than 9,
        # digit must be 9.
        if (s > 9):

            res[i] = 9
            s -= 9

        else:

            res[i] = s
            s = 0

    # Whatever is left should
    # be the most significant
    # digit.
    # The initially subtracted 1 is
    # incorporated here.
    res[0] = s + 1

    print("Smallest number is ",end="")
    for i in range(m):
        print(res[i],end="")

s = 9
m = 2
findSmallest(m, s)

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find the smallest
// number that can be formed from
// given sum of digits and number
// of digits
using System;

class GFG
{
    // Function to print the smallest
    // possible number with digit sum 's'
    // and 'm' number of digits
    static void findSmallest(int m, int s)
    {
        // If sum of digits is 0,
        // then a number is possible
        // only if number of digits is 1
        if (s == 0)
        {
            Console.Write(m == 1 ?
                          "Smallest number is 0" :
                                  "Not possible");

            return ;
        }

        // Sum greater than the
        // maximum possible sum
        if (s > 9 * m)
        {
            Console.Write("Not possible");
            return ;
        }

        // Create an array to
        // store digits of result
        int []res = new int[m];

        // deduct sum by one to account
        // for cases later (There must be
        // 1 left for the most significant
        // digit)
        s -= 1;

        // Fill last m-1 digits
        // (from right to left)
        for (int i = m - 1; i > 0; i--)
        {
            // If sum is still greater
            // than 9, digit must be 9
            if (s > 9)
            {
                res[i] = 9;
                s -= 9;
            }
            else
            {
                res[i] = s;
                s = 0;
            }
        }

        // Whatever is left should be
        // the most significant digit

        // The initially subtracted 1 is
        // incorporated here
        res[0] = s + 1;

        Console.Write("Smallest number is ");
        for (int i = 0; i < m; i++)
            Console.Write(res[i]);
    }

    // Driver Code
    public static void Main ()
    {
        int s = 9, m = 2;
        findSmallest(m, s);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the smallest
// number that can be formed from
// given sum of digits and number
// of digits.

// Prints the smallest possible
// number with digit sum 's'
// and 'm' number of digits.
function findSmallest($m, $s)
{
    // If sum of digits is 0, then
    // a number is possible only if
    // number of digits is 1.
    if ($s == 0)
    {
        if(($m == 1) == true)

        echo "Smallest number is " , 0;
        else
        echo "Not possible";
        return ;
    }

    // Sum greater than the
    // maximum possible sum.
    if ($s > 9 * $m)
    {
        echo "Not possible";
        return ;
    }

    // Create an array to store
    // digits of result int res[m];
    // deduct sum by one to account
    // for cases later (There must
    // be 1 left for the most
    // significant digit)
    $s -= 1;

    // Fill last m-1 digits
    // (from right to left)
    for ($i = $m - 1; $i > 0; $i--)
    {
        // If sum is still greater
        // than 9, digit must be 9.
        if ($s > 9)
        {
            $res[$i] = 9;
            $s -= 9;
        }
        else
        {
            $res[$i] = $s;
            $s = 0;
        }
    }

    // Whatever is left should be
    // the most significant digit.

    // The initially subtracted 1
    // is incorporated here.
    $res[0] = $s + 1;

    echo "Smallest number is ";
    for ($i = 0; $i < $m; $i++)
        echo $res[$i];
}

// Driver code
$s = 9; $m = 2;
findSmallest($m, $s);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find the smallest number that can be
// formed from given sum of digits and number of digits.

// Prints the smallest possible number with digit sum 's'
// and 'm' number of digits.
function findSmallest(m, s)
{
    // If sum of digits is 0, then a number is possible
    // only if number of digits is 1.
    if (s == 0)
    {
        (m == 1)? document.write("Smallest number is ") + 0
                : document.write("Not possible");
        return ;
    }

    // Sum greater than the maximum possible sum.
    if (s > 9*m)
    {
        document.write("Not possible");
        return ;
    }

    // Create an array to store digits of result
    let res = new Array(m);

    // deduct sum by one to account for cases later
    // (There must be 1 left for the most significant
    // digit)
    s -= 1;

    // Fill last m-1 digits (from right to left)
    for (let i=m-1; i>0; i--)
    {
        // If sum is still greater than 9,
        // digit must be 9.
        if (s > 9)
        {
            res[i] = 9;
            s -= 9;
        }
        else
        {
            res[i] = s;
            s = 0;
        }
    }

    // Whatever is left should be the most significant
    // digit.
    res[0] = s + 1; // The initially subtracted 1 is
                    // incorporated here.

    document.write("Smallest number is ");
    for (let i=0; i<m; i++)
        document.write(res[i]);
}

// Driver code

    let s = 9, m = 2;
    findSmallest(m, s);

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
Smallest number is 18
```

该解决方案的时间复杂度为 0(m)。
我们将很快讨论在给定位数和位数的情况下寻找最大可能数的方法。
本文由**瓦伊巴夫·阿加瓦尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息