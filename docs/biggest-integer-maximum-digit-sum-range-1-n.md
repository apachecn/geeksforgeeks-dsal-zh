# 最大整数，其最大位数和在 1 到 n 的范围内

> 原文:[https://www . geesforgeks . org/maximum-integer-maximum-digits-sum-range-1-n/](https://www.geeksforgeeks.org/biggest-integer-maximum-digit-sum-range-1-n/)

给定一个数 n，找到一个范围从 1 到 n 的数，使其和最大。如果有几个这样的整数，确定其中最大的**。**

****示例:****

```
Input:  n = 100
Output: 99  
99 is the largest number in range from
1 to 100 with maximum sum of digits.

Input: n = 48
Output: 48
Explanation: 
There are two numbers with maximum
digit sum. The numbers are 48 and 39
Since 48 > 39, it is our answer.
```

**一种**天真的**方法是对从 1 到 n 的所有数字进行迭代，找出哪个数字的数字和最大。这个解的时间复杂度是 O(n)。**

**一种有效的方法是从 n 迭代到 1。对当前数字的每个数字执行以下操作，如果该数字不为零，将其减少 1，并将所有其他数字更改为其右侧的 9。如果结果整数的位数总和严格大于当前答案的位数总和，则使用结果整数更新答案。如果结果整数之和与当前答案相同，则如果结果整数大于当前答案，则用结果整数更新当前答案。**

****如何减少一个数字，把它右边的其他所有数字都改成 9？**
让 x 成为我们当前的数字。我们可以用下面的公式找到当前数字的下一个数字。在下面的公式中，b 是 10 的幂，表示当前数字的位置。每次迭代后，我们把 x 减少到 x/10，把 b 变成 b * 10。
我们使用(x–1)* b+(b–1)；**

**这一行可以进一步解释为，如果数字是 x = 521，b = 1，那么**

*   **(521–1)* 1+(1-1)给你 520，这是我们需要做的事情，将位置号减少 1，将右边所有其他数字替换为 9。**
*   **在 x /= 10 给你 x 为 52，b*=10 给你 b 为 10 之后，再次执行为(52-1)*(10) + 9 给你 519，这就是我们要做的，将当前索引减少 1，所有其他权限增加 9。**

## **C++**

```
// CPP program to find the
// number with maximum digit
// sum.
#include <bits/stdc++.h>
using namespace std;

// function to calculate the 
// sum of digits of a number.
int sumOfDigits(int a)
{
    int sum = 0;
    while (a)
    {
        sum += a % 10;
        a /= 10;
    }
    return sum;
}

// Returns the maximum number
// with maximum sum of digits.
int findMax(int x)
{
    // initializing b as 1 and
    // initial max sum to be of n
    int b = 1, ans = x;

    // iterates from right to
    // left in a digit
    while (x)
    {

        // while iterating this
        // is the number from
        // from right to left
        int cur = (x - 1) * b + (b - 1);

        // calls the function to
        // check if sum of cur is
        // more then of ans
        if (sumOfDigits(cur) > sumOfDigits(ans) ||
           (sumOfDigits(cur) == sumOfDigits(ans) &&
            cur > ans))
            ans = cur;

        // reduces the number to one unit less
        x /= 10;
        b *= 10;
    }

    return ans;
}

// driver program
int main()
{
    int n = 521;
    cout << findMax(n);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find the
// number with maximum digit
// sum.
import java.io.*;

class GFG {

    // function to calculate the 
    // sum of digits of a number.  
    static int sumOfDigits(int a)
    {
        int sum = 0;
        while (a!=0)
        {
            sum += a % 10;
            a /= 10;
        }
        return sum;
    }

    // Returns the maximum number
    // with maximum sum of digits.
    static int findMax(int x)
    {
        // initializing b as 1 and
        // initial max sum to be of n
        int b = 1, ans = x;

        // iterates from right to
        // left in a digit
        while (x!=0)
        {

            // while iterating this
            // is the number from
            // from right to left
            int cur = (x - 1) * b + (b - 1);

            // calls the function to
            // check if sum of cur is
            // more then of ans
            if (sumOfDigits(cur) > sumOfDigits(ans) ||
            (sumOfDigits(cur) == sumOfDigits(ans) &&
                cur > ans))
                ans = cur;

            // reduces the number to one unit less
            x /= 10;
            b *= 10;
        }

        return ans;
    }

    // driver program
    public static void main (String[] args)
    {
        int n = 521;
        System.out.println(findMax(n));
    }
}

/*This article is contributed by Nikita Tiwari.*/
```

## **蟒蛇 3**

```
# Python 3 program to
# find the number
# with maximum digit
# sum.

# function to calculate
# the sum of digits of
# a number.
def sumOfDigits(a) :
    sm = 0
    while (a!=0) :
        sm = sm + a % 10
        a = a // 10

    return sm

# Returns the maximum number
# with maximum sum of digits.
def findMax(x) :

    # initializing b as 1
    # and initial max sum
    # to be of n
    b = 1
    ans = x

    # iterates from right
    # to left in a digit
    while (x!=0) :
        # while iterating this
        # is the number from
        # right to left
        cur = (x - 1) * b + (b - 1)

        # calls the function to
        # check if sum of cur is
        # more then of ans
        if (sumOfDigits(cur) > sumOfDigits(ans) or
        (sumOfDigits(cur) == sumOfDigits(ans) and
            cur > ans)) :
                ans = cur

        # reduces the number
        # to one unit less
        x =x // 10
        b = b * 10

    return ans

# driver program to test the above function
n = 521
print(findMax(n))

# This article is contributed by Nikita Tiwari.
```

## **C#**

```
// C# program to find the number
// with maximum digit sum.
using System;

class GFG {

    // function to calculate the 
    // sum of digits of a number.  
    static int sumOfDigits(int a)
    {
        int sum = 0;
        while (a!=0)
        {
            sum += a % 10;
            a /= 10;
        }
        return sum;
    }

    // Returns the maximum number
    // with maximum sum of digits.
    static int findMax(int x)
    {
        // initializing b as 1 and
        // initial max sum to be of n
        int b = 1, ans = x;

        // iterates from right to
        // left in a digit
        while (x!=0)
        {

            // while iterating this
            // is the number from
            // from right to left
            int cur = (x - 1) * b + (b - 1);

            // calls the function to
            // check if sum of cur is
            // more then of ans
            if (sumOfDigits(cur) > sumOfDigits(ans) ||
               (sumOfDigits(cur) == sumOfDigits(ans) &&
                                            cur > ans))
                ans = cur;

            // reduces the number to one unit less
            x /= 10;
            b *= 10;
        }

        return ans;
    }

    // driver program
    public static void Main()
    {
        int n = 521;
        Console.WriteLine(findMax(n));
    }
}

// This article is contributed by Anant Agarwal.
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP program to find the
// number with maximum digit
// sum.

// function to calculate the
// sum of digits of a number.
function sumOfDigits($a)
{
    $sum = 0;
    while ($a)
    {
        $sum += $a % 10;
        $a = (int)$a / 10;
    }
    return $sum;
}

// Returns the maximum number
// with maximum sum of digits.
function findMax( $x)
{
    // initializing b as 1 and
    // initial max sum to be of n
    $b = 1; $ans = $x;

    // iterates from right to
    // left in a digit
    while ($x)
    {

        // while iterating this
        // is the number from
        // from right to left
        $cur = ($x - 1) * $b +
                     ($b - 1);

        // calls the function to
        // check if sum of cur is
        // more then of ans
        if (sumOfDigits($cur) > sumOfDigits($ans) ||
           (sumOfDigits($cur) == sumOfDigits($ans) &&
                                        $cur > $ans))
            $ans = $cur;

        // reduces the number
        // to one unit less
        $x = (int)$x / 10;
        $b *= 10;
    }

    return $ans;
}

// Driver Code
$n = 521;
echo findMax($n);

// This code is contributed by ajit
?>
```

## **java 描述语言**

```
<script>

// Javascript program to find the
// number with maximum digit
// sum.

// Function to calculate the
// sum of digits of a number.
function sumOfDigits(a)
{
    var sum = 0;
    while (a != 0)
    {
        sum += a % 10;
        a = parseInt(a / 10);
    }
    return sum;
}

// Returns the maximum number
// with maximum sum of digits.
function findMax(x)
{

    // Initializing b as 1 and
    // initial max sum to be of n
    var b = 1, ans = x;

    // Iterates from right to
    // left in a digit
    while (x != 0)
    {

        // While iterating this
        // is the number from
        // from right to left
        var cur = (x - 1) * b + (b - 1);

        // Calls the function to
        // check if sum of cur is
        // more then of ans
        if (sumOfDigits(cur) >
            sumOfDigits(ans) ||
           (sumOfDigits(cur) ==
            sumOfDigits(ans) &&
            cur > ans))
            ans = cur;

        // Reduces the number to one unit less
        x = parseInt(x / 10);
        b *= 10;
    }
    return ans;
}

// Driver Code
var n = 521;

document.write(findMax(n));

// This code is contributed by todaysgaurav

</script>
```

****输出:****

```
499
```

****时间复杂度:** O(m)，其中 m 为 n 中的位数。**

**本文由 [**奋斗者**](https://www.facebook.com/raja.vikramaditya.7) 投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。**