# 1 的总数

> 原文:[https://www.geeksforgeeks.org/total-no-1s-numbers/](https://www.geeksforgeeks.org/total-no-1s-numbers/)

给定一个整数 n，计算所有小于或等于 n 的正整数中出现的数字 1 的总数。
**示例:**

```
Input : n = 13
Output : 6
Explanation:
Here, no <= 13 containing 1 are 1, 10, 11,
12, 13\. So, total 1s are 6.

Input : n = 5
Output : 1
Here, no <= 13 containing 1 are 1.
So, total 1s are 1.
```

**方法 1:**

1.  从 1 到 n 迭代 I。
2.  将 I 转换为字符串，并计算每个整数字符串中的“1”。
3.  将每个字符串中的“1”计数加到总和中。

下面是上述方法的代码。

## C++

```
// c++ code to count the frequency of 1
// in numbers less than or equal to
// the given number.
#include <bits/stdc++.h>
using namespace std;
int countDigitOne(int n)
{
    int countr = 0;
    for (int i = 1; i <= n; i++) {
        string str = to_string(i);
        countr += count(str.begin(), str.end(), '1');
    }
    return countr;
}

// driver function
int main()
{
    int n = 13;
    cout << countDigitOne(n) << endl;
    n = 131;
    cout << countDigitOne(n) << endl;
    n = 159;
    cout << countDigitOne(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to count the frequency of 1
// in numbers less than or equal to
// the given number.
class GFG
{
static int countDigitOne(int n)
{
    int countr = 0;
    for (int i = 1; i <= n; i++)
    {
        String str = String.valueOf(i);
        countr += str.split("1", -1) . length - 1;
    }
    return countr;
}

// Driver Code
public static void main(String[] args)
{
    int n = 13;
    System.out.println(countDigitOne(n));
    n = 131;
    System.out.println(countDigitOne(n));
    n = 159;
    System.out.println(countDigitOne(n));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 code to count the frequency
# of 1 in numbers less than or equal
# to the given number.

def countDigitOne(n):
    countr = 0;
    for i in range(1, n + 1):
        str1 = str(i);
        countr += str1.count("1");

    return countr;

# Driver Code
n = 13;
print(countDigitOne(n));

n = 131;
print(countDigitOne(n));

n = 159;
print(countDigitOne(n));

# This code is contributed by mits
```

## C#

```
// C# code to count the frequency of 1
// in numbers less than or equal to
// the given number.
using System;
class GFG
{
static int countDigitOne(int n)
{
    int countr = 0;
    for (int i = 1; i <= n; i++)
    {
        string str = i.ToString();
        countr += str.Split("1") . Length - 1;
    }
    return countr;
}

// Driver Code
public static void Main()
{
    int n = 13;
    Console.WriteLine(countDigitOne(n));
    n = 131;
    Console.WriteLine(countDigitOne(n));
    n = 159;
    Console.WriteLine(countDigitOne(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to count the frequency of 1
// in numbers less than or equal to
// the given number.

function countDigitOne($n)
{
    $countr = 0;
    for ($i = 1; $i <= $n; $i++)
    {
        $str = strval($i);
        $countr += substr_count($str, '1');
    }
    return $countr;
}

// Driver Code
$n = 13;
echo countDigitOne($n) . "\n";

$n = 131;
echo countDigitOne($n) . "\n";

$n = 159;
echo countDigitOne($n) . "\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

    // Javascript code to count the frequency of 1
    // in numbers less than or equal to
    // the given number.

    function countDigitOne(n)
    {
        let countr = 0;
        for (let i = 1; i <= n; i++)
        {
            let str = i.toString();
            countr += str.split("1") . length - 1;
        }
        return countr;
    }

    let n = 13;
    document.write(countDigitOne(n) + "</br>");
    n = 131;
    document.write(countDigitOne(n) + "</br>");
    n = 159;
    document.write(countDigitOne(n) + "</br>");

</script>
```

**输出:**

```
6
66
96
```

**时间复杂度:** O(nlog(n))
**进场 2:**

1.  将 countr 初始化为 0。
2.  从 1 到 n 迭代 I，每次递增 10。
3.  在每个(i * 10)间隔后，在国家中加上(n / (i * 10 ) ) * i。
4.  将最小值(最大值(n mod(I * 10)–I+1，0)，I)添加到 countr。

下面是上述方法的代码。

## C++

```
// c++ code to count the frequency of 1
// in numbers less than or equal to
// the given number.
#include <bits/stdc++.h>
using namespace std;

// function to count the frequency of 1.
int countDigitOne(int n)
{
    int countr = 0;
    for (int i = 1; i <= n; i *= 10) {
        int divider = i * 10;
        countr += (n / divider) * i +
               min(max(n % divider - i + 1, 0), i);
    }
    return countr;
}

// driver function
int main()
{
    int n = 13;
    cout << countDigitOne(n) << endl;
    n = 113;
    cout << countDigitOne(n) << endl;
    n = 205;
    cout << countDigitOne(n) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/// Java code to count the
// frequency of 1 in numbers
// less than or equal to
// the given number.
import java.io.*;

class GFG
{

// function to count
// the frequency of 1.
static int countDigitOne(int n)
{
    int countr = 0;
    for (int i = 1;
             i <= n; i *= 10)
    {
        int divider = i * 10;
        countr += (n / divider) * i +
                Math.min(Math.max(n %
                         divider - i +
                            1, 0), i);
    }
    return countr;
}

// Driver Code
public static void main (String[] args)
{
    int n = 13;
    System.out.println(countDigitOne(n));

    n = 113;
    System.out.println(countDigitOne(n));

    n = 205;
    System.out.println(countDigitOne(n));
}
}

// This code is contributed by akt_mit
```

## 蟒蛇 3

```
# Python3 code to count the
# frequency of 1 in numbers
# less than or equal to
# the given number.

# function to count the
# frequency of 1.
def countDigitOne(n):
    countr = 0;
    i = 1;
    while(i <= n):
        divider = i * 10;
        countr += (int(n / divider) * i +
                 min(max(n % divider -i +
                              1, 0), i));
        i *= 10;

    return countr;

# Driver Code
n = 13;
print(countDigitOne(n));
n = 113;
print(countDigitOne(n));
n = 205;
print(countDigitOne(n));

# This code is contributed by mits
```

## C#

```
// C# code to count the
// frequency of 1 in numbers
// less than or equal to
// the given number.
using System;

class GFG
{

// function to count
// the frequency of 1.
static int countDigitOne(int n)
{
    int countr = 0;
    for (int i = 1;
             i <= n; i *= 10)
    {
        int divider = i * 10;
        countr += (n / divider) * i +
                   Math.Min(Math.Max(n % divider -
                                     i + 1, 0), i);
    }
    return countr;
}

// Driver Code
public static void Main()
{
    int n = 13;
    Console.WriteLine(countDigitOne(n));

    n = 113;
    Console.WriteLine(countDigitOne(n));

    n = 205;
    Console.WriteLine(countDigitOne(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to count the
// frequency of 1 in numbers
// less than or equal to
// the given number.

// function to count the
// frequency of 1.
function countDigitOne($n)
{
    $countr = 0;
    for ($i = 1; $i <= $n; $i *= 10)
    {
        $divider = $i * 10;
        $countr += (int)($n / $divider) * $i +
                       min(max($n % $divider -
                              $i + 1, 0), $i);
    }

    return $countr;
}

// Driver Code
$n = 13;
echo countDigitOne($n), "\n";
$n = 113;
echo countDigitOne($n), "\n";
$n = 205;
echo countDigitOne($n), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript code to count the frequency of 1
// in numbers less than or equal to
// the given number.

// function to count the frequency of 1.
function countDigitOne(n)
{
    var countr = 0;
    for (var i = 1; i <= n; i *= 10) {
        var divider = i * 10;
        countr += parseInt(n / divider) * i +
            Math.min(Math.max(n % divider - i + 1, 0), i);
    }
    return countr;
}

// driver function
var n = 13;
document.write(countDigitOne(n)+ "<br>");
n = 113;
document.write(countDigitOne(n)+ "<br>");
n = 205;
document.write(countDigitOne(n)+ "<br>");

</script>
```

**输出:**

```
6
40
141
```

**时间复杂度:** O(log(n))