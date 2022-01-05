# 两两乘积之和

> 原文:[https://www.geeksforgeeks.org/sum-pairwise-products/](https://www.geeksforgeeks.org/sum-pairwise-products/)

对于给定的任何无符号整数 n，求∑(i*j)的最终值，其中(1 <=i<=n) and (i <= j <= n).
**示例:**

```
Input : n = 3
Output : 25
We get the sum as following. Note that
first term i varies from 1 to 3 and second
term values from value of first term to n.
1*1 + 1*2 + 1*3 + 2*2 + 2*3 + 3*3 = 25

Input : 5
Output : 140
```

**方法 1(简单)**我们运行两个循环，计算所需的和。

## C++

```
// Simple CPP program to find sum
// of given series.
#include <bits/stdc++.h>
using namespace std;

long long int findSum(int n)
{
   long long int sum = 0;
   for (int i=1; i<=n; i++)
     for (int j=i; j<=n; j++)
        sum = sum + i*j;
   return sum;
}

int main()
{
    int n = 5;
    cout << findSum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program to find sum
// of given series.
class GFG {

    static int findSum(int n)
    {
        int sum = 0;

        for (int i=1; i<=n; i++)
            for (int j=i; j<=n; j++)
                sum = sum + i*j;

        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {

        int n = 5;

        System.out.println(findSum(n));
    }
}

// This code is contributed by Smitha Dinesh Semwal.
```

## 蟒蛇 3

```
# Simple Python3 program to  
# find sum of given series.

def findSum(n) :
    sm = 0
    for i in range(1, n + 1) :
        for j in range(i, n + 1) :
            sm = sm + i * j

    return sm

# Driver Code
n = 5
print(findSum(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// Simple C# program to find sum
// of given series.
class GFG {

    static int findSum(int n)
    {
        int sum = 0;

        for (int i=1; i<=n; i++)
            for (int j=i; j<=n; j++)
                sum = sum + i*j;

        return sum;
    }

    // Driver code
    public static void Main()
    {

        int n = 5;

        System.Console.WriteLine(findSum(n));
    }
}

// This code is contributed by mits.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP program to find sum
// of given series.

function findSum($n)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        for ($j = $i; $j <= $n; $j++)
            $sum = $sum + $i * $j;
    return $sum;
}

// Driver Code
$n = 5;
echo findSum($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Simple JavaScript program to find sum
// of given series.

    function findSum(n)
    {
        let sum = 0;

        for (let i=1; i<=n; i++)
            for (let j=i; j<=n; j++)
                sum = sum + i*j;

        return sum;
    }

// Driver Code

        let n = 5;

        document.write(findSum(n));

</script>
```

**Output:** 

```
140
```