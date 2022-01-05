# 使用位运算符

检查一个数字是正、负还是零

> 原文:[https://www . geesforgeks . org/check-number-正数-负数-零-使用位运算符/](https://www.geeksforgeeks.org/check-number-positive-negative-zero-using-bit-operators/)

给定一个数字 N，在不使用条件语句的情况下检查它是正的、负的还是零。
示例:

```
Input : 30
Output : 30 is positive

Input : -20
Output : -20 is negative

Input: 0
Output: 0 is zero
```

有符号移位 n>>31 将每一个负数转换为-1，每隔一个负数转换为 0。
当我们做一个-n > > 31 时，如果它是一个正数，那么它会像我们做的那样返回-1-n>>31，反之亦然。
但是当我们对 0 做运算时，那么 n > > 31 和-n > > 31 都返回 0，所以我们得到一个公式:

> 1+(n > > 31)–(-n > > 31)

..1) **当 n 为负时** :
1 +(-1)-0=0
..2) **当 n 为正时:**
1+0-(-1)=2
..3) **当 n 为 0 时:**
1+0-0=1
所以我们知道它为负数时返回 0，为零时返回 1，为正数时返回 2。
所以为了不使用 if 语句，我们存储在第 0 个索引“负”，第 1 个索引“零”和第 2 个索引“正”，并根据它打印。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to find if a number is
// positive, negative or zero using
// bit wise operators.
#include <iostream>
using namespace std;

// function to return 1 if it is zero
// returns 0 if it is negative
// returns 2 if it is positive
int index(int i)
{
    return 1 + (i >> 31) - (-i >> 31);
}

void check(int n)
{
    // string array to store all kinds of number
    string s[] = { "negative", "zero", "positive" };

    // function call to check the sign of number
    int val = index(n);

    cout << n << " is " << s[val] << endl;
}

// driver program to test the above function
int main()
{
    check(30);
    check(-20);
    check(0);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a number is
// positive, negative or zero using
// bit wise operators.
class GFG {

    // function to return 1 if it is zero
    // returns 0 if it is negative
    // returns 2 if it is positive
    static int index(int i)
    {
        return 1 + (i >> 31) - (-i >> 31);
    }

    static void check(int n)
    {

        // string array to store all kinds
        // of number
        String s[] = { "negative", "zero",
                              "positive" };

        // function call to check the sign
        // of number
        int val = index(n);

        System.out.println(n + " is " + s[val]);
    }

    // Driver code
    public static void main(String[] args)
    {
        check(30);
        check(-20);
        check(0);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python 3 program to
# find if a number is
# positive, negative
# or zero using
# bit wise operators.

# function to return 1 if it is zero
# returns 0 if it is negative
# returns 2 if it is positive
def index(i):

    return 1 + (i >> 31) - (-i >> 31)

def check(n):

    # string array to store all kinds of number
    s = "negative", "zero", "positive"

    # function call to check the sign of number
    val = index(n)

    print(n,"is",s[val])

# driver program to
# test the above function
check(30)
check(-20)
check(0)

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to find if a number is
// positive, negative or zero using
// bit wise operators.
using System;

class GFG {

    // function to return 1 if it is zero
    // returns 0 if it is negative
    // returns 2 if it is positive
    static int index(int i)
    {
        return 1 + (i >> 31) - (-i >> 31);
    }

    static void check(int n)
    {

        // string array to store all kinds of number
        String []s = { "negative", "zero", "positive" };

        // function call to check the sign of number
        int val = index(n);

        Console.WriteLine(n + " is " + s[val]);
    }

    //Driver code
    public static void Main()
    {
        check(30);
        check(-20);
        check(0);
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if a number is
// positive, negative or zero using
// bit wise operators.

// function to return 1 if it is zero
// returns 0 if it is negative
// returns 2 if it is positive
function index($i)
{
    return 1 + ($i >> 31) -
               (-$i >> 31);
}

function check($n)
{

    // string array to store
    // all kinds of number
    $s = array("negative", "zero", "positive" );

    // function call to check
    // the sign of number
    $val = index($n);

    echo $n, " is ", $s[$val], "\n";
}

    // Driver Code
    check(30);
    check(-20);
    check(0);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to find if a number is
// positive, negative or zero using
// bit wise operators.

    // function to return 1 if it is zero
    // returns 0 if it is negative
    // returns 2 if it is positive
    function index(i)
    {
        return 1 + (i >> 31) - (-i >> 31);
    }

    function check(n)
    {
        // string array to store all kinds of number
        let s = [ "negative", "zero", "positive" ];

        // function call to check the sign of number
        let val = index(n);

        document.write(n + " is " + s[val] + "<br>");
    }

// driver program to test the above function

    check(30);
    check(-20);
    check(0);

// This code is contributed by Surbhi Tyagi

</script>
```

**输出:**

```
30 is positive
-20 is negative
0 is zero
```