# 给定三角形第 n 行所有数字的总和

> 原文:[https://www . geesforgeks . org/给定三角形的第 n 行所有数字的总和/](https://www.geeksforgeeks.org/sum-of-all-the-numbers-in-the-nth-row-of-the-given-triangle/)

给定一个正整数 **N** ，任务是求下面三角形的 **N <sup>第</sup>T5】行中所有数字的和。** 

> 1
> 3 2
> 6 2 3
> 10 2 3 4
> 15 2 3 4 5
> …
> …
> …

**例:**

> **输入:** N = 2
> **输出:** 5
> 3 + 2 = 5
> **输入:** N = 3
> **输出:** 11
> 6 + 2 + 3 = 11

**进场:**仔细看图案，可以观察到会形成一个系列为 **1、5、11、19、29、41、55、……**，其**N<sup>th</sup>T7】的术语为**(N–1)+N<sup>2</sup>**。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum
// of the nth row elements of
// the given triangle
int getSum(int n)
{
    return ((n - 1) + pow(n, 2));
}

// Driver code
int main()
{
    int n = 3;

    cout << getSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the sum
// of the nth row elements of
// the given triangle
static int getSum(int n)
{
    return ((n - 1) + (int)Math.pow(n, 2));
}

// Driver code
public static void main(String[] args)
{
    int n = 3;

    System.out.println(getSum(n));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the sum
# of the nth row elements of
# the given triangle
def getSum(n) :

    return ((n - 1) + pow(n, 2));

# Driver code
if __name__ == "__main__" :

    n = 3;

    print(getSum(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the sum
// of the nth row elements of
// the given triangle
static int getSum(int n)
{
    return ((n - 1) + (int)Math.Pow(n, 2));
}

// Driver code
public static void Main(String[] args)
{
    int n = 3;

    Console.WriteLine(getSum(n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the sum
// of the nth row elements of
// the given triangle
function getSum(n)
{
    return ((n - 1) + Math.pow(n, 2));
}

// Driver code
var n = 3;
document.write(getSum(n));

</script>
```

**Output:** 

```
11
```