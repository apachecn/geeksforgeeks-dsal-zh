# 从 0 到 n 的数字中 2 作为一个数字出现的次数

> 原文:[https://www . geeksforgeeks . org/从 0 到 n 的 2 位数出现次数/](https://www.geeksforgeeks.org/number-of-occurrences-of-2-as-a-digit-in-numbers-from-0-to-n/)

在从 0 到 n 的所有数字中，将 2 的数字计为数字。

**示例:**

```
Input : 22
Output : 6
Explanation: Total 2s that appear as digit
             from 0 to 22 are (2, 12, 20,
             21, 22);

Input : 100
Output : 20
Explanation: total 2's comes between 0 to 100 
are (2, 12, 20, 21, 22..29, 32, 42, 52, 62, 72,
82, 92);
```

一个**简单蛮力**的解决方案是迭代从 0 到 n 的所有数字。对于每个被访问的数字，计算其中的 2。最后返回总计数。

下面是这个想法的实现。

## C++

```
// C++ program to count 2s from 0 to n
#include <bits/stdc++.h>
using namespace std;

// Counts the number of '2'
// digits in a single number
int number0f2s(int n)
{
    int count = 0;
    while (n > 0)
    {
        if (n % 10 == 2)
            count++;

        n = n / 10;
    }
    return count;
}

// Counts the number of '2'
// digits between 0 and n
int numberOf2sinRange(int n)
{
    // Initialize result
    int count = 0 ;

    // Count 2's in every number
    // from 2 to n
    for (int i = 2; i <= n; i++)
        count += number0f2s(i);

    return count;
}

// Driver Code
int main()
{
    cout << numberOf2sinRange(22);
    cout << endl;
    cout << numberOf2sinRange(100);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count 2s from 0 to n

class GFG
{

// Counts the number of '2'
// digits in a single number
static int number0f2s(int n)
{
    int count = 0;
    while (n > 0)
    {
        if (n % 10 == 2)
        count++;

        n = n / 10;
    }
    return count;
}

// Counts the number of '2'
// digits between 0 and n
static int numberOf2sinRange(int n)
{

    // Initialize result
    int count = 0;

    // Count 2's in every number
    // from 2 to n
    for (int i = 2; i <= n; i++)
    count += number0f2s(i);

    return count;
}

// Driver code
public static void main(String[] args)
{
    System.out.print(numberOf2sinRange(22));
    System.out.println();
    System.out.print(numberOf2sinRange(100));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to count
# 2s from 0 to n

# Counts the number of
# '2' digits in a
# single number
def number0f2s(n):

    count = 0
    while (n > 0):

        if (n % 10 == 2):
            count = count + 1

        n = n // 10

    return count

# Counts the number of '2'
# digits between 0 and n
def numberOf2sinRange(n):

    # Initialize result
    count = 0

    # Count 2's in every number
    # from 2 to n
    for i in range(2, n + 1):
        count = count + number0f2s(i)

    return count

# Driver code

print(numberOf2sinRange(22))
print(numberOf2sinRange(100))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to count 2s from 0 to n
using System;

class GFG
{

// Counts the number of '2' digits
// in a single number
static int number0f2s(int n)
{
    int count = 0;
    while (n > 0)
    {
        if (n % 10 == 2)
            count++;

    n = n / 10;
    }
    return count;
}

// Counts the number of '2' digits
// between 0 and n
static int numberOf2sinRange(int n)
{

    // Initialize result
    int count = 0;

    // Count 2's in every number
    // from 2 to n
    for (int i = 2; i <= n; i++)
    count += number0f2s(i);

    return count;
}

// Driver code
public static void Main()
{
    Console.Write(numberOf2sinRange(22));
    Console.WriteLine();
    Console.Write(numberOf2sinRange(100));
}
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to count 2s from 0 to n

// Counts the number of '2'
// digits in a single number
function number0f2s($n)
{
    $count = 0;
    while ($n > 0)
    {
        if ($n % 10 == 2)
            $count++;

        $n = $n / 10;
    }
    return $count;
}

// Counts the number of '2'
// digits between 0 and n
function numberOf2sinRange($n)
{

    // Initialize result
    $count = 0 ;

    // Count 2's in every number
    // from 2 to n
    for ($i = 2; $i <= $n; $i++)
        $count += number0f2s($i);

    return $count;
}

// Driver Code
    echo (numberOf2sinRange(22));
    echo "\n";
    echo numberOf2sinRange(100);

// This code is contributed by
// nitin mittal.
?>
```

## java 描述语言

```
<script>

    // JavaScript program to count 2s from 0 to n

    // Counts the number of '2'
    // digits in a single number
    function number0f2s(n)
    {
        let count = 0;
        while (n > 0)
        {
            if (n % 10 == 2)
                count++;

            n = parseInt(n / 10, 10);
        }
        return count;
    }

    // Counts the number of '2'
    // digits between 0 and n
    function numberOf2sinRange(n)
    {
        // Initialize result
        let count = 0 ;

        // Count 2's in every number
        // from 2 to n
        for (let i = 2; i <= n; i++)
            count += number0f2s(i);

        return count;
    }

    document.write(numberOf2sinRange(22) + "</br>");
    document.write(numberOf2sinRange(100));

</script>
```

**Output:** 

```
6
20
```

下面是这种方法的另一种实现。

## C++

```
// Write C++ code here
#include <bits/stdc++.h>
using namespace std;
int numberOf2sinRange(int n)
{
    string s = "";
    for(int i = 0; i < n + 1; i++)
        s += to_string(i);       
    int count = 0;
    for(int i = 0; i < s.length(); i++)
    {
        if(s[i] == '2')
        {
            count++;
        }
    }
    return count;
}

// Driver code
int main()
{
    int n = 30;
    cout << numberOf2sinRange(n);
    return 0;
}

// This code is contributed by divyeshrabadiya07.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for above implementation
class GFG
{
  static int numberOf2sinRange(int n)
  {
    String s = "";
    for(int i = 0; i < n + 1; i++)
      s += String.valueOf(i);      
    int count = 0;
    for(int i = 0; i < s.length(); i++)
    {
      if(s.charAt(i) == '2')
      {
        count++;
      }
    }
    return count;
  }

  // Driver code
  public static void main(String[] args) {
    int n = 30;
    System.out.println(numberOf2sinRange(n));
  }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Write Python3 code here
def numberOf2sinRange(n):
    s = ""
    for i in range(0,n+1):
        s+=str(i)
    return(list(s).count('2'))

# Driver code
n = 30
print(numberOf2sinRange(n))
```

## C#

```
// C# code for above implementation
using System;
class GFG
{
  static int numberOf2sinRange(int n)
  {
    string s = "";
    for(int i = 0; i < n + 1; i++)
      s += i + "";  
    int count = 0;
    for(int i = 0; i < s.Length; i++)
    {
      if(s[i] == '2')
      {
        count++;
      }
    }
    return count;
  }

  // Driver code
  public static void Main(string[] args)
  {
    int n = 30;
    Console.Write(numberOf2sinRange(n));
  }
}

// This code is contributed by rutvik_56.
```

## java 描述语言

```
<script>

// Javascript code for above implementation
function numberOf2sinRange(n)
{
    var s = "";
    for(var i = 0; i < n + 1; i++)
        s += i.toString();

    var count = 0;
    for(var i = 0; i < s.length; i++)
    {
        if (s.charAt(i) == '2')
        {
            count++;
        }
    }
    return count;
}

// Driver code
var n = 30;

document.write(numberOf2sinRange(n));

// This code is contributed by Princi Singh

</script>
```

**Output:** 

```
13
```

**改进方案**
思路是一个数字一个数字看问题。想象一系列数字:

```
0  1  2  3  4  5  6  7  8  9
10 11 12 13 14 15 16 17 18 19
20 21 22 23 24 25 26 27 28 29
......
110 111 112 113 114 115 116 117 118 119 
```

我们知道，大约有十分之一的时间，最后一个数字是 2，因为它在十个数字的任何序列中出现一次。事实上，任何一个数字都是 2，大约是时间的十分之一。

我们说“大致”是因为有(非常常见的)边界条件。例如，在 1 和 100 之间，10 的数字正好是时间的 1/10<sup>。然而，在 1 和 37 之间，10 的数字是 2，比 1/10 <sup>的</sup>时间多得多。
我们可以通过分别查看三种情况来计算出具体的比例:数字 2。</sup>

**案例数字< 2**
考虑数值 x = 61523 和索引 d = 3 处的数字(此处从右开始考虑索引，最右边的索引为 0)。我们观察到 x[d] = 1。在范围 2000–2999、12000–12999、22000–22999、32000 32999、42000–42999 和 52000–52999 中，第三位数有 2。所以第三位数总共有 6000 个 2。这和我们计算 1 到 60000 之间第三位数的所有 2 是一样的。

换句话说，我们可以向下舍入到最近的 10 <sup>d+1</sup> ，然后除以 10，计算出第 d 位的 2s 数。

```
if x[d) < 2: count2sinRangeAtDigit(x, d) =
  Compute y = round down to nearest 10d+1 
  return y/10 
```

**格位> 2**
现在，我们来看看 x 的第 d 位(从右开始)大于 2 (x[d] > 2)的情况。我们可以应用几乎完全相同的逻辑，看到 0–63525 范围内的第三位数与 0–70000 范围内的位数相同。所以，我们不是向下舍入，而是向上舍入。

```
if x[d) > 2: count2sinRangeAtDigit(x, d) =
  Compute y = round down to nearest 10d+1 
  return y / 10 
```

**案例数字= 2**
最后一个案例可能是最棘手的，但它遵循了早期的逻辑。考虑 x = 62523 和 d = 3。我们知道以前有同样的 2s 范围(即 2000–2999，12000–12999，…，52000–52999)。有多少出现在 62000–62523 的最终部分范围的第三位？那应该很容易。只是 524 (62000，62001，…，62523)。

```
if x[d] = 2: count2sinRangeAtDigit(x, d) = 
   Compute y = round down to nearest 10d+1 
   Compute z = right side of x (i.e., x%  10d)
   return y/10 + z + 1
```

现在，我们只需要遍历数字中的每个数字。实现这段代码相当简单。

下面是这个想法的实现。

## C++

```
// C++ program to count 2s from 0 to n
#include <bits/stdc++.h>
using namespace std;

// Counts the number of 2s
// in a number at d-th digit
int count2sinRangeAtDigit(int number, int d)
{
    int powerOf10 = (int)pow(10, d);
    int nextPowerOf10 = powerOf10 * 10;
    int right = number % powerOf10;

    int roundDown = number - number % nextPowerOf10;
    int roundup = roundDown + nextPowerOf10;

    int digit = (number / powerOf10) % 10;

    // if the digit in spot digit is
    if (digit < 2)
        return roundDown / 10;

    if (digit == 2)
        return roundDown / 10 + right + 1;

    return roundup / 10;
}

// Counts the number of '2' digits between 0 and n
int numberOf2sinRange(int number)
{
    // Convert integer to String
    // to find its length
    stringstream convert;
    convert << number;
    string s = convert.str();
    int len = s.length();

    // Traverse every digit and
    // count for every digit
    int count = 0;
    for (int digit = 0; digit < len; digit++)
        count += count2sinRangeAtDigit(number, digit);

    return count;
}

// Driver Code
int main()
{
    cout << numberOf2sinRange(22) << endl;
    cout << numberOf2sinRange(100);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count 2s from 0 to n
class GFG
{

    // Counts the number of 2s
    // in a number at d-th digit
    static int count2sinRangeAtDigit(int number, int d)
    {
        int powerOf10 = (int) Math.pow(10, d);
        int nextPowerOf10 = powerOf10 * 10;
        int right = number % powerOf10;

        int roundDown = number - number % nextPowerOf10;
        int roundup = roundDown + nextPowerOf10;

        int digit = (number / powerOf10) % 10;

        // if the digit in spot digit is
        if (digit < 2)
        {
            return roundDown / 10;
        }

        if (digit == 2)
        {
            return roundDown / 10 + right + 1;
        }
        return roundup / 10;
    }

    // Counts the number of '2' digits between 0 and n
    static int numberOf2sinRange(int number)
    {
        // Convert integer to String
        // to find its length
        String convert;
        convert = String.valueOf(number);
        String s = convert;
        int len = s.length();

        // Traverse every digit and
        // count for every digit
        int count = 0;
        for (int digit = 0; digit < len; digit++)
        {
            count += count2sinRangeAtDigit(number, digit);
        }

        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        System.out.println(numberOf2sinRange(22));
        System.out.println(numberOf2sinRange(100));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to count 2s from 0 to n

# Counts the number of 2s in a
# number at d-th digit
def count2sinRangeAtDigit(number, d):

    powerOf10 = int(pow(10, d));
    nextPowerOf10 = powerOf10 * 10;
    right = number % powerOf10;

    roundDown = number - number % nextPowerOf10;
    roundup = roundDown + nextPowerOf10;

    digit = (number // powerOf10) % 10;

    # if the digit in spot digit is
    if (digit < 2):
        return roundDown // 10;

    if (digit == 2):
        return roundDown // 10 + right + 1;

    return roundup // 10;

# Counts the number of '2' digits
# between 0 and n
def numberOf2sinRange(number):

    # Convert integer to String
    # to find its length
    s = str(number);
    len1 = len(s);

    # Traverse every digit and
    # count for every digit
    count = 0;
    for digit in range(len1):
        count += count2sinRangeAtDigit(number,
                                       digit);

    return count;

# Driver Code
print(numberOf2sinRange(22));
print(numberOf2sinRange(100));

# This code is contributed by mits
```

## C#

```
// C# program to count 2s from 0 to n
using System;

class GFG
{

// Counts the number of 2s
// in a number at d-th digit
static int count2sinRangeAtDigit(int number,
                                 int d)
{
    int powerOf10 = (int) Math.Pow(10, d);
    int nextPowerOf10 = powerOf10 * 10;
    int right = number % powerOf10;

    int roundDown = number - number % nextPowerOf10;
    int roundup = roundDown + nextPowerOf10;

    int digit = (number / powerOf10) % 10;

    // if the digit in spot digit is
    if (digit < 2)
    {
        return roundDown / 10;
    }

    if (digit == 2)
    {
        return roundDown / 10 + right + 1;
    }
    return roundup / 10;
}

// Counts the number of '2' digits
// between 0 and n
static int numberOf2sinRange(int number)
{
    // Convert integer to String
    // to find its length
    string convert;
    convert = number.ToString();
    string s = convert;
    int len = s.Length;

    // Traverse every digit and
    // count for every digit
    int count = 0;
    for (int digit = 0; digit < len; digit++)
    {
        count += count2sinRangeAtDigit(number,
                                       digit);
    }

    return count;
}

// Driver Code
public static void Main()
{
    Console.WriteLine(numberOf2sinRange(22));
    Console.WriteLine(numberOf2sinRange(100));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count 2s from 0 to n

// Counts the number of 2s in a number
// at d-th digit
function count2sinRangeAtDigit($number, $d)
{
    $powerOf10 = (int)pow(10, $d);
    $nextPowerOf10 = $powerOf10 * 10;
    $right = $number % $powerOf10;

    $roundDown = $number - $number %
                 $nextPowerOf10;
    $roundup = $roundDown + $nextPowerOf10;

    $digit = ($number / $powerOf10) % 10;

    // if the digit in spot digit is
    if ($digit < 2)
        return $roundDown / 10;

    if ($digit == 2)
        return $roundDown / 10 + $right + 1;

    return $roundup / 10;
}

// Counts the number of '2' digits
// between 0 and n
function numberOf2sinRange($number)
{
    // Convert integer to String
    // to find its length
    $s = strval($number);
    $len = strlen($s);

    // Traverse every digit and
    // count for every digit
    $count = 0;
    for ($digit = 0; $digit < $len; $digit++)
        $count += count2sinRangeAtDigit($number,
                                        $digit);

    return $count;
}

// Driver Code
print(numberOf2sinRange(22) . "\n");
print(numberOf2sinRange(100) . "\n");

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to count 2s from 0 to n

    // Counts the number of 2s
    // in a number at d-th digit
    function count2sinRangeAtDigit(number , d)
    {
        var powerOf10 = parseInt( Math.pow(10, d));
        var nextPowerOf10 = powerOf10 * 10;
        var right = number % powerOf10;

        var roundDown = number - number % nextPowerOf10;
        var roundup = roundDown + nextPowerOf10;

        var digit = parseInt(number / powerOf10) % 10;

        // if the digit in spot digit is
        if (digit < 2)
        {
            return roundDown / 10;
        }

        if (digit == 2)
        {
            return roundDown / 10 + right + 1;
        }
        return roundup / 10;
    }

    // Counts the number of '2' digits between 0 and n
    function numberOf2sinRange(number)
    {
        // Convert integer to String
        // to find its length
        var convert;
        convert = number.toString();
        var s = convert;
        var len = s.length;

        // Traverse every digit and
        // count for every digit
        var count = 0;
        for (digit = 0; digit < len; digit++)
        {
            count += count2sinRangeAtDigit(number, digit);
        }

        return count;
    }

    // Driver Code
    document.write(numberOf2sinRange(22));
    document.write("<br>"+numberOf2sinRange(100));

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
6
20
```

**时间复杂度:** O(logN)

本文由 Somesh Awasthi 先生供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。