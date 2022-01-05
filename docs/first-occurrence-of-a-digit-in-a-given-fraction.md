# 给定分数中数字的第一次出现

> 原文:[https://www . geesforgeks . org/给定分数中第一个出现的数字/](https://www.geeksforgeeks.org/first-occurrence-of-a-digit-in-a-given-fraction/)

给定三个整数 a、b 和 c，求 c 在 a/b 中小数点后的第一次出现。如果不存在，请打印-1。
示例:

```
Input : a = 2 b = 3 c = 6 
Output : 1 
Explanation: 
0.666666.. so 6 occurs at first place 
of a/b after decimal point

Input : a = 1 b = 4 c = 5 
Output : 2 
Explanation: 
1 / 4 = 0.25 which gives 5's position
to be 2.
```

一种**天真的方法**是执行除法并保留小数部分，然后迭代并检查给定的数字是否存在。当进行 2/3 等除法运算时，这种方法效果不好，因为它会产生 0.66666666，但在编程语言中，它会将其舍入到 0.66667，因此我们会得到一个 7，这在原始的 a/b
中是不存在的。一种有效的方法**将是数学方法**，如果我们将每次 a 乘以 b 并乘以 10，我们每次都会得到小数部分之后的整数。所需的调制次数将为 b，因为小数点后最多有 b 个整数。因此，我们将其与 c 进行比较，如果存在的话，就可以得到我们想要的值。
以下是上述方法的实施:

## C++

```
// CPP program to find first occurrence
// of c in a/b
#include <bits/stdc++.h>
using namespace std;

// function to print the first digit
int first(int a, int b, int c)
{
    // reduce the number to its mod
    a %= b;

    // traverse for every decimal places
    for (int i = 1; i <= b; i++)
    {
        // get every fraction places
        // when (a*10/b)/c
        a = a * 10;

        // check if it is equal to
        // the required integer
        if (a / b == c)
            return i;

        // mod the number
        a %= b;
    }
    return -1;
}

// driver program to test the above function
int main()
{
    int a = 1, b = 4, c = 5;
    cout << first(a, b, c);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find first occurrence
// of c in a/b
import java.util.*;
import java.lang.*;

public class GfG{
    // Function to print the first digit
    public static int first(int a, int b, int c)
    {
        // Reduce the number to its mod
        a %= b;

        // Traverse for every decimal places
        for (int i = 1; i <= b; i++)
        {
            // Get every fraction places
            // when (a*10/b)/c
            a = a * 10;

            // Check if it is equal to
            // the required integer
            if (a / b == c)
                return i;

            // Mod the number
            a %= b;
        }
        return -1;
    }

    // Driver function
    public static void main(String argc[]){
        int a = 1, b = 4, c = 5;
        System.out.println(first(a, b, c));
    }

}
/* This code is contributed by Sagar Shukla */
```

## 蟒蛇 3

```
# Python3 program to find first occurrence
# of c in a/b

# function to print the first digit
def first( a , b , c ):

    # reduce the number to its mod
    a %= b

    # traverse for every decimal places
    for i in range(1, b + 1):

        # get every fraction places
        # when (a*10/b)/c
        a = a * 10

        # check if it is equal to
        # the required integer
        if int(a / b) == c:
            return i

        # mod the number
        a %= b

    return -1

# driver code to test the above function
a = 1
b = 4
c = 5
print(first(a, b, c))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find first occurrence
// of c in a/b
using System;

public class GfG{

    // Function to print the first digit
    public static int first(int a, int b, int c)
    {

        // Reduce the number to its mod
        a %= b;

        // Traverse for every decimal places
        for (int i = 1; i <= b; i++)
        {

            // Get every fraction places
            // when (a*10/b)/c
            a = a * 10;

            // Check if it is equal to
            // the required integer
            if (a / b == c)
                return i;

            // Mod the number
            a %= b;
        }

        return -1;
    }

    // Driver function
    public static void Main() {

        int a = 1, b = 4, c = 5;

        Console.WriteLine(first(a, b, c));
    }
}

/* This code is contributed by vt_m */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find first
// occurrence of c in a/b

// function to print
// the first digit
function first( $a, $b, $c)
{

    // reduce the number
    // to its mod
    $a %= $b;

    // traverse for every
    // decimal places
    for ($i = 1; $i <= $b; $i++)
    {

        // get every fraction places
        // when (a*10/b)/c
        $a = $a * 10;

        // check if it is equal to
        // the required integer
        if ($a / $b == $c)
            return $i;

        // mod the number
        $a %= $b;
    }
    return -1;
}

    // Driver Code
    $a = 1; $b = 4; $c = 5;
    echo first($a, $b, $c);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find first occurrence
// of c in a/b

    // Function to print the first digit
    function first(a, b, c)
    {
        // Reduce the number to its mod
        a %= b;

        // Traverse for every decimal places
        for (let i = 1; i <= b; i++)
        {
            // Get every fraction places
            // when (a*10/b)/c
            a = a * 10;

            // Check if it is equal to
            // the required integer
            if (a / b == c)
                return i;

            // Mod the number
            a %= b;
        }
        return -1;
    }

// Driver Code

        let a = 1, b = 4, c = 5;
         document.write(first(a, b, c));

// This code is contributed by chinmoy1997pal.
</script>
```

输出:

```
2
```