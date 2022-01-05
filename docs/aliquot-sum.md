# 等分总和

> 原文:[https://www.geeksforgeeks.org/aliquot-sum/](https://www.geeksforgeeks.org/aliquot-sum/)

在数论中，正整数 n 的 [**等份和**](https://en.wikipedia.org/wiki/Aliquot_sum) s(n)是 n 的所有本征除数之和，即除 n 本身以外的 n 的所有除数。
它们由等分因子的和来定义。除了数本身，数的等分因子是它的所有因子。等分总和是等分因子的总和，例如，等分因子 12 是 1、2、3、4 和 6，等分总和是 16。
等分总和等于其值的数字是完美数字(例如 6)。
**举例:**

```
Input : 12
Output : 16
Explanation :
Proper divisors of 12 is = 1, 2, 3, 4, 6 
and sum 1 + 2 + 3 + 4 + 6 = 16

Input : 15
Output : 9
Explanation :
Proper divisors of 15 is 1, 3, 5
and sum 1 + 3 + 5 = 9
```

一个**简单的解决方案**是遍历所有小于 n 的数，对于每个数 I，检查 I 是否除以 n，如果是，我们将其加到结果中。

## C++

```
// CPP program for aliquot sum
#include <iostream>
using namespace std;

// Function to calculate sum of
// all proper divisors
int aliquotSum(int n)
{
    int sum = 0;
    for (int i = 1; i < n; i++)
        if (n % i == 0)
            sum += i;       

    return sum;
}

// Driver Code
int main()
{
    int n = 12;
    cout << aliquotSum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for aliquot sum
import java.io.*;

class GFG {

    // Function to calculate sum of
    // all proper divisors
    static int aliquotSum(int n)
    {
        int sum = 0;
        for (int i = 1; i < n; i++)
            if (n % i == 0)
                sum += i;

        return sum;
    }

    // Driver Code
    public static void main(String args[])
                           throws IOException
    {
        int n = 12;
        System.out.println(aliquotSum(n));
    }
}

/* This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program for aliquot sum

# Function to calculate sum of
# all proper divisors
def aliquotSum(n) :
    sm = 0
    for i in range(1,n) :
        if (n % i == 0) :
            sm = sm + i    

    return sm # return sum

# Driver Code
n = 12
print(aliquotSum(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program for aliquot sum
using System;

class GFG {

    // Function to calculate sum of
    // all proper divisors
    static int aliquotSum(int n)
    {
        int sum = 0;
        for (int i = 1; i < n; i++)
            if (n % i == 0)
                sum += i;

        return sum;
    }

    // Driver Code
    public static void Main()

    {
        int n = 12;
        Console.WriteLine(aliquotSum(n));
    }
}

/* This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for aliquot sum

// Function to calculate sum of
// all proper divisors
function aliquotSum($n)
{
    $sum = 0;
    for ($i = 1; $i < $n; $i++)
        if ($n % $i == 0)
            $sum += $i;    

    return $sum;
}

// Driver Code
$n = 12;
echo(aliquotSum($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program for aliquot sum

// Function to calculate sum of
// all proper divisors
    function aliquotSum(n)
    {
        let sum = 0;
        for (let i = 1; i < n; i++)
            if (n % i == 0)
                sum += i;

        return sum;
    }

// Driver code

        let n = 12;
        document.write(aliquotSum(n));

</script>
```

**输出:**

```
16
```

**有效解:**
[自然数所有适当因子之和](https://www.geeksforgeeks.org/sum-of-all-proper-divisors-of-a-natural-number/)
[自然数所有因子之和](https://www.geeksforgeeks.org/sum-factors-number/)