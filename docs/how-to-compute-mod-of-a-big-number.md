# 如何计算一个大数的 mod？

> 原文:[https://www . geesforgeks . org/如何计算大数字 mod/](https://www.geeksforgeeks.org/how-to-compute-mod-of-a-big-number/)

给定一个用字符串表示的大数字“num”和一个整数 x，求“num % x”或“num mod x”的值。输出应为整数。

**示例:**

```
Input:  num = "12316767678678",  a = 10
Output: num (mod a) ≡ 8
```

其思想是逐个处理所有数字，并使用

xy(修改 a)≥x(修改 a)* 10)+y(修改 a))修改 a

其中，x:最左边的数字

y:除 x 以外的其余数字。

例如:

625 % 5 = (((6 % 5)*10) + (25 % 5)) % 5 = 0

下面是实现。

感谢 utkarsh111 提出以下解决方案。

## C++

```
// C++ program to compute mod of a big number represented
// as string
#include <iostream>
using namespace std;

// Function to compute num (mod a)
int mod(string num, int a)
{
    // Initialize result
    int res = 0;

    // One by one process all digits of 'num'
    for (int i = 0; i < num.length(); i++)
        res = (res * 10 + (int)num[i] - '0') % a;

    return res;
}

// Driver program
int main()
{
    string num = "12316767678678";
    cout << mod(num, 10);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compute mod of a big
// number represented as string
import java.io.*;

class GFG {

    // Function to compute num (mod a)
    static int mod(String num, int a)
    {

        // Initialize result
        int res = 0;

        // One by one process all digits of 'num'
        for (int i = 0; i < num.length(); i++)
            res = (res * 10 + (int)num.charAt(i) - '0') % a;

        return res;
    }

    // Driver program
    public static void main(String[] args)
    {

        String num = "12316767678678";

        System.out.println(mod(num, 10));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# program to compute mod of a big number
# represented as string

# Function to compute num (mod a)

def mod(num, a):

    # Initialize result
    res = 0

    # One by one process all digits
    # of 'num'
    for i in range(0, len(num)):
        res = (res * 10 + int(num[i])) % a

    return res

# Driver program
num = "12316767678678"
print(mod(num, 10))

# This code is contributed by Sam007
```

## C#

```
// C# program to compute mod of a big
// number represented as string
using System;

public class GFG {

    // Function to compute num (mod a)
    static int mod(String num, int a)
    {

        // Initialize result
        int res = 0;

        // One by one process all
        // digits of 'num'
        for (int i = 0; i < num.Length; i++)
            res = (res * 10 + (int)num[i] - '0') % a;

        return res;
    }

    // Driver code
    public static void Main()
    {
        String num = "12316767678678";

        Console.WriteLine(mod(num, 10));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to compute mod
// of a big number represented
// as string

// Function to compute num (mod a)
function mod($num, $a)
{
    // Initialize result
    $res = 0;

    // One by one process
    // all digits of 'num'
    for ($i = 0; $i < $r = strlen($num); $i++)
        $res = ($res * 10 +
                $num[$i] - '0') % $a;

    return $res;
}

// Driver Code
$num = "12316767678678";
echo mod($num, 10);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to compute mod
// of a big number represented
// as string

// Function to compute num (mod a)
function mod(num, a)
{

    // Initialize result
    let res = 0;

    // One by one process
    // all digits of 'num'
    for(let i = 0; i < num.length; i++)
        res = (res * 10 +
            parseInt(num[i])) % a;

    return res;
}

// Driver Code
let num = "12316767678678";

document.write(mod(num, 10));

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
8
```

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息