# 系列 1.2.3 + 2.3.4 + … + n(n+1)(n+2)的和

> 原文:[https://www.geeksforgeeks.org/sum-series-1-2-3-2-3-4-nn1n2/](https://www.geeksforgeeks.org/sum-series-1-2-3-2-3-4-nn1n2/)

求级数 n 项之和:1.2.3 + 2.3.4 + … + n(n+1)(n+2)。在本例中，1.2.3 代表第一项，2.3.4 代表第二项。
**例:**

```
Input : 2
Output : 30
1.2.3 + 2.3.4 = 6 + 24 = 30

Input : 3
Output : 90
```

**简单方法**我们对 i = 1 到 n 运行一个循环，求(i)*(i+1)*(i+2)的和。
最后显示总数。

## C++

```
// CPP program to find sum of the series
// 1.2.3 + 2.3.4 + 3.4.5 + ...
#include <bits/stdc++.h>
using namespace std;

int sumofseries(int n)
{
    int res = 0;
    for (int i = 1; i <= n; i++)
        res += (i) * (i + 1) * (i + 2);   
    return res;
}

// Driver Code
int main()
{
    cout << sumofseries(3) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of the series
// 1.2.3 + 2.3.4 + 3.4.5 + ...
import java.io.*;
import java.math.*;

class GFG
{

    static int sumofseries(int n)
    {
    int res = 0;
    for (int i = 1; i <= n; i++)
        res += (i) * (i + 1) * (i + 2);
    return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        System.out.println(sumofseries(3));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find sum of the series
# 1.2.3 + 2.3.4 + 3.4.5 + ...

def sumofseries(n):

    res = 0
    for i in range(1, n+1):
        res += (i) * (i + 1) * (i + 2)
    return res

# Driver Program
print(sumofseries(3))

# This code is contributed
# by Smitha Dinesh Semwal
```

## C#

```
// Java program to find sum of the series
// 1.2.3 + 2.3.4 + 3.4.5 + ...
using System;

class GFG
{

    static int sumofseries(int n)
    {
        int res = 0;
        for (int i = 1; i <= n; i++)
            res += (i) * (i + 1) * (i + 2);
        return res;
    }

    // Driver Code
    public static void Main()
    {
        Console.WriteLine(sumofseries(3));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// sum of the series
// 1.2.3 + 2.3.4 + 3.4.5 + ...

function sumofseries($n)
{
    $res = 0;
    for ($i = 1; $i <= $n; $i++)
        $res += ($i) * ($i + 1) *
                       ($i + 2);
    return $res;
}

    // Driver Code
    echo sumofseries(3);

//This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// JavaScript program to find sum of the series
// 1.2.3 + 2.3.4 + 3.4.5 + ...

    function sumofseries(n)
    {
    let res = 0;
    for (let i = 1; i <= n; i++)
        res += (i) * (i + 1) * (i + 2);
    return res;
    }

// Driver Code

    document.write(sumofseries(3));

// This code is contributed by code_hunt.
</script>
```

**Output :** 

```
90
```