# 计算小于 N 的完美正方形的乘积

> 原文:[https://www . geesforgeks . org/count-number-小于 n-哪些是完美平方的乘积/](https://www.geeksforgeeks.org/count-number-less-than-n-which-are-product-of-perfect-squares/)

给定一个整数 N，任务是计算小于 N 的数 P，使得 P 是两个不同的完美平方的乘积。
**例** :

```
Input : N = 36
Output : 5
Numbers are 4 = 12 * 22, 
9 = 12 * 32, 
16 = 12 * 42, 
25 = 12 * 52, 
36 = 12 * 62

Input : N = 1000000
Output : 999
```

**方法:**让我们考虑一个数字 P = (a <sup>2</sup> * b <sup>2</sup> )这样 P < = N 所以我们有(a <sup>2</sup> * b <sup>2</sup> ) < = N 这可以写成(a * b) < = sqrt(N)。
所以我们要对(a，b)进行计数，这样(a * b) < = sqrt(N)和 a < = b.
让我们取一个数 **Q = (a * b)** 这样 Q < = sqrt(N)。
取 a = 1，我们有 b = sqrt(N)–1 个数字，这样，(a * b = Q < = sqrt(N))。
因此我们可以拥有所有 sqrt(N)–1 的数字，这样(a<sup>2</sup>* b<sup>2</sup>)<= N .
以下是上述方法的实现:

## C++

```
// C++ program to count number less
// than N which are product of
// any two perfect squares

#include <bits/stdc++.h>
using namespace std;

// Function to count number less
// than N which are product of
// any two perfect squares
int countNumbers(int N)
{
    return int(sqrt(N)) - 1;
}

// Driver program
int main()
{
    int N = 36;

    cout << countNumbers(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number less
// than N which are product of
// any two perfect squares
import java.util.*;

class solution
{

// Function to count number less
// than N which are product of
// any two perfect squares
static int countNumbers(int N)
{
    return (int)Math.sqrt(N) - 1;
}

// Driver program
public static void main(String args[])
{
    int N = 36;

    System.out.println(countNumbers(N));

}

}

//This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python 3 program to count number
# less than N which are product of
# any two perfect squares
import math

# Function to count number less
# than N which are product of
# any two perfect squares
def countNumbers(N):
    return int(math.sqrt(N)) - 1

# Driver Code
if __name__ == "__main__":
    N = 36

    print(countNumbers(N))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to count number less
// than N which are product of
// any two perfect squares
using System;

class GFG
{
// Function to count number less
// than N which are product of
// any two perfect squares
static int countNumbers(int N)
{
    return (int)(Math.Sqrt(N)) - 1;
}

// Driver Code
public static void Main()
{
    int N = 36;

    Console.Write(countNumbers(N));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number less
// than N which are product of
// any two perfect squares

// Function to count number less
// than N which are product of
// any two perfect squares
function countNumbers($N)
{
    return (int)(sqrt($N)) - 1;
}

// Driver Code
$N = 36;
echo countNumbers($N);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>
    // Javascript program to count number less
    // than N which are product of
    // any two perfect squares

    // Function to count number less
    // than N which are product of
    // any two perfect squares
    function countNumbers(N)
    {
        return parseInt(Math.sqrt(N), 10) - 1;
    }

    let N = 36;

    document.write(countNumbers(N));

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(log(N))