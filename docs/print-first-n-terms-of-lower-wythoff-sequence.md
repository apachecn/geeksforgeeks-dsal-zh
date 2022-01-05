# 打印下 Wythoff 序列的前 N 项

> 原文:[https://www . geesforgeks . org/print-first-n-terms-lower-wythoff-sequence/](https://www.geeksforgeeks.org/print-first-n-terms-of-lower-wythoff-sequence/)

给定一个整数 **N** ，任务是打印[下 Wythoff 序列](https://en.wikipedia.org/wiki/Beatty_sequence#Examples)的第一个 **N** 术语。

**示例:**

> **输入:** N = 5
> **输出:** 1，3，4，6，8
> 
> **输入:** N = 10
> **输出:** 1、3、4、6、8、9、11、12、14、16

**方法:**下 Wythoff 序列是这样一个序列，其**n<sup>th</sup>T5】项为 **a(n) =地板(n *φ)**，其中**φ=(1+sqrt(5))/2**。所以，我们运行一个循环，找到序列的第一个 **n** 项。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the first n terms
// of the lower Wythoff sequence
void lowerWythoff(int n)
{

    // Calculate value of phi
    double phi = (1 + sqrt(5)) / 2.0;

    // Find the numbers
    for (int i = 1; i <= n; i++) {

        // a(n) = floor(n * phi)
        double ans = floor(i * phi);

        // Print the nth numbers
        cout << ans;

        if (i != n)
            cout << ", ";
    }
}

// Driver code
int main()
{
    int n = 5;

    lowerWythoff(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to print the first n terms
// of the lower Wythoff sequence
static void lowerWythoff(int n)
{

    // Calculate value of phi
    double phi = (1 + Math.sqrt(5)) / 2.0;

    // Find the numbers
    for (int i = 1; i <= n; i++)
    {

        // a(n) = floor(n * phi)
        double ans = Math.floor(i * phi);

        // Print the nth numbers
        System.out.print((int)ans);

        if (i != n)
            System.out.print(" , ");
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 5;

    lowerWythoff(n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# from math import sqrt,floor
from math import sqrt, floor

# Function to print the first n terms
# of the lower Wythoff sequence
def lowerWythoff(n) :

    # Calculate value of phi
    phi = (1 + sqrt(5)) / 2;

    # Find the numbers
    for i in range(1, n + 1) :

        # a(n) = floor(n * phi)
        ans = floor(i * phi);

        # Print the nth numbers
        print(ans,end="");

        if (i != n) :
            print( ", ",end = "");

# Driver code
if __name__ == "__main__" :

    n = 5;
    lowerWythoff(n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print the first n terms
// of the lower Wythoff sequence
static void lowerWythoff(int n)
{

    // Calculate value of phi
    double phi = (1 + Math.Sqrt(5)) / 2.0;

    // Find the numbers
    for (int i = 1; i <= n; i++)
    {

        // a(n) = floor(n * phi)
        double ans = Math.Floor(i * phi);

        // Print the nth numbers
        Console.Write((int)ans);

        if (i != n)
            Console.Write(" , ");
    }
}

// Driver code
static public void Main ()
{
    int n = 5;

    lowerWythoff(n);
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to print the first n terms
// of the lower Wythoff sequence
function lowerWythoff(n)
{

    // Calculate value of phi
    var phi = (1 + Math.sqrt(5)) / 2.0;

    // Find the numbers
    for(var i = 1; i <= n; i++)
    {

        // a(n) = floor(n * phi)
        var ans = Math.floor(i * phi);

        // Print the nth numbers
        document.write( ans);

        if (i != n)
            document.write(", ");
    }
}

// Driver code
var n = 5;

lowerWythoff(n);

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
1, 3, 4, 6, 8
```