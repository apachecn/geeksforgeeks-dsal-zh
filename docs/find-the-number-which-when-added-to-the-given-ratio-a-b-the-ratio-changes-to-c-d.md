# 找出当加到给定的 a : b 比例时，该比例变为 c : d 的数字

> 原文:[https://www . geeksforgeeks . org/find-the-number-当添加到给定比率时-a-b-比率-变化-c-d/](https://www.geeksforgeeks.org/find-the-number-which-when-added-to-the-given-ratio-a-b-the-ratio-changes-to-c-d/)

给定四个整数 **a** 、 **b** 、 **c** 和 **d** 。任务是找到数字 **X** ，当加到数字 **a** 和 **b** 上时，比值从 **a : b** 变为 **c : d** 。
**例:**

> **输入:** a = 3，b = 6，c = 3，d = 4
> **输出:** 6
> 当 a 和 b 相加 6 时
> a = 3 + 6 = 9
> b = 6 + 6 = 12
> 并且，新的比值将为 9 : 12 = 3 : 4
> **输入:** a = 2，b = 3，c = 4，d = 5
> **输出:**

**进场:**旧比例为 **a : b** ，新比例为 **c : d** 。设所需数为 **X** 、
So、 **(a + X) / (b + X) = c / d**
or、ad + dx = bc + cx
or、X(d–c)= BC–ad
So、**X =(BC–ad)/(d–c)**
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// required number X
int getX(int a, int b, int c, int d)
{
    int X = (b * c - a * d) / (d - c);
    return X;
}

// Driver code
int main()
{
    int a = 2, b = 3, c = 4, d = 5;

    cout << getX(a, b, c, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the
// required number X
static int getX(int a, int b, int c, int d)
{
    int X = (b * c - a * d) / (d - c);
    return X;
}

// Driver code
public static void main (String[] args)
{

    int a = 2, b = 3, c = 4, d = 5;
    System.out.println (getX(a, b, c, d));

}
}

// The code is contributed by ajit..@23
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return the
# required number X
def getX(a, b, c, d):

    X = (b * c - a * d) // (d - c)
    return X

# Driver code

a = 2
b = 3
c = 4
d = 5

print(getX(a, b, c, d))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the
// required number X
static int getX(int a, int b, int c, int d)
{
    int X = (b * c - a * d) / (d - c);
    return X;
}

// Driver code
static public void Main ()
{
    int a = 2, b = 3, c = 4, d = 5;
    Console.Write(getX(a, b, c, d));
}
}

// The code is contributed by Tushil.
```

## java 描述语言

```
<script>
// javascript implementation of the approach

// Function to return the
// required number X
function getX(a , b , c , d)
{
    var X = (b * c - a * d) / (d - c);
    return X;
}

// Driver code

var a = 2, b = 3, c = 4, d = 5;
document.write(getX(a, b, c, d));

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
2
```