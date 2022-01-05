# 第 n 个奇数的程序

> 原文:[https://www.geeksforgeeks.org/program-for-n-th-odd-number/](https://www.geeksforgeeks.org/program-for-n-th-odd-number/)

给定一个数字 n，打印第 n 个奇数。第一个奇数是 1，第二个是 3，依此类推。
**例:**

```
Input : 3
Output : 5
First three odd numbers are 1, 3, 5, ..

Input : 5
Output : 9
First 5 odd numbers are 1, 3, 5, 7, 9, ..
```

> 第 n 个奇数由公式 2*n-1 给出。

## C++

```
// CPP program to find the nth odd number
#include <bits/stdc++.h>
using namespace std;

// Function to find the nth odd number
int nthOdd(int n)
{
    return (2 * n - 1);
}

// Driver code
int main()
{
    int n = 10;
    cout << nthOdd(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find the nth odd number

class GFG
{
    // Function to find the nth odd number
    static int nthOdd(int n)
    {
        return (2 * n - 1);
    }

    // Driver code
    public static void main(String [] args)
    {
        int n = 10;
        System.out.println(nthOdd(n));

    }
}

// This code is contributed
// by ihritik
```

## 蟒蛇 3

```
# Python 3 program to find the
# nth odd number

# Function to find the nth odd number
def nthOdd(n):

    return (2 * n - 1)

# Driver code
if __name__=='__main__':
    n = 10
    print(nthOdd(n))

# This code is contributed
# by ihritik
```

## C#

```
// C# program to find the nth odd number
using System;

class GFG
{

// Function to find the nth odd number
static int nthOdd(int n)
{
    return (2 * n - 1);
}

// Driver code
public static void Main()
{
    int n = 10;
    Console.WriteLine(nthOdd(n));
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// Nth odd number

// Function to find the
// Nth odd number
function nthOdd($n)
{
    return (2 * $n - 1);
}

// Driver code
$n = 10;
echo nthOdd($n);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// Javascript program to find the nth odd number

// Function to find the nth odd number
function nthOdd(n)
{
    return (2 * n - 1);
}

// Driver code

var n = 10;
document.write( nthOdd(n));

</script>
```

**输出:**

```
19
```