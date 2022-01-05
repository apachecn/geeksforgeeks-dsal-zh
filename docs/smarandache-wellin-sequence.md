# 斯马兰达什-韦林序列

> 原文:[https://www.geeksforgeeks.org/smarandache-wellin-sequence/](https://www.geeksforgeeks.org/smarandache-wellin-sequence/)

给定一个数字“n”，生成 Smarandache-Wellin 序列的第一个“n”项。
**斯马兰达什-韦林序列**是由斯马兰达什-韦林数组成的序列。组成序列的每个 Smarandache-Wellin 数都是通过从第一个素数(即 2)开始连接连续的素数而获得的。因此，序列的第一项是 2，第二项是 23，第三项是 235，…类似地，第 n 项由从第一个质数即 2 开始的第一个“n”个质数串联而成。
**示例:**

```
Input : 5
Output : 2 23 235 2357 235711

Input : 10
Output : 2 23 235 2357 235711 23571113 2357111317 235711131719 23571113171923
2357111317192329
```

**方法:**
**1)** 最初找到第一个‘n’个质数，并将其存储在列表中。
**2)** 接下来，从第一个术语开始串联列表的每个术语，并且每次将串联术语的长度增加 1。
**3)** 每次继续打印如此形成的串联术语，以生成序列。
下面是 Python 中的实现。

## C++

```
// C++ program to print the first
// 'n' terms of the Smarandache-Wellin
// Sequence
#include<bits/stdc++.h>
using namespace std;

// Function to collect
// first 'n' prime numbers
void primes(int n)
{
    int i = 2;
    int j = 0;

    // List to store
    // first 'n' primes
    int result[n];
    int z = 0;
    while(j < n)
    {
        bool flag = true;
        for(int item = 2;
                item <= (int)(i * 1 / 2);
                item++)
           if(i % item == 0 && i != item)
           {
               flag = false;
               break;
            }

        if (flag)
        {
            result[z++] = i;
            j += 1;
        }
        i += 1;
    }

    for(i = 0; i < 5; i++)
    {
       for(j = 0; j <= i; j++)
          cout << result[j];
       cout << " ";
    }
}

// Function to generate
// Smarandache-Wellin Sequence
void smar_wln(int n)
{

    // Storing the first 'n'
    // prime numbers in a list
    primes(n);

}

// Driver Code
int main()
{
    int n = 5;

    cout << "First " << n
         << " terms of the Sequence are"
         << endl;

    smar_wln(n);
}

// This code is contributed by Ritik Bansal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the
// first 'n' terms of the
// Smarandache-Wellin Sequence

class GFG{
// Function to collect
// first 'n' prime numbers
static void primes(int n)
{
    int i = 2;
    int j = 0;

    // List to store
    // first 'n' primes
    int[] result=new int[n];
    int z = 0;
    while(j < n)
    {
        boolean flag = true;
        for(int item = 2;item <= (int)(i * 1 / 2); item++)
            if(i % item == 0 && i != item)
            {
                flag = false;
                break;
            }
        if (flag)
        {
            result[z++] = i;
            j += 1;
        }
        i += 1;
    }

    for(i = 0; i < result.length; i++)
    {
        for(j = 0; j <= i; j++)
            System.out.print(result[j]);
        System.out.print(" ");
    }
}

// Function to generate
// Smarandache-Wellin Sequence
static void smar_wln(int n)
{
    // Storing the first 'n'
    // prime numbers in a list
    primes(n);

}
// Driver Code
public static void main(String[] args)
{
int n = 5;
System.out.println("First "+n+" terms of the Sequence are");
smar_wln(n);
}
}
// This code is contributed
// by mits
```

## 蟒蛇 3

```
# Python program to print the first 'n' terms
# of the Smarandache-Wellin Sequence

from __future__ import print_function

# Function to collect first 'n' prime numbers

def primes(n):
    i, j = 2, 0
    # List to store first 'n' primes
    result = []
    while j < n:
        flag = True
        for item in range(2, int(i**0.5)+1):
            if i % item == 0 and i != item:
                flag = False
                break
        if flag:
            result.append(i)
            j += 1
        i += 1
    return result

# Function to generate Smarandache-Wellin
# Sequence

def smar_wln(n):
    # Storing the first 'n' prime numbers in
    # a list
    arr = primes(n)
    for i in range(0, len(arr)):
        for j in range(0, i + 1):
            print(arr[j], end ='')
        print(end =' ')

# Driver Method

if __name__=='__main__':
    n = 5
    print('First {} terms of the Sequence are\n'.format(n))
    smar_wln(n)
```

## C#

```
// C# program to print the
// first 'n' terms of the
// Smarandache-Wellin Sequence
class GFG
{
// Function to collect
// first 'n' prime numbers
static void primes(int n)
{
    int i = 2;
    int j = 0;

    // List to store
    // first 'n' primes
    int[] result = new int[n];
    int z = 0;
    while(j < n)
    {
        bool flag = true;
        for(int item = 2;
                item <= (int)(i * 1 / 2); item++)
            if(i % item == 0 && i != item)
            {
                flag = false;
                break;
            }
        if (flag)
        {
            result[z++] = i;
            j += 1;
        }
        i += 1;
    }

    for(i = 0; i < result.Length; i++)
    {
        for(j = 0; j <= i; j++)
            System.Console.Write(result[j]);
        System.Console.Write(" ");
    }
}

// Function to generate
// Smarandache-Wellin Sequence
static void smar_wln(int n)
{
    // Storing the first 'n'
    // prime numbers in a list
    primes(n);

}

// Driver Code
static void Main()
{
    int n = 5;
    System.Console.WriteLine("First " + n +
             " terms of the Sequence are");
    smar_wln(n);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the
// first 'n' terms of the
// Smarandache-Wellin Sequence

// Function to collect
// first 'n' prime numbers
function primes($n)
{
    $i = 2;
    $j = 0;

    // List to store
    // first 'n' primes
    $result;
    $z = 0;
    while($j < $n)
    {
        $flag = true;
        for($item = 2;
            $item <= (int)($i * 1 / 2); $item++)
            if($i % $item == 0 && $i != $item)
            {
                $flag = false;
                break;
            }
        if ($flag)
        {
            $result[$z++] = $i;
            $j += 1;
        }
        $i += 1;
    }
    return $result;
}

// Function to generate
// Smarandache-Wellin Sequence
function smar_wln($n)
{
    // Storing the first 'n'
    // prime numbers in a list
    $arr = primes($n);
    for($i = 0;
        $i < count($arr); $i++)
    {
        for($j = 0; $j <= $i; $j++)
            echo $arr[$j];
        echo " ";
    }
}
// Driver Code
$n = 5;
echo "First $n terms of the".
        " Sequence are\n";
smar_wln($n);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to print the first
// 'n' terms of the Smarandache-Wellin
// Sequence

// Function to collect
// first 'n' prime numbers
function primes(n)
{
    var i = 2;
    var j = 0;

    // List to store
    // first 'n' primes
    var result = Array(n)
    var z = 0;
    while(j < n)
    {
        var flag = true;
        for(var item = 2;
                item <= parseInt(i * 1 / 2);
                item++)
           if(i % item == 0 && i != item)
           {
               flag = false;
               break;
            }

        if (flag)
        {
            result[z++] = i;
            j += 1;
        }
        i += 1;
    }

    for(i = 0; i < 5; i++)
    {
       for(j = 0; j <= i; j++)
          document.write( result[j]);
       document.write(" ");
    }
}

// Function to generate
// Smarandache-Wellin Sequence
function smar_wln(n)
{

    // Storing the first 'n'
    // prime numbers in a list
    primes(n);

}

// Driver Code
var n = 5;

document.write( "First " + n
     + " terms of the Sequence are<br>" );
smar_wln(n);

// This code is contributed by rrrtnx.
</script>
```

**输出**T2】

```
First 5 terms of the Sequence are

2 23 235 2357 235711 
```