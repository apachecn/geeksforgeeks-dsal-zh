# 巧克力和包装纸拼图程序

> 原文:[https://www . geesforgeks . org/program-巧克力-包装纸-拼图/](https://www.geeksforgeeks.org/program-chocolate-wrapper-puzzle/)

给定以下三个值，任务是找到你能吃的最大巧克力总数。

1.  钱:买巧克力的钱
2.  价格:一块巧克力的价格
3.  包装:多拿一块巧克力需要退回的包装数量。

可以假设所有给定值都是大于 1 的正整数。
**例:**

```
Input: money = 16, price = 2, wrap = 2
Output:   15
Price of a chocolate is 2\. You can buy 8 chocolates from
amount 16\. You can return 8 wrappers back and get 4 more
chocolates. Then you can return 4 wrappers and get 2 more
chocolates. Finally you can return 2 wrappers to get 1
more chocolate.

Input:   money = 15, price = 1, wrap = 3
Output:   22
We buy and eat 15 chocolates
We return 15 wrappers and get 5 more chocolates.
We return 3 wrappers, get 1 chocolate and eat it
(keep 2 wrappers). Now we have 3 wrappers. Return
3 and get 1 more chocolate.
So total chocolates = 15 + 5 + 1 + 1

Input:  money = 20, price = 3, wrap = 5
Output:   7
```

来源:[拼图 22 |(最多巧克力)](https://www.geeksforgeeks.org/puzzle-22-maximum-chocolates/)

一种**天真的方法**是通过返回包装纸来连续计算巧克力的数量，直到剩下的包装纸没有变得少于获得巧克力所需的数量。

下面是这个方法的实现。

## C++

```
// Recursive C++ program to find maximum
// number of chocolates
#include <iostream>
using namespace std;

// Returns number of chocolates we can
// have from given number of chocolates
// and number of wrappers required to
// get a chocolate.
int countRec(int choc, int wrap)
{
    // If number of chocolates is less than
    // number of wrappers required.
    if (choc < wrap)
        return 0;

    // We can immediately get newChoc using
    // wrappers of choc.
    int newChoc = choc/wrap;

    // Now we have "newChoc + choc%wrap" wrappers.
    return newChoc + countRec(newChoc + choc%wrap,
                              wrap);
}

// Returns maximum number of chocolates we can eat
// with given money, price of chocolate and number
// of wrappers required to get a chocolate.
int countMaxChoco(int money, int price, int wrap)
{
    // We can directly buy below number of chocolates
    int choc = money/price;

    // countRec returns number of chocolates we can
    // have from given number of chocolates
    return choc + countRec(choc, wrap);
}

// Driver code
int main()
{
    int money = 15 ; // total money
    int price = 1; // cost of each candy
    int wrap = 3 ; // no of wrappers needs to be
    // exchanged for one chocolate.

    cout << countMaxChoco(money, price, wrap);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive java program to find maximum
// number of chocolates

import java.io.*;

class GFG {

    // Returns number of chocolates we can
    // have from given number of chocolates
    // and number of wrappers required to
    // get a chocolate.
    static int countRec(int choc, int wrap)
    {

        // If number of chocolates is less than
        // number of wrappers required.
        if (choc < wrap)
            return 0;

        // We can immediately get newChoc using
        // wrappers of choc.
        int newChoc = choc / wrap;

        // Now we have "newChoc + choc%wrap"
        // wrappers.
        return newChoc + countRec(newChoc +
                          choc % wrap, wrap);
    }

    // Returns maximum number of chocolates
    // we can eat with given money, price of
    // chocolate and number of wrappers
    // required to get a chocolate.
    static int countMaxChoco(int money,
                          int price, int wrap)
    {

        // We can directly buy below number of
        // chocolates
        int choc = money/price;

        // countRec returns number of chocolates
        // we can have from given number of
        // chocolates
        return choc + countRec(choc, wrap);
    }

    // Driver code
    public static void main (String[] args)
    {
        int money = 15 ; // total money
        int price = 1; // cost of each candy

        // no of wrappers needs to be
        // exchanged for one chocolate.
        int wrap = 3 ;
        System.out.println(
            countMaxChoco(money, price, wrap));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Recursive Python3 program to find
# maximum number of chocolates
import math

# Returns number of chocolates we can
# have from given number of chocolates
# and number of wrappers required to
# get a chocolate.
def countRec(choc, wrap):

    # If number of chocolates is less
    # than number of wrappers required.
    if (choc < wrap):
        return 0;

    # We can immediately get newChoc
    # using wrappers of choc.
    newChoc = choc / wrap;

    # Now we have "newChoc + choc%wrap" wrappers.
    return newChoc + countRec(newChoc + choc %
                                  wrap, wrap);

# Returns maximum number of chocolates
# we can eat with given money, price
# of chocolate and number of wrappers
# required to get a chocolate.
def countMaxChoco(money, price, wrap):

    # We can directly buy below
    # number of chocolates
    choc = money / price;

    # countRec returns number
    # of chocolates we can
    # have from given number
    # of chocolates
    return math.floor(choc + countRec(choc, wrap));

# Driver code

# total money
money = 15;

# cost of each candy
price = 1;

# no of wrappers needs to be
wrap = 3 ;

# exchanged for one chocolate.
print(countMaxChoco(money, price, wrap));

# This code is contributed by mits
```

## C#

```
// Recursive C# program to find maximum
// number of chocolates

using System;

class GFG {

    // Returns number of chocolates we can
    // have from given number of chocolates
    // and number of wrappers required to
    // get a chocolate.
    static int countRec(int choc, int wrap)
    {

        // If number of chocolates is less than
        // number of wrappers required.
        if (choc < wrap)
            return 0;

        // We can immediately get newChoc using
        // wrappers of choc.
        int newChoc = choc / wrap;

        // Now we have "newChoc + choc%wrap"
        // wrappers.
        return newChoc + countRec(newChoc +
                        choc % wrap, wrap);
    }

    // Returns maximum number of chocolates
    // we can eat with given money, price of
    // chocolate and number of wrappers
    // required to get a chocolate.
    static int countMaxChoco(int money,
                        int price, int wrap)
    {

        // We can directly buy below number of
        // chocolates
        int choc = money/price;

        // countRec returns number of chocolates
        // we can have from given number of
        // chocolates
        return choc + countRec(choc, wrap);
    }

    // Driver code
    public static void Main ()
    {
        int money = 15 ; // total money
        int price = 1; // cost of each candy

        // no of wrappers needs to be
        // exchanged for one chocolate.
        int wrap = 3 ;
        Console.WriteLine(
            countMaxChoco(money, price, wrap));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Recursive PHP program to find maximum
// number of chocolates

// Returns number of chocolates we can
// have from given number of chocolates
// and number of wrappers required to
// get a chocolate.
function countRec($choc, $wrap)
{

    // If number of chocolates is less than
    // number of wrappers required.
    if ($choc < $wrap)
        return 0;

    // We can immediately get newChoc using
    // wrappers of choc.
    $newChoc = $choc/$wrap;

    // Now we have "newChoc + choc%wrap" wrappers.
    return $newChoc + countRec($newChoc + $choc % $wrap,
                                                  $wrap);
}

// Returns maximum number of chocolates we can eat
// with given money, price of chocolate and number
// of wrappers required to get a chocolate.
function countMaxChoco($money, $price, $wrap)
{

    // We can directly buy below
    // number of chocolates
    $choc = $money/$price;

    // countRec returns number
    // of chocolates we can
    // have from given number
    // of chocolates
    return floor($choc + countRec($choc, $wrap));
}

    // Driver code
    // total money
    $money = 15;

    // cost of each candy
    $price = 1;

    // no of wrappers needs to be
    $wrap = 3 ;

    // exchanged for one chocolate.
    echo countMaxChoco($money, $price, $wrap);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find maximum
// number of chocolates

// Returns number of chocolates we can
    // have from given number of chocolates
    // and number of wrappers required to
    // get a chocolate.
    function countRec(choc, wrap)
    {

        // If number of chocolates is less than
        // number of wrappers required.
        if (choc < wrap)
            return 0;

        // We can immediately get newChoc using
        // wrappers of choc.
        let newChoc = choc / wrap;

        // Now we have "newChoc + choc%wrap"
        // wrappers.
        return newChoc + countRec(newChoc +
                          choc % wrap, wrap);
    }

    // Returns maximum number of chocolates
    // we can eat with given money, price of
    // chocolate and number of wrappers
    // required to get a chocolate.
    function countMaxChoco(money,
                          price, wrap)
    {

        // We can directly buy below number of
        // chocolates
        let choc = money/price;

        // countRec returns number of chocolates
        // we can have from given number of
        // chocolates
        return choc + countRec(choc, wrap);
    }

// Driver code
          let money = 15 ; // total money
        let price = 1; // cost of each candy

        // no of wrappers needs to be
        // exchanged for one chocolate.
        let wrap = 3 ;
        document.write(Math.floor(
            countMaxChoco(money, price, wrap)));

</script>
```

**输出:**

```
22
```

一个**有效的解决方法**是用一个直接的公式来求巧克力的数量。

```
Find initial number of chocolates by
dividing the amount with per piece cost.
i.e. choc = money / price

then apply below formula
choc += (choc - 1)/(wrap - 1)
```

在上面天真的实现中，我们注意到在找到巧克力的初始数量后，我们递归地将巧克力的数量除以所需的包装数量。直到我们带着一块巧克力或包装纸离开。
我们正在重新计算值(即(choc/wrap + choc%wrap)/wrap，直到得到 1。
据观察，我们只需将巧克力和包装纸的值减 1，然后除以即可得到结果 **(choc-1)/(包装纸-1)**

下面是上述方法的实现:

## C++

```
// Efficient C++ program to find maximum
// number of chocolates
#include <iostream>
using namespace std;

// Returns maximum number of chocolates we can eat
// with given money, price of chocolate and number
// of wrapprices required to get a chocolate.
int countMaxChoco(int money, int price, int wrap)
{
    // Corner case
    if (money < price)
       return 0;

    // First find number of chocolates that
    // can be purchased with the given amount
    int choc = money / price;

    // Now just add number of chocolates with the
    // chocolates gained by wrapprices
    choc = choc + (choc - 1) / (wrap - 1);
    return choc;
}

// Driver code
int main()
{
    int money = 15 ; // total money
    int price = 1; // cost of each candy
    int wrap = 3 ; // no of wrappers needs to be
    // exchanged for one chocolate.

    cout << countMaxChoco(money, price, wrap);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to find maximum
// number of chocolates
import java.io.*;

class GFG {

    // Returns maximum number of chocolates
    // we can eat with given money, price
    // of chocolate and number of wrapprices
    // required to get a chocolate.
    static int countMaxChoco(int money,
                        int price, int wrap)
    {

        // Corner case
        if (money < price)
            return 0;

        // First find number of chocolates
        // that can be purchased with the
        // given amount
        int choc = money / price;

        // Now just add number of chocolates
        // with the chocolates gained by
        // wrapprices
        choc = choc + (choc - 1) / (wrap - 1);
        return choc;
    }

    // Driver code
    public static void main (String[] args)
    {

        // total money
        int money = 15;

        // cost of each candy
        int price = 1;

        // no of wrappers needs to be
        int wrap = 3 ;

        // exchanged for one chocolate.
        System.out.println(
           countMaxChoco(money, price, wrap));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Efficient Python3 program to find
# maximum number of chocolates

# Returns maximum number of
# chocolates we can eat with
# given money, price of chocolate
# and number of wrapprices
# required to get a chocolate.
def countMaxChoco(money, price, wrap) :

    # Corner case
    if (money < price) :
        return 0

    # First find number of chocolates
    # that can be purchased with the
    # given amount
    choc = int(money / price)

    # Now just add number of
    # chocolates with the chocolates
    # gained by wrapprices
    choc = choc + (choc - 1) / (wrap - 1)
    return int(choc )

# Driver code
money = 15 # total money
price = 1 # cost of each candy
wrap = 3 # no of wrappers needs to be
         # exchanged for one chocolate.

print(countMaxChoco(money, price, wrap))

# This code is contributed by Smitha
```

## C#

```
// Efficient C# program to find maximum
// number of chocolates
using System;

class GFG {

    // Returns maximum number of chocolates
    // we can eat with given money, price
    // of chocolate and number of wrapprices
    // required to get a chocolate.
    static int countMaxChoco(int money,
                        int price, int wrap)
    {

        // Corner case
        if (money < price)
            return 0;

        // First find number of chocolates
        // that can be purchased with the
        // given amount
        int choc = money / price;

        // Now just add number of chocolates
        // with the chocolates gained by
        // wrapprices
        choc = choc + (choc - 1) / (wrap - 1);
        return choc;
    }

    // Driver code
    public static void Main ()
    {

        // total money
        int money = 15;

        // cost of each candy
        int price = 1;

        // no of wrappers needs to be
        int wrap = 3 ;

        // exchanged for one chocolate.
        Console.WriteLine(
        countMaxChoco(money, price, wrap));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP program to find maximum
// number of chocolates

// Returns maximum number
// of chocolates we can eat
// with given money, price
// of chocolate and number
// of wrapprices required
// to get a chocolate.
function countMaxChoco($money, $price, $wrap)
{
    // Corner case
    if ($money < $price)
    return 0;

    // First find number
    // of chocolates that
    // can be purchased
    // with the given amount
    $choc = $money / $price;

    // Now just add number
    // of chocolates with the
    // chocolates gained by wrapprices
    $choc = $choc + ($choc - 1) /
                    ($wrap - 1);
    return $choc;
}

    // Driver code

     // total money
    $money = 15 ;

    // cost of each candy
    $price = 1;

    // no of wrappers needs to be
    // exchanged for one chocolate.
    $wrap = 3 ;
    echo countMaxChoco($money, $price, $wrap);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Efficient Javascript program to find maximum
// number of chocolates

// Returns maximum number of chocolates
// we can eat with given money, price
// of chocolate and number of wrapprices
// required to get a chocolate.
function countMaxChoco(money, price, wrap)
{

    // Corner case
    if (money < price)
        return 0;

    // First find number of chocolates
    // that can be purchased with the
    // given amount
    let choc = parseInt(money / price, 10);

    // Now just add number of chocolates
    // with the chocolates gained by
    // wrapprices
    choc = choc + parseInt((choc - 1) /
                           (wrap - 1), 10);
    return choc;
}

// Driver code

// Total money
let money = 15;

// Cost of each candy
let price = 1;

// No of wrappers needs to be
let wrap = 3;

// Exchanged for one chocolate.
document.write(countMaxChoco(money, price, wrap));

// This code is contributed by divyesh072019

</script>
```

**输出:**

```
22
```

本文由 [**萨希尔·查布拉(akku)**](https://practice.geeksforgeeks.org/user-profile.php?user=sahil_coder) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。