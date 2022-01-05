# 在一串 N 个字符中插入两对括号的方法数量

> 原文:[https://www . geeksforgeeks . org/将两对括号插入 n 字符字符串的方法数/](https://www.geeksforgeeks.org/number-of-ways-to-insert-two-pairs-of-parentheses-into-a-string-of-n-characters/)

给定一个长度为 **N** 的字符串 **str** ，任务是找出在给定字符串中只插入 2 对括号的方法，这样得到的字符串仍然有效。
**例:**

> **输入:** str = "ab"
> **输出:** 6
> ((a))b、(a)(b)、(a)(b)、(a(b))、a((b))
> 共 6 路。
> **输入:** str = "aab"
> **输出:** 20

**方法:**可以观察到，对于绳子的长度 **1、2、3、…、N** 一系列将形成为 **1、6、20、50、105、196、336、540、…** ，其 **N <sup>th</sup>** 术语为**(N+1)<sup>2</sup>*((N+1)<sup>2</sup>–1
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of ways
// to insert the bracket pairs
int cntWays(string str, int n)
{
    int x = n + 1;
    int ways = x * x * (x * x - 1) / 12;
    return ways;
}

// Driver code
int main()
{
    string str = "ab";
    int n = str.length();

    cout << cntWays(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the number of ways
// to insert the bracket pairs
static int cntWays(String str, int n)
{
    int x = n + 1;
    int ways = x * x * (x * x - 1) / 12;
    return ways;
}

// Driver code
public static void main(String []args)
{
    String str = "ab";
    int n = str.length();

    System.out.println(cntWays(str, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the number of ways
# to insert the bracket pairs
def cntWays(string, n) :

    x = n + 1;
    ways = x * x * (x * x - 1) // 12;
    return ways;

# Driver code
if __name__ == "__main__" :

    string = "ab";
    n = len(string);

    print(cntWays(string, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the number of ways
// to insert the bracket pairs
static int cntWays(String str, int n)
{
    int x = n + 1;
    int ways = x * x * (x * x - 1) / 12;
    return ways;
}

// Driver code
public static void Main(String []args)
{
    String str = "ab";
    int n = str.Length;

    Console.WriteLine(cntWays(str, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the number of ways
// to insert the bracket pairs
function cntWays(str, n)
{
    var x = n + 1;
    var ways = x * x * (x * x - 1) / 12;
    return ways;
}

// Driver code
var str = "ab";
var n = str.length;
document.write(cntWays(str, n));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
6
```