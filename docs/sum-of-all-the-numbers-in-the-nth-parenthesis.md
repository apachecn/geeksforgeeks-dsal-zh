# 第 n 个括号

中所有数字的总和

> 原文:[https://www . geesforgeks . org/第 n 个括号中所有数字的总和/](https://www.geeksforgeeks.org/sum-of-all-the-numbers-in-the-nth-parenthesis/)

给定整数 **N** 和序列 **(1)、(3、5)、(7、9、11)、(13、15、17、19)……..**任务是找出 **N <sup>th</sup>** 括号中所有数字的和。
**举例:**

> **输入:** N = 2
> **输出:** 8
> 3 + 5 = 8
> **输入:** N = 3
> **输出:** 27
> 7 + 9 + 11 = 27

**方法:**可以观察到对于 **N = 1、2、3、…** 的值，将形成一个系列为 **1、8、27、64、125、216、343、…** ，其**N<sup>th</sup>T9】术语为 **N <sup>3</sup>**
以下是上述方法的实现:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of the
// numbers in the nth parenthesis
int findSum(int n)
{
    return pow(n, 3);
}

// Driver code
int main()
{
    int n = 3;

    cout << findSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the sum of the
// numbers in the nth parenthesis
static int findSum(int n)
{
    return (int)Math.pow(n, 3);
}

// Driver code
public static void main(String[] args)
{
    int n = 3;

    System.out.println(findSum(n));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the sum of the
# numbers in the nth parenthesis
def findSum(n) :

    return n ** 3;

# Driver code
if __name__ == "__main__" :

    n = 3;

    print(findSum(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to return the sum of the
// numbers in the nth parenthesis
static int findSum(int n)
{
    return (int)Math.Pow(n, 3);
}

// Driver code
public static void Main(String[] args)
{
    int n = 3;

    Console.WriteLine(findSum(n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the sum of the
// numbers in the nth parenthesis
function findSum(n)
{
    return Math.pow(n, 3);
}

// Driver code
var n = 3;
document.write(findSum(n));

</script>
```

**Output:** 

```
27
```

**时间复杂度:** O(1)