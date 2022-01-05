# 求数列 1、3、6、10、15、21 的第 n 项……

> 原文:[https://www . geesforgeks . org/find-n th-term-series-136101521/](https://www.geeksforgeeks.org/find-nth-term-series-136101521/)

给定一个数 n，求数列 1，3，6，10，15，21 的第 n 项…

示例:

```
Input : 3
Output : 6

Input : 4
Output : 10 
```

给定的数列表示[三角数](https://www.geeksforgeeks.org/triangular-numbers/)，它们是自然数的和。

**天真方法:**
级数基本上代表自然数的和。第一项是单个数的和。第二项是两个数的和，以此类推。一个简单的解决方案是将前 n 个自然数相加。

## C++

```
// CPP program to find n-th term of
// series 1, 3, 6, 10, 15, 21...
#include <iostream>
using namespace std;

// Function to find the nth term of series
int term(int n)
{     
    // Loop to add numbers
    int ans = 0;
    for (int i = 1; i <= n; i++)   
        ans += i;

    return ans;
}

// Driver code
int main()
{
    int n = 4;
    cout << term(n) ;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th term of
// series 1, 3, 6, 10, 15, 21...
import java.io.*;

class GFG {

    // Function to find the nth term of series
    static int term(int n)
    {    
        // Loop to add numbers
        int ans = 0;
        for (int i = 1; i <= n; i++)
            ans += i;

        return ans;
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 4;
        System.out.println(term(n));
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python 3 program to find
# n-th term of
# series 1, 3, 6, 10, 15, 21...

# Function to find the
# nth term of series
def term(n) :
    # Loop to add numbers
    ans = 0
    for i in range(1,n+1) :
        ans = ans + i

    return ans

# Driver code
n = 4
print(term(n))

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# program to find n-th term of
// series 1, 3, 6, 10, 15, 21...
using System;

class GFG {

    // Function to find the nth term
    // of series
    static int term(int n)
    {

        // Loop to add numbers
        int ans = 0;
        for (int i = 1; i <= n; i++)
            ans += i;

        return ans;
    }

    // Driver code
    public static void Main()
    {
        int n = 4;

        Console.WriteLine(term(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n-th term of
// series 1, 3, 6, 10, 15, 21...

// Function to find the nth
// term of series
function term($n)
{

    // Loop to add numbers
    $ans = 0;
    for ($i = 1; $i <= $n; $i++)
        $ans += $i;

    return $ans;
}

// Driver code
$n = 4;
echo(term($n)) ;

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find n-th term of
// series 1, 3, 6, 10, 15, 21...

// Function to find the nth term of series
function term(n)
{

    // Loop to add numbers
    let ans = 0;
    for(let i = 1; i <= n; i++)   
        ans += i;

    return ans;
}

// Driver code
let n = 4;

document.write(term(n));

// This code is contributed by rishavmahato348

</script>
```

**输出:**

```
10
```

该解决方案的时间复杂度为 0(n)。

#### 高效方法:

本系列中的模式为 **n <sup>次</sup>项等于(n-1) <sup>次</sup>项与 n** 项之和。
示例:

```
n = 2
2nd term equals to sum of 1st term and 2 i.e
A2 = A1 + 2 
   = 1 + 2
   = 3

Similarly,
A3 = A2 + 3
   = 3 + 3
   = 6 and so on..
```

我们得到:

```
A(n) = A(n - 1) + n 
     = A(n - 2) + n + (n - 1)
     = A(n - 3) + n + (n - 1) + (n - 2) 
       .
       .
       .
     = A(1) + 2 + 3... + (n-1) + n

A(n) = 1 + 2 + 3 + 4... + (n - 1) + n
     = n(n + 1) / 2

i.e A(n) is sum of First n natural numbers.
```

下面是上述方法的实现:

## C++

```
// CPP program to find the n-th
// term in series 1 3 6 10 ...
#include <bits/stdc++.h>
using namespace std;

// Function to find nth term
int term(int n)
{
    return n * (n + 1) / 2;
}

// Driver code
int main()
{
    int n = 4;
    cout << term(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the n-th
// term in series 1 3 6 10 ...
import java.io.*;

class Series {

    // Function to find nth term
    static int term(int n){
        return n * (n + 1) / 2;
    }

    // Driver Code
    public static void main (String[] args) {
        int n = 4;
        System.out.println(term(n));
    }
}

// This code is contributed by Chinmoy Lenka
```

## 计算机编程语言

```
# Python program to find the Nth
# term in series 1 3 6 10 ...

# Function to print nth term
# of series 1 3 6 10 ....
def term(n):
    return n *(n + 1) / 2

# Driver code
n = 4
print term(n)
```

## C#

```
// C# program to find the n-th
// term in series 1 3 6 10 ...
using System;

class GFG {

    // Function to find nth term
    static int term(int n)
    {
        return n * (n + 1) / 2;
    }

    // Driver Code
    public static void Main()
    {
        int n = 4;

        Console.WriteLine(term(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the n-th
// term in series 1 3 6 10 ...

// Function to find nth term
function term($n)
{
    return $n * ($n + 1) / 2;
}

// Driver code
$n = 4;
echo(term($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript program to find the n-th
// term in series 1 3 6 10 ...

// Function to find nth term
function term(n)
{
    return parseInt(n * (n + 1) / 2);
}

// Driver code
let n = 4;
document.write(term(n));

// This code is contributed by subhammahato348.
</script>
```

**输出:**

```
10
```

**时间复杂度:** O(1)