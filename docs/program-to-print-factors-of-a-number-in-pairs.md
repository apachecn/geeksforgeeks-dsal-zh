# 成对打印一个数的因子的程序

> 原文:[https://www . geesforgeks . org/程序打印成对数字因子/](https://www.geeksforgeeks.org/program-to-print-factors-of-a-number-in-pairs/)

给定一个数字 n，程序员的任务是以成对出现的方式打印数字的因子。一对表示该对的乘积应该导致数字本身；
示例:

```
Input : 24
Output : 1*24
         2*12
         3*8
         4*6

Input : 50
Output : 1*50
         2*25
         5*10
```

这个程序最简单的方法是，我们运行一个从 1 到 N 的平方根的循环，如果数字 N 除以 I，则打印和打印 I 和 N%i。
我们运行循环直到 n 的平方根的数学原因如下:
If **a*b = N** 其中**1<a≤b<n**T6】n = ab≥a^2⇔a^2≤n⇔a≤√n

## C++

```
// CPP program to print prime factors in
// pairs.
#include <iostream>
using namespace std;

void printPFsInPairs(int n)
{
    for (int i = 1; i * i <= n; i++)
        if (n % i == 0)
            cout << i << "*" << n / i << endl;
}

// Driver code
int main()
{
    int n = 24;
    printPFsInPairs(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print prime factors in
// pairs.
public class GEE {

    static void printPFsInPairs(int n)
    {
        for (int i = 1; i * i <= n; i++)
            if (n % i == 0)
                System.out.println(i + "*" + n / i);
    }

    // Driver code
    public static void main(String[] args)
    {

        int n = 24;
        printPFsInPairs(n);
    }
}
```

## C#

```
// C# program to print prime factors in
// pairs.
using System;
public class GEE {

    static void printPFsInPairs(int n)
    {
        for (int i = 1; i * i <= n; i++)
            if (n % i == 0)
                Console.Write(i + "*" + n / i + "\n");
    }

    // Driver code
    public static void Main()
    {

        int n = 24;
        printPFsInPairs(n);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to print prime factors in
# pairs.

def printPFsInPairs(n):
    for i in range(1, int(pow(n, 1 / 2))+1):
        if n % i == 0:
            print(str(i) +"*"+str(int(n / i)))  

# Driver code
n = 24
printPFsInPairs(n)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print prime factors in
// pairs.

function printPFsInPairs($n)
{
    for ($i = 1; $i*$i <= $n; $i++)
        if ($n % $i == 0)
            echo $i."*". $n / $i ."\n";   
}

// Driver code
$n = 24;
printPFsInPairs($n);
return 0;
?>
```

## java 描述语言

```
<script>

// Javascript program to print prime factors in
// pairs.

function printPFsInPairs(n)
{
    for (let i = 1; i * i <= n; i++)
        if (n % i == 0)
            document.write(i + "*" + parseInt(n / i) + "<br>");
}

// Driver code
let n = 24;
printPFsInPairs(n);

</script>
```

**Output:** 

```
1*24
2*12
3*8
4*6
```