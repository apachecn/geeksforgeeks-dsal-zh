# 构建从 x^2 x^1 获得的数值的数字频率数组..，x^n

> 原文:[https://www . geesforgeks . org/construct-a-frequency-array-of-values-from-x1-x2-xn/](https://www.geeksforgeeks.org/construct-a-frequency-array-of-digits-of-the-values-obtained-from-x1-x2-xn/)

给定两个整数(x 和 n)。任务是找到一个数组，使它包含出现在(x^1，x^2，…)的索引号的频率。，x^(n-1)，x^(n)。

**例:**

```
Input: x = 15, n = 3
Output: 0 1 2 2 0 3 0 1 0 0
Numbers x^1 to x^n are 15, 225, 3375.
So frequency array is 0 1 2 2 0 3 0 1 0 0.

Input: x = 1, n = 5
Output: 0 5 0 0 0 0 0 0 0 0
Numbers x^1 to x^n are 1, 1, 1, 1, 1\. 
So frequency of digits is 0 5 0 0 0 0 0 0 0 0\. 
```

**进场:**

1.  维护一个频率计数数组来存储数字 0-9 的计数。
2.  遍历从 x^1 到 x^n 的每个数字，对于每个数字，在频率计数数组中的相应索引上加 1。
3.  打印频率阵列

下面是上述方法的实现:

## C++

```
// CPP implementation of above approach
#include<bits/stdc++.h>
using namespace std;

// Function that traverses digits in a number and
// modifies frequency count array
void countDigits(double val, long arr[])
{
    while ((long)val > 0) {
        long digit = (long)val % 10;
        arr[(int)digit]++;
        val = (long)val / 10;
    }
    return;
}

void countFrequency(int x, int n)
{

    // Array to keep count of digits
    long freq_count[10]={0};

    // Traversing through x^1 to x^n
    for (int i = 1; i <= n; i++)
    {
        // For power function, both its parameters are
        // to be in double
        double val = pow((double)x, (double)i);
        // calling countDigits function on x^i
        countDigits(val, freq_count);
    }

    // Printing count of digits 0-9
    for (int i = 0; i <= 9; i++)
    {
        cout << freq_count[i] <<  " ";
    }
}
// Driver code
int main()
{
    int x = 15, n = 3;
    countFrequency(x, n);
}
// This code is contributed by ihritik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;
import java.util.*;
public class GFG {

    // Function that traverses digits in a number and
    // modifies frequency count array
    static void countDigits(double val, long[] arr)
    {
        while ((long)val > 0) {
            long digit = (long)val % 10;
            arr[(int)digit]++;
            val = (long)val / 10;
        }
        return;
    }

    static void countFrequency(int x, int n)
    {

        // Array to keep count of digits
        long[] freq_count = new long[10];

        // Traversing through x^1 to x^n
        for (int i = 1; i <= n; i++) {
            // For power function, both its parameters are
            // to be in double
            double val = Math.pow((double)x, (double)i);
            // calling countDigits function on x^i
            countDigits(val, freq_count);
        }

        // Printing count of digits 0-9
        for (int i = 0; i <= 9; i++) {
            System.out.print(freq_count[i] + " ");
        }
    }
    // Driver code
    public static void main(String args[])
    {
        int x = 15, n = 3;
        countFrequency(x, n);
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation
# of above approach
import math

# Function that traverses digits
# in a number and modifies
# frequency count array
def countDigits(val, arr):

    while (val > 0) :
        digit = val % 10
        arr[int(digit)] += 1
        val = val // 10

    return;

def countFrequency(x, n):

    # Array to keep count of digits
    freq_count = [0] * 10

    # Traversing through x^1 to x^n
    for i in range(1, n + 1) :

        # For power function,
        # both its parameters
        # are to be in double
        val = math.pow(x, i)

        # calling countDigits
        # function on x^i
        countDigits(val, freq_count)

    # Printing count of digits 0-9
    for i in range(10) :
        print(freq_count[i], end = " ");

# Driver code
if __name__ == "__main__":

    x = 15
    n = 3
    countFrequency(x, n)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function that traverses digits
// in a number and modifies
// frequency count array
static void countDigits(double val,
                        long[] arr)
{
    while ((long)val > 0)
    {
        long digit = (long)val % 10;
        arr[(int)digit]++;
        val = (long)val / 10;
    }
    return;
}

static void countFrequency(int x, int n)
{

    // Array to keep count of digits
    long[] freq_count = new long[10];

    // Traversing through x^1 to x^n
    for (int i = 1; i <= n; i++)
    {
        // For power function, both its
        // parameters are to be in double
        double val = Math.Pow((double)x,
                              (double)i);

        // calling countDigits
        // function on x^i
        countDigits(val, freq_count);
    }

    // Printing count of digits 0-9
    for (int i = 0; i <= 9; i++)
    {
        Console.Write(freq_count[i] + " ");
    }
}

// Driver code
public static void Main()
{
    int x = 15, n = 3;
    countFrequency(x, n);
}
}

// This code is contributed
// by Shashank
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function that traverses digits
// in a number and modifies
// frequency count array
function countDigits($val, &$arr)
{
    while ($val > 0)
    {
        $digit = $val % 10;
        $arr[(int)($digit)] += 1;
        $val = (int)($val / 10);
    }
    return;
}

function countFrequency($x, $n)
{

    // Array to keep count of digits
    $freq_count = array_fill(0, 10, 0);

    // Traversing through x^1 to x^n
    for ($i = 1; $i < $n + 1; $i++)
    {

        // For power function,
        // both its parameters
        // are to be in double
        $val = pow($x, $i);

        // calling countDigits
        // function on x^i
        countDigits($val, $freq_count);
    }
    // Printing count of digits 0-9
    for ($i = 0; $i < 10; $i++)
    {
        echo $freq_count[$i] . " ";
}
}

// Driver code
$x = 15;
$n = 3;
countFrequency($x, $n)

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

    // Function that traverses digits in a number and
    // modifies frequency count array
    function countDigits(val,arr)
    {
        while (val > 0) {
            let digit = val % 10;
            arr[digit]++;
            val = Math.floor(val / 10);
        }
        return;
    }

    function countFrequency(x,n)
    {
        // Array to keep count of digits
        let freq_count = new Array(10);
          for(let i=0;i<10;i++)
        {
            freq_count[i]=0;
        }
        // Traversing through x^1 to x^n
        for (let i = 1; i <= n; i++) {
            // For power function, both its parameters are
            // to be in double
            let val = Math.pow(x, i);
            // calling countDigits function on x^i
            countDigits(val, freq_count);
        }

        // Printing count of digits 0-9
        for (let i = 0; i <= 9; i++) {
            document.write(freq_count[i] + " ");
        }
    }

    // Driver code
    let x = 15, n = 3;
    countFrequency(x, n);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
0 1 2 2 0 3 0 1 0 0
```