# 第 n 个偶数的程序

> 原文:[https://www.geeksforgeeks.org/program-for-n-th-even-number/](https://www.geeksforgeeks.org/program-for-n-th-even-number/)

给定一个数字 n，打印第 n 个偶数。第一个偶数是 2，第二个是 4，以此类推。

**示例:**

```
Input : 3
Output : 6
First three even numbers are 2, 4, 6, ..

Input : 5
Output : 10
First five even numbers are 2, 4, 6, 8, 19..

```

> 第 n 个偶数由公式 2*n 给出。

## C++

```
// CPP program to find the nth even number
#include <bits/stdc++.h>
using namespace std;

// Function to find the nth even number
int nthEven(int n)
{
    return (2 * n);
}

// Driver code
int main()
{
    int n = 10;
    cout << nthEven(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find the nth EVEN number

class GFG
{
    // Function to find the nth odd number
    static int nthEven(int n)
    {
        return (2 * n);
    }

    // Driver code
    public static void main(String [] args)
    {
        int n = 10;
        System.out.println(nthEven(n));

    }
}

// This code is contributed
// by ihritik
```

## 蟒蛇 3

```
# Python 3 program to find the 
# nth odd number

#  Function to find the nth Even number
def nthEven(n):

    return (2 * n)

# Driver code
if __name__=='__main__':
    n = 10
    print(nthEven(n))

# This code is contributed
# by ihritik
```

## C#

```
// C# program to find the 
// nth EVEN number
using System;

class GFG
{
// Function to find the
// nth odd number
static int nthEven(int n)
{
    return (2 * n);
}

// Driver code
public static void Main()
{
    int n = 10;
    Console.WriteLine(nthEven(n));
}
}

// This code is contributed
// by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// nth even number

// Function to find the
// nth even number
function nthEven($n)
{
    return (2 * $n);
}

// Driver code
$n = 10;
echo nthEven($n);

// This code is contributed
// by anuj_67
?>
```

**输出:**

```
20
```