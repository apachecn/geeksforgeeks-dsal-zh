# N 次抛硬币中获得 K 个头像的概率

> 原文:[https://www . geeksforgeeks . org/获得 k-heads-in-n-coin-tosses 的概率/](https://www.geeksforgeeks.org/probability-of-getting-k-heads-in-n-coin-tosses/)

给定两个整数 **N** 和 **R** 。任务是计算连续投掷中准确获得 **r** 人头的概率。
一枚公平的硬币在每一次抛硬币时都有相等的概率落在头上或尾巴上。

**示例:**

```
Input : N = 1, R = 1 
Output : 0.500000 

Input : N = 4, R = 3
Output : 0.250000 
```

**接近**
N 次抛硬币中获得 K 个头像的概率可以使用以下公式计算:
![[\frac{1}{2^n} * \frac{n!}{ r! * (n-r)!}]  ](img/4ae2bd67a2b0acfc02d32c092937b647.png "Rendered by QuickLaTeX.com")

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// function to calculate factorial
int fact(int n)
{
    int res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// apply the formula
double count_heads(int n, int r)
{
    double output;
    output = fact(n) / (fact(r) * fact(n - r));
    output = output / (pow(2, n));
    return output;
}

// Driver function
int main()
{
    int n = 4, r = 3;

    // call count_heads with n and r
    cout << count_heads(n, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG{

// function to calculate factorial
static int fact(int n)
{
    int res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// apply the formula
static double count_heads(int n, int r)
{
    double output;
    output = fact(n) / (fact(r) * fact(n - r));
    output = output / (Math.pow(2, n));
    return output;
}

// Driver function
public static void main(String[] args)
{
    int n = 4, r = 3;

    // call count_heads with n and r
    System.out.print(count_heads(n, r));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find probability
# of getting K heads in N coin tosses

# Function to calculate factorial
def fact(n):

    res = 1
    for i in range(2, n + 1):
        res = res * i
    return res

# Applying the formula
def count_heads(n, r):

    output = fact(n) / (fact(r) * fact(n - r))
    output = output / (pow(2, n))
    return output

# Driver code
n = 4
r = 3

# Call count_heads with n and r
print (count_heads(n, r))

# This code is contributed by Pratik Basu
```

## C#

```
using System;

public class GFG{

// Function to calculate factorial
static int fact(int n)
{
    int res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Apply the formula
static double count_heads(int n, int r)
{
    double output;
    output = fact(n) / (fact(r) * fact(n - r));
    output = output / (Math.Pow(2, n));
    return output;
}

// Driver function
public static void Main(String[] args)
{
    int n = 4, r = 3;

    // Call count_heads with n and r
    Console.Write(count_heads(n, r));
}
}
// This code contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Function to calculate factorial
function fact(n)
{
    var res = 1;
    for(var i = 2; i <= n; i++)
        res = res * i;

    return res;
}

// Apply the formula
function count_heads(n, r)
{
    var output;
    output = fact(n) / (fact(r) * fact(n - r));
    output = output / (Math.pow(2, n));
    return output;
}

// Driver Code
var n = 4, r = 3;

// Call count_heads with n and r
document.write(count_heads(n, r));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
0.250000
```

**时间复杂度:**在此实现中，我们必须根据值 **n** 计算阶乘，因此时间复杂度将是 **O(n)**
**辅助空间:**在此实现中，我们没有使用任何额外的空间，因此所需的辅助空间是 **O(1)**