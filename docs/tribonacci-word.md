# Tribonacci 词

> 原文:[https://www.geeksforgeeks.org/tribonacci-word/](https://www.geeksforgeeks.org/tribonacci-word/)

像[斐波那契字](https://www.geeksforgeeks.org/fibonacci-word/)，一个 Tribonacci 字。是特定的数字序列。Tribonacci 单词是通过重复连接形成的，就像 Fibonacci 单词是通过重复相加形成的一样。但与斐波那契字不同的是，Tribonacci 字是由后三项重复相加而成的，它的前三项互不相同。

```
In Tribonacci word,
  S(0) = 1, 
  S(1) = 12, 
  S(2) = 1213,
  S(3) = 1213121 
  ..... 
where S(n) = S(n-1) + S(n-2) + S(n-3) and + 
represents the concatenation of 
strings. 
```

任务是为给定的数字 n 找到第 n 个 Tribonacci 单词。示例:

```
Input : n = 4
Output : S(4) = 1213121121312

Input : n = 3
Output : S(3) = 1213121
```

就像在斐波那契字的程序中一样，我们在这里使用寻找第 n 个斐波那契字的迭代概念，对于寻找第 n 个 Tribonacci 字，我们可以使用迭代概念。因此，为了找到第 n 个 tribonacci 单词，我们将取三个字符串 Sn_1、Sn_2 和 Sn_3，它们分别表示 S(n-1)、S(n-2)和 S(n-3)，在每次迭代中，我们将更新 tmp = Sn_3、Sn_3 = Sn_3 + Sn_2 + Sn_1、Sn_1 = Sn_2 和 Sn_2 = tmp，这样我们就可以找到第 n 个 Tribonacci 单词。

## C++

```
// C++ program for nth Fibonacci word
#include <bits/stdc++.h>
using namespace std;

// Returns n-th Tribonacci word
string tribWord(int n) {
  string Sn_1 = "1";
  string Sn_2 = "12";
  string Sn_3 = "1213";
  string tmp;
  for (int i = 3; i <= n; i++) {
    tmp = Sn_3;
    Sn_3 += (Sn_2 + Sn_1);
    Sn_1 = Sn_2;
    Sn_2 = tmp;
  }

  return Sn_3;
}

// driver program
int main() {
  int n = 6;
  cout << tribWord(n);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// program for nth Tribonacci word
class GFG {

// Returns n-th Tribonacci word
static String tribWord(int n) {
    String Sn_1 = "1";
    String Sn_2 = "12";
    String Sn_3 = "1213";
    String tmp;
    for (int i = 3; i <= n; i++) {
    tmp = Sn_3;
    Sn_3 += (Sn_2 + Sn_1);
    Sn_1 = Sn_2;
    Sn_2 = tmp;
    }

    return Sn_3;
}

// Driver code
public static void main(String[] args) {
    int n = 6;
    System.out.print(tribWord(n));
}
}
// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 Program for nth
# Tribonacci word

# Returns n-th Tribonacci word
def tribWord(n):
    Sn_1 = "1"
    Sn_2 = "12"
    Sn_3 = "1213"
    for i in range(3, n+1):
        tmp = Sn_3
        Sn_3 += (Sn_2 + Sn_1)
        Sn_1 = Sn_2
        Sn_2 = tmp

    return Sn_3

# Driver code
n = 6
print(tribWord(n))

# This code is contributed By Anant Agarwal.
```

## C#

```
// C# program for nth Tribonacci word
using System;

class GFG {

    // Returns n-th Tribonacci word
    static string tribWord(int n)
    {
        string Sn_1 = "1";
        string Sn_2 = "12";
        string Sn_3 = "1213";
        string tmp;

        for (int i = 3; i <= n; i++) {
            tmp = Sn_3;
            Sn_3 += (Sn_2 + Sn_1);
            Sn_1 = Sn_2;
            Sn_2 = tmp;
        }

        return Sn_3;
    }

    // Driver code
    public static void Main() {

        int n = 6;

        Console.WriteLine(tribWord(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// Returns n-th Tribonacci word
function tribWord($n)
{
$Sn_1 = "1";
$Sn_2 = "12";
$Sn_3 = "1213";
$tmp;
for ($i = 3; $i <= $n; $i++)
{
    $tmp = $Sn_3;
    $Sn_3 .= ($Sn_2.$Sn_1);
    $Sn_1 = $Sn_2;
    $Sn_2 = $tmp;
}

return $Sn_3;
}

// Driver Code
$n = 6;
echo tribWord($n);

// This code is contributed by mits

?>
```

## java 描述语言

```
<script>

// javascript program for nth Fibonacci word

// Returns n-th Tribonacci word
function tribWord(n) {
  var Sn_1 = "1";
  var Sn_2 = "12";
  var Sn_3 = "1213";
  var tmp;
  for (var i = 3; i <= n; i++) {
    tmp = Sn_3;
    Sn_3 += (Sn_2 + Sn_1);
    Sn_1 = Sn_2;
    Sn_2 = tmp;
  }

  return Sn_3;
}

// driver program
var n = 6;
document.write( tribWord(n));

// This code is contributed by noob2000.
</script>
```

输出:

```
12131211213121213121121312131211213121213121
```

https://youtu.be/TM5

-和 2AKJY