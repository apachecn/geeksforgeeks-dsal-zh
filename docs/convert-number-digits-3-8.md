# 转换为数字只有 3 和 8 的数字

> 原文:[https://www.geeksforgeeks.org/convert-number-digits-3-8/](https://www.geeksforgeeks.org/convert-number-digits-3-8/)

迷人的数字是由 3 和 8 组成的数字。给我们一个 n 位数，你总共有三个操作:

1.  给定数字加 1。
2.  给定数字减 1。
3.  选择一个数字并用任何其他需要的数字替换它。

我们需要找到操作的总数来把给定的数变成迷人的数。
示例:

```
Input : num = 343
Output : Minimum Operation = 1

Input : num = 88
Output : Minimum operation = 0
```

在找到合适的解决方案之前，让我们仔细看看给定的操作。

1.  给定的数字加 1，它将计数 1 操作，它能做的是将最后一个数字加 1，除非它是 9，如果最后一个数字是 9，那么它也将改变最后一个数字之前的数字。所以在最好的情况下，如果最后一个数字是 2 或 7，这个操作将把它们变成 3 或 8，代价是 1 个操作。
2.  给定数字减去 1，也将把 1 算作运算，并且只减少最后一个数字，除非它是 0。所以在最好的情况下，如果最后一个数字是 4 或 9，这个操作会以 1 次操作的代价将它们变成 3 或 8。
3.  选择任意一个数字并改变其值将被视为一次操作，但它肯定会将数字变成迷人的数字，即 3 或 8。因此，在最好和最坏的情况下，该操作将同时改变一个位数。

所以，对于求最小运算来说，加法和减法对我们没有用，只有不等于 3 或 8 的位数会被选择和改变。所以，总数不等于 3 或 8 的数字将是我们的答案。

## C++

```
// CPP to find min operations required to
// convert into charming number
#include <bits/stdc++.h>
using namespace std;

// function for minimum operation
int minOp(long long int num)
{
    // remainder and operations count
    int rem;
    int count = 0;

    // count digits not equal to 3 or 8
    while (num) {
        rem = num % 10;
        if (!(rem == 3 || rem == 8))
            count++;
        num /= 10;
    }
    return count;
}

// driver function
int main()
{
    long long int num = 234198;
    cout << "Minimum Operations =" << minOp(num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java to find min operations required to
// convert into charming number
class GFG
{

    // function for minimum operation
    static int minOp(int num)
    {

        // remainder and operations count
        int rem;
        int count = 0;

        // count digits not equal to 3 or 8
        while (num>0) {
            rem = num % 10;
            if (!(rem == 3 || rem == 8))
                count++;
            num /= 10;
        }

        return count;
    }

    // Driver code
    public static void main (String[] args)
    {
        int num = 234198;

        System.out.print("Minimum Operations ="+minOp(num));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python to find min
# operations required to
# convert into charming number

# function for minimum operation
def minOp(num):

    # remainder and operations count
    count = 0

    #count digits not equal to 3 or 8
    while (num):
        rem = num % 10
        if (not(rem == 3 or rem == 8)):
            count=count + 1
        num = num // 10

    return count

# Driver code

num = 234198
print("Minimum Operations =" ,minOp(num))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# to find min operations required to
// convert into charming number
using System;

class GFG
{

    // function for minimum operation
    static int minOp(int num)
    {

        // remainder and operations count
        int rem;
        int count = 0;

        // count digits not equal to 3 or 8
        while (num > 0)
        {
            rem = num % 10;
            if (! (rem == 3 || rem == 8))
                count++;
            num /= 10;
        }

        return count;
    }

    // Driver code
    public static void Main ()
    {
        int num = 234198;

        Console.WriteLine("Minimum Operations =" +
                           minOp(num));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP to find min operations required to
// convert into charming number

// function for minimum operation
function minOp($num)
{

    // remainder and operations count
    $count = 0;

    // count digits not equal to 3 or 8
    while ($num)
    {
        $rem = intval($num % 10);
        if (!($rem == 3 || $rem == 8))
            $count++;
        $num = intval($num / 10);
    }
    return $count;
}

    // Driver Code
    $num = 234198;
    echo "Minimum Operations = " . minOp($num);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript to find min operations required to
// convert into charming number

// function for minimum operation
function minOp(num)
{
    // remainder and operations count
    var rem;
    var count = 0;

    // count digits not equal to 3 or 8
    while (num) {
        rem = num % 10;
        if (!(rem == 3 || rem == 8))
            count++;
        num = parseInt(num/10);
    }
    return count;
}

// driver function
var num = 234198;
document.write( "Minimum Operations = " + minOp(num));

</script>
```

输出:

```
Minimum Operations = 4
```