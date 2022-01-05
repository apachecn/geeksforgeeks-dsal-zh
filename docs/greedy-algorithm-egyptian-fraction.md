# 埃及分数的贪婪算法

> 原文:[https://www . geesforgeks . org/greedy-algorithm-Egyptian-fraction/](https://www.geeksforgeeks.org/greedy-algorithm-egyptian-fraction/)

每个正分数可以表示为唯一单位分数的和。如果分子是 1，分母是正整数，分数就是单位分数，例如 1/3 就是单位分数。这种表示被称为埃及分数，因为它被古埃及人使用。
以下是几个例子:

```
Egyptian Fraction Representation of 2/3 is 1/2 + 1/6
Egyptian Fraction Representation of 6/14 is 1/3 + 1/11 + 1/231
Egyptian Fraction Representation of 12/13 is 1/2 + 1/3 + 1/12 + 1/156
```

我们可以使用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms-set-1-activity-selection-problem/)生成埃及分数。对于给定数量的形式‘NR/dr’，其中 dr > nr，首先找到最大可能的单位分数，然后对剩余部分重复。例如，考虑 6/14，我们首先找到 14/6 的上限，即 3。所以第一个单位分数变成 1/3，然后重复(6/14–1/3)，即 4/42。
以下是上述想法的实现。

## C++

```
// C++ program to print a fraction in Egyptian Form using Greedy
// Algorithm
#include <iostream>
using namespace std;

void printEgyptian(int nr, int dr)
{
    // If either numerator or denominator is 0
    if (dr == 0 || nr == 0)
        return;

    // If numerator divides denominator, then simple division
    // makes the fraction in 1/n form
    if (dr%nr == 0)
    {
        cout << "1/" << dr/nr;
        return;
    }

    // If denominator divides numerator, then the given number
    // is not fraction
    if (nr%dr == 0)
    {
        cout << nr/dr;
        return;
    }

    // If numerator is more than denominator
    if (nr > dr)
    {
        cout << nr/dr << " + ";
        printEgyptian(nr%dr, dr);
        return;
    }

    // We reach here dr > nr and dr%nr is non-zero
    // Find ceiling of dr/nr and print it as first
    // fraction
    int n = dr/nr + 1;
    cout << "1/" << n << " + ";

    // Recur for remaining part
    printEgyptian(nr*n-dr, dr*n);
 }

// Driver Program
int main()
{
    int nr = 6, dr = 14;
    cout << "Egyptian Fraction Representation of "
         << nr << "/" << dr << " is\n ";
    printEgyptian(nr, dr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to print a fraction
// in Egyptian Form using Greedy
// Algorithm

class GFG {

    static void printEgyptian(int nr, int dr) {
        // If either numerator or
        // denominator is 0
        if (dr == 0 || nr == 0) {
            return;
        }

        // If numerator divides denominator,
        // then simple division makes
        // the fraction in 1/n form
        if (dr % nr == 0) {
            System.out.print("1/" + dr / nr);
            return;
        }

        // If denominator divides numerator,
        // then the given number is not fraction
        if (nr % dr == 0) {
            System.out.print(nr / dr);
            return;
        }

        // If numerator is more than denominator
        if (nr > dr) {
            System.out.print(nr / dr + " + ");
            printEgyptian(nr % dr, dr);
            return;
        }

        // We reach here dr > nr and dr%nr
        // is non-zero. Find ceiling of
        // dr/nr and print it as first
        // fraction
        int n = dr / nr + 1;
        System.out.print("1/" + n + " + ");

        // Recur for remaining part
        printEgyptian(nr * n - dr, dr * n);
    }

// Driver Code
    public static void main(String[] args) {
        int nr = 6, dr = 14;
        System.out.print("Egyptian Fraction Representation of "
                + nr + "/" + dr + " is\n ");
        printEgyptian(nr, dr);
    }
}

/*This code is contributed by Rajput-Ji*/
```

## 蟒蛇 3

```
# Python3 program to print a fraction
# in Egyptian Form using Greedy
# Algorithm

# import math package to use
# ceiling function
import math

# define a function egyptianFraction
# which receive parameter nr as
# numerator and dr as denominator
def egyptianFraction(nr, dr):

    print("The Egyptian Fraction " +
          "Representation of {0}/{1} is".
                format(nr, dr), end="\n")

    # empty list ef to store
    # denominator
    ef = []

    # while loop runs until
    # fraction becomes 0 i.e,
    # numerator becomes 0
    while nr != 0:

        # taking ceiling
        x = math.ceil(dr / nr)

        # storing value in ef list
        ef.append(x)

        # updating new nr and dr
        nr = x * nr - dr
        dr = dr * x

    # printing the values
    for i in range(len(ef)):
        if i != len(ef) - 1:
            print(" 1/{0} +" .
                    format(ef[i]), end = " ")
        else:
            print(" 1/{0}" .
                    format(ef[i]), end = " ")

# calling the function
egyptianFraction(6, 14)

# This code is contributed
# by Anubhav Raj Singh
```

## C#

```
// C# program to print a fraction
// in Egyptian Form using Greedy
// Algorithm
using System;

class GFG
{
static void printEgyptian(int nr, int dr)
{
    // If either numerator or
    // denominator is 0
    if (dr == 0 || nr == 0)
        return;

    // If numerator divides denominator,
    // then simple division  makes
    // the fraction in 1/n form
    if (dr % nr == 0)
    {
        Console.Write("1/" + dr / nr);
        return;
    }

    // If denominator divides numerator,
    // then the given number is not fraction
    if (nr % dr == 0)
    {
        Console.Write(nr / dr);
        return;
    }

    // If numerator is more than denominator
    if (nr > dr)
    {
        Console.Write(nr / dr + " + ");
        printEgyptian(nr % dr, dr);
        return;
    }

    // We reach here dr > nr and dr%nr
    // is non-zero. Find ceiling of
    // dr/nr and print it as first
    // fraction
    int n = dr / nr + 1;
    Console.Write("1/" + n + " + ");

    // Recur for remaining part
    printEgyptian(nr * n - dr, dr * n);
}

// Driver Code
public static void Main()
{
    int nr = 6, dr = 14;
    Console.Write( "Egyptian Fraction Representation of " +
                                 nr + "/" + dr + " is\n ");
    printEgyptian(nr, dr);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print a fraction
// in Egyptian Form using Greedy
// Algorithm

function printEgyptian($nr, $dr)
{
    // If either numerator or
    // denominator is 0
    if ($dr == 0 || $nr == 0)
        return;

    // If numerator divides denominator,
    // then simple division makes the
    // fraction in 1/n form
    if ($dr % $nr == 0)
    {
        echo "1/", (int)$dr / $nr;
        return;
    }

    // If denominator divides numerator,
    // then the given number is not fraction
    if ($nr%$dr == 0)
    {
        echo (int)($nr / $dr);
        return;
    }

    // If numerator is more than denominator
    if ($nr > $dr)
    {
        echo (int)($nr/$dr), " + ";
        printEgyptian($nr % $dr, $dr);
        return;
    }

    // We reach here dr > nr and dr%nr is
    // non-zero. Find ceiling of dr/nr and
    // print it as first fraction
    $n = (int)($dr / $nr ) + 1;
    echo "1/" , $n , " + ";

    // Recur for remaining part
    printEgyptian($nr * $n - $dr, $dr * $n);
}

// Driver Code
$nr = 6;
$dr = 14;
echo "Egyptian Fraction Representation of ",
                    $nr, "/", $dr, " is\n ";
printEgyptian($nr, $dr);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript program to print a fraction
    // in Egyptian Form using Greedy
    // Algorithm

    function printEgyptian(nr, dr)
    {
        // If either numerator or
        // denominator is 0
        if (dr == 0 || nr == 0)
            return;

        // If numerator divides denominator,
        // then simple division  makes
        // the fraction in 1/n form
        if (dr % nr == 0)
        {
            document.write("1/" + parseInt(dr / nr, 10));
            return;
        }

        // If denominator divides numerator,
        // then the given number is not fraction
        if (nr % dr == 0)
        {
            document.write(parseInt(nr / dr, 10));
            return;
        }

        // If numerator is more than denominator
        if (nr > dr)
        {
            document.write(parseInt(nr / dr, 10) + " + ");
            printEgyptian(nr % dr, dr);
            return;
        }

        // We reach here dr > nr and dr%nr
        // is non-zero. Find ceiling of
        // dr/nr and print it as first
        // fraction
        let n = parseInt(dr / nr, 10) + 1;
        document.write("1/" + n + " + ");

        // Recur for remaining part
        printEgyptian(nr * n - dr, dr * n);
    }

      let nr = 6, dr = 14;
    document.write( "Egyptian Fraction Representation of " + nr + "/" + dr + " is\n ");
    printEgyptian(nr, dr);

// This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
Egyptian Fraction Representation of 6/14 is
 1/3 + 1/11 + 1/231 
```

贪婪算法之所以有效，是因为分数总是被简化成分母大于分子，分子不除分母的形式。对于这种简化形式，突出显示的递归调用是针对简化的分子进行的。所以递归调用继续减少分子，直到它达到 1。

参考文献:
[http://www . mathematics . surrey . AC . uk/hosted-sites/R .克诺特/Fractions/Egyptian . html](http://www.maths.surrey.ac.uk/hosted-sites/R.Knott/Fractions/egyptian.html)
本文由**舒巴姆**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。