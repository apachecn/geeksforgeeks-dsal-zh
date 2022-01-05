# 给定单位数字的整数之和

> 原文:[https://www . geesforgeks . org/整数之和-up-n-带给定单位数字/](https://www.geeksforgeeks.org/sum-of-integers-upto-n-with-given-unit-digit/)

给定两个整数 **N** 和 **D** ，任务是求从 **1** 到 **N** 的所有整数的和，单位数字为 **D** 。
**举例:**

> **输入:** N = 30，D = 3
> **输出:** 39
> 3 + 13 + 23 = 39
> **输入:** N = 5，D = 7
> **输出:** 0

**天真的做法:**

*   从 **1** 穿越到 **N** 。
*   如果数字的单位数字是 **D** ，则将数字加到**和**上。
*   最后打印**和**的值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to return the required sum
ll getSum(int n, int d)
{
    ll sum = 0;
    for (int i = 1; i <= n; i++) {

        // If the unit digit is d
        if (i % 10 == d)
            sum += i;
    }
    return sum;
}

// Driver code
int main()
{
    int n = 30, d = 3;
    cout << getSum(n, d);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class solution
{

// Function to return the required sum
static long getSum(int n, int d)
{
    long sum = 0;
    for (int i = 1; i <= n; i++) {

        // If the unit digit is d
        if (i % 10 == d)
            sum += i;
    }
    return sum;
}

// Driver code
public static void main(String args[])
{
    int n = 30, d = 3;
    System.out.println(getSum(n, d));

}
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required sum
def getSum(n, d) :
    sum = 0;
    for i in range(n + 1) :

        # If the unit digit is d
        if (i % 10 == d) :
            sum += i
    return sum

# Driver code
if __name__ == "__main__" :

    n , d = 30, 3
    print(getSum(n, d))

# This code is contributed by Ryuga
```

<gfg-tab role="tab" slot="tab" id="gfg-tab-3">C#</gfg-tab><gfg-panel role="tabpanel" slot="panel" id="gfg-panel-3" data-code-lang="CSharp"></gfg-panel>

```
 // C# implementation of the approach
using System;
class gfg
{
  // Function to return the required sum
 public static int getSum(int n, int d)
 {
    int sum = 0;
    for (int i = 1; i <= n; i++) {

        // If the unit digit is d
        if (i % 10 == d)
            sum += i;
    }
    return sum;
}

// Driver code
 public static int Main()
 { 
    int n = 30, d = 3;
    Console.WriteLine( getSum(n, d));
    return 0;
 }
} 
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the required sum
function getSum($n, $d)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
    {

        // If the unit digit is d
        if ($i % 10 == $d)
            $sum += $i;
    }
    return $sum;
}

// Driver code
$n = 30;
$d = 3;
echo getSum($n, $d);

// This code is contributed by Sachin
?>
```

## java 描述语言

```
<script>

// java script implementation of the approach

// Function to return the required sum
function getSum(n, d)
{
    let sum = 0;
    for (let i = 1; i <= n; i++)
    {

        // If the unit digit is d
        if (i % 10 == d)
            sum += i;
    }
    return sum;
}

// Driver code
let n = 30;
let d = 3;
document.write( getSum(n, d));

// This code is contributed
// by bobby
</script>
```

**Output:** 

```
39
```

**高效方式:**而 **D < N** 更新 **sum = sum + D** 和 **D = D + 10** 。最后打印**总和**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to return the required sum
ll getSum(int n, int d)
{
    ll sum = 0;
    while (d <= n)
    {
        sum += d;
        d += 10;
    }
    return sum;
}

// Driver code
int main()
{
    int n = 30, d = 3;
    cout << getSum(n, d);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class Solution
{

// Function to return the required sum
static long getSum(int n, int d)
{
    long sum = 0;
    while (d <= n) {
        sum += d;
        d += 10;
    }
    return sum;
}

// Driver code
public static void main(String args[])
{
    int n = 30, d = 3;
    System.out.print(getSum(n, d));

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
# Function to return the required sum
def getSum(n, d):
    sum = 0
    while (d <= n):
        sum += d
        d += 10
    return sum

# Driver code
n = 30
d = 3
print(getSum(n, d))

# This code is contributed
# by sahishelangia
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to return the required sum
static long getSum(int n, int d)
{
    long sum = 0;
    while (d <= n)
    {
        sum += d;
        d += 10;
    }
    return sum;
}

// Driver code
public static void Main()
{
    int n = 30, d = 3;
    Console.Write(getSum(n, d));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
// Function to return the required sum
function getSum($n, $d)
{
    $sum = 0;
    while ($d <= $n)
    {
        $sum += $d;
        $d += 10;
    }
    return $sum;
}

// Driver code
$n = 30; $d = 3;
echo(getSum($n, $d));

// This Code is contributed
// by Mukul Singh
?>
```

## java 描述语言

```
<script>
// java script  implementation of the approach
// Function to return the required sum
function getSum(n, d)
{
    let sum = 0;
    while (d <= n)
    {
        sum += d;
        d += 10;
    }
    return sum;
}

// Driver code
let n = 30;
let d = 3;
document.write(getSum(n, d));

// This code is contributed
// by sravan kumar
</script>
```

**Output:** 

```
39
```