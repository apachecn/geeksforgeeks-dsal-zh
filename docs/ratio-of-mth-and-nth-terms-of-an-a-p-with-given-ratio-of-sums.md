# a . p .的第 n 项和第 m 项与给定总和比率的比率

> 原文:[https://www . geeksforgeeks . org/给定总和比率的第 n 个术语比率/](https://www.geeksforgeeks.org/ratio-of-mth-and-nth-terms-of-an-a-p-with-given-ratio-of-sums/)

假设带有第一项“a”和普通差“d”的 A.P .的前 m 项和前 n 项之和的比值为 **m^2:n^2** 。任务是找到这个 A.P.
**的第 n 项和第 mth 项的比值示例:**

```
Input: m = 3, n = 2
Output: 1.6667

Input: m = 5, n = 3
Output: 1.8
```

**方法:**
让前 m 项和 n 项之和分别用 Sm 和 Sn 表示。
同样，让 mth 和第 n 项分别用 tm 和 tn 表示。

> sm =(m *[2 * a+(m-1)* d])/2
> sn =(n *[2 * a+(n-1)* d])/2
> 给定:Sm / Sn = m^2 / n^2
> 因此，((m *[2 * a+(m-1)* d])/2)/((n *[2 * a+(n-1)* d])/2)= m^2/n^2
> =>(2 * a+(m-1) mth 和第 n 项可以写成:
> mth 项= tm = a +(m-1)*d = a + (m-1)*(2*a)
> 第 n 项= tn = a +(n-1)*d = a + (n-1)*(2*a)
> 因此比值将为:
> TM/TN =(a+(m-1)*(2 * a))/(a+(n-1)*(2 * a))
> TM/TN

下面是需要的实现:

## C++

```
// C++ code to calculate ratio
#include <bits/stdc++.h>
using namespace std;

// function to calculate ratio of mth and nth term
float CalculateRatio(float m, float n)
{
    // ratio will be tm/tn = (2*m - 1)/(2*n - 1)
    return (2 * m - 1) / (2 * n - 1);
}

// Driver code
int main()
{
    float m = 6, n = 2;
    cout << CalculateRatio(m, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to calculate ratio
import java.io.*;

class Nth {

// function to calculate ratio of mth and nth term
static float CalculateRatio(float m, float n)
{
    // ratio will be tm/tn = (2*m - 1)/(2*n - 1)
    return (2 * m - 1) / (2 * n - 1);
}
}

// Driver code
class GFG {

    public static void main (String[] args) {
    float m = 6, n = 2;
    Nth a=new Nth();
System.out.println(a.CalculateRatio(m, n));

    }
}

// this code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python3 program to calculate ratio

# function to calculate ratio
# of mth and nth term
def CalculateRatio(m, n):

    # ratio will be tm/tn = (2*m - 1)/(2*n - 1)
    return (2 * m - 1) / (2 * n - 1);

# Driver code
if __name__=='__main__':
    m = 6;
    n = 2;
    print (float(CalculateRatio(m, n)));

# This code is contributed by
# Shivi_Aggarwal
```

## C#

```
// C# code to calculate ratio
using System;

class Nth {

// function to calculate ratio of mth and nth term
float CalculateRatio(float m, float n)
{
    // ratio will be tm/tn = (2*m - 1)/(2*n - 1)
    return (2 * m - 1) / (2 * n - 1);
}

    // Driver code
    public static void Main () {
    float m = 6, n = 2;
    Nth a=new Nth();
Console.WriteLine(a.CalculateRatio(m, n));

    }
}
// this code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to calculate ratio

// function to calculate ratio
// of mth and nth term
function CalculateRatio( $m, $n)
{
    // ratio will be tm/tn = (2*m - 1)/(2*n - 1)
    return (2 * $m - 1) / (2 * $n - 1);
}

// Driver code

$m = 6; $n = 2;
echo CalculateRatio($m, $n);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// JavaScript code to calculate ratio

// function to calculate ratio of mth and nth term
function CalculateRatio(m, n)
{
    // ratio will be tm/tn = (2*m - 1)/(2*n - 1)
    return (2 * m - 1) / (2 * n - 1);
}

// Driver code

    let m = 6, n = 2;
    document.write(CalculateRatio(m, n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
3.66667
```