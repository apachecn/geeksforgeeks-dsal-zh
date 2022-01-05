# 从连续年复利中求利率百分比的程序

> 原文:[https://www . geeksforgeeks . org/program-to-find-利率-连续多年复利百分比/](https://www.geeksforgeeks.org/program-to-find-the-rate-percentage-from-compound-interest-of-consecutive-years/)

给定两个整数 **N1** 和 **N2** ，这是连续两年的**复利**。任务是计算费率百分比。
**示例:**

> **输入:** N1 = 660，N2 = 720
> T3】输出: 9.09091 %
> **输入:** N1 = 100，N2 = 120
> **输出:** 20 %

**方法:**利率百分比可以用公式**((N2-N1)* 100)/N1**计算，其中 **N1** 为某年复利， **N2** 为下一年复利。

> 让我们考虑第一个例子:
> 连续两年复利的差异是因为前一年利息收到的利息。因此，
> –>N2–N1 = N1 *(速率/100)
> –>720–660 = 660 *(速率/100)
> –>(60/660)* 100 =速率
> –>速率= (100 / 11) = 9.09%(近似值)

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// required rate percentage
float Rate(int N1, int N2)
{
    float rate = (N2 - N1) * 100 / float(N1);

    return rate;
}

// Driver code
int main()
{
    int N1 = 100, N2 = 120;

    cout << Rate(N1, N2) << " %";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    // Function to return the
    // required rate percentage
    static int Rate(int N1, int N2)
    {
        float rate = (N2 - N1) * 100 / N1;

        return (int)rate;
    }

    // Driver code
    public static void main(String[] args)
    {
        int N1 = 100, N2 = 120;

        System.out.println(Rate(N1, N2) + " %");
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the
# required rate percentage
def Rate( N1, N2):
    rate = (N2 - N1) * 100 // (N1);

    return rate

# Driver code
if __name__ == "__main__":
    N1 = 100
    N2 = 120

    print(Rate(N1, N2) ," %")

# This code is contributed by ChitraNayal   
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the
    // required rate percentage
    static int Rate(int N1, int N2)
    {
        float rate = (N2 - N1) * 100 / N1;

        return (int)rate;
    }

    // Driver code
    static public void Main ()
    {
        int N1 = 100, N2 = 120;

        Console.WriteLine(Rate(N1, N2) + " %");
    }
}

// This code has been contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the
// required rate percentage
function Rate($N1, $N2)
{
    $rate = ($N2 - $N1) * 100 / $N1;

    return $rate;
}

// Driver code
$N1 = 100;
$N2 = 120;

echo Rate($N1, $N2), "%";

// This code is contributed by AnkitRai01
?>
```

## java 描述语言

```
<script>

// javascript implementation of the approach

    // Function to return the
    // required rate percentage
    function Rate(N1 , N2) {
        var rate = (N2 - N1) * 100 / N1;

        return parseInt( rate);
    }

    // Driver code

        var N1 = 100, N2 = 120;

        document.write(Rate(N1, N2) + " %");

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
20 %
```

**时间复杂度:** O(1)

**辅助空间:** O(1)