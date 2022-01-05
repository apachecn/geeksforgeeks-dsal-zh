# 系列之和 2^0 + 2^1 + 2^2 +…..+ 2^n

> 原文:[https://www . geesforgeks . org/系列之和-20-21-22-2n/](https://www.geeksforgeeks.org/sum-of-the-series-20-21-22-2n/)

给定一个整数 N，任务是求数列 2<sup>0</sup>+2<sup>1</sup>+2<sup>2</sup>+2<sup>3</sup>+…。+ 2 <sup>n</sup> 。
**举例:**

> **输入:**5
> T3【输出】:31
> 2<sup>0</sup>2<sup>1</sup>+2222+2<sup>+2<sup>+2+8<sup>+9</sup>= 1+2+</sup></sup>

一个**天真的做法**是计算总和就是把 2 的每一次幂从 0 加到 n 上
下面是上面做法的实现:

## C++

```
// C++ program to find sum
#include <bits/stdc++.h>
using namespace std;

// function to calculate sum of series
int calculateSum(int n)
{
    // initialize sum as 0
    int sum = 0;

    // loop to calculate sum of series
    for (int i = 0; i < n; i++) {

        // calculate 2^i
        // and add it to sum

        sum = sum + (1 << i);
    }
    return sum;
}

// Driver code
int main()
{
    int n = 10;
    cout << "Sum of series of power of 2 is : "
         << calculateSum(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum
class GFG {
    // function to calculate sum of series
    static int calculate sum(int n)
    {
        // initialize sum as 0
        int sum = 0;

        // loop to calculate sum of series
        for (int i = 0; i < n; i++) {

            // calculate 2^i
            // and add it to sum

            sum = sum + (1 << i);
        }
        return sum;
    }
    // Main function
    public static void main(String[] args)
    {

        int n = 10;
        System.out.println("Sum of the series : " + calculateSum(n));
    }
};
```

## 蟒蛇 3

```
# Python3 program to calculate
# sum of series of power of 2

# function to calculate sum of series
def calculateSum(n):
     sum = 0

     # loop to calculate sum of series
     for i in range (0, n):

         # calculate 2 ^ i
         sum = sum+ (1 << i)

     return sum

# Driver code
n = 10
print("Sum of series ", calculateSum(n))
```

## C#

```
// C# program to find sum
using System;

class GFG
{
    // function to calculate
    // sum of series
    static int calculateSum(int n)
    {
        // initialize sum as 0
        int sum = 0;

        // loop to calculate
        // sum of series
        for (int i = 0; i < n; i++)
        {

            // calculate 2^i
            // and add it to sum

            sum = sum + (1 << i);
        }
        return sum;
    }

    // Driver code
    public static void Main()
    {
        int n = 10;
        Console.WriteLine("Sum of the series : " +
                                 calculateSum(n));
    }
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of the
// series 2^0 + 2^1 + 2^2 +…..+ 2^n

// function to calculate
// sum of series
function calculateSum($n)
{
    // initialize sum as 0
    $sum = 0;

    // loop to calculate
    // sum of series
    for ($i = 0; $i < $n; $i++)
    {

        // calculate 2^i
        // and add it to sum

        $sum = $sum + (1 << $i);
    }
    return $sum;
}

// Driver code
$n = 10;
echo "Sum of the series of " .
              "power 2 is : ",
             calculateSum($n);

// This code is contributed
// by Smitha
?>
```

## java 描述语言

```
<script>

// Javascript  program to find sum of the
// series 2^0 + 2^1 + 2^2 +…..+ 2^n

// function to calculate
// sum of series
function calculateSum(n)
{
    // initialize sum as 0
    let sum = 0;

    // loop to calculate
    // sum of series
    for (let i = 0; i < n; i++)
    {

        // calculate 2^i
        // and add it to sum

        sum = sum + (1 << i);
    }
    return sum;
}

// Driver code
let n = 10;
document.write("Sum of the series of power 2 is : "
                           + calculateSum(n))

//This code is contributed by sravan kumar
</script>
```

**Output:** 

```
Sum of series of power of 2 is : 1023
```

**时间复杂度:** O(n)
一种**有效的方法**是找到 2^(n+1)并从中减去 1，因为我们知道 2^n 可以写成:

```
2n = ( 20+21+22+23+24 +...... 2n-1) +1
```

以下是上述方法的实现:

## C++

```
// C++ program to find sum
#include <bits/stdc++.h>
using namespace std;

int calculateSum(int n)
{
    // calculate  and return 2^(n+1) -1
    return (1 << (n + 1)) - 1;
}

int main()
{
    int n = 10;
    cout << "Sum of series of power of 2 is :"
         << calculateSum(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// sum of series of power of 2

class GFG {

    // function to calculate sum of series
    static int calculate sum(int n)
    {

        // calculate 2^(n+1)
        int sum = (1 << (n + 1));
        return sum - 1;
    }

    // Driver code
    public static void main(String[] args)
    {

        int n = 10;
        System.out.println("Sum of the series of power 2 is : "
                           + calculateSum(n));
    }
};
```

## 蟒蛇 3

```
# Python3 program to calculate
# sum of series of 2's power

# function to calculate sum of series
def calculateSum(n):

      # calculate 2^(n + 1)
      sum = (1 << (n + 1))
      return sum-1

# Driver code
n = 10
print("Sum of series ", calculateSum(n))
```

## C#

```
// C# program to calculate
// sum of series of power of 2
using System;
class GFG
{

    // function to calculate
    // sum of series
    static int calculateSum(int n)
    {

        // calculate 2^(n+1)
        int sum = (1 << (n + 1));
        return sum - 1;
    }

    // Driver code
    public static void Main()
    {
        int n = 10;
        Console.Write("Sum of the series " +
                        "of power 2 is : " +
                           calculateSum(n));
    }

// This code is contributed
// by Smitha
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate
// sum of series of power of 2

// function to calculate
// sum of series
function calculateSum($n)
{

    // calculate 2^(n+1)
    $sum = (1 << ($n + 1));
    return $sum - 1;
}

// Driver code
$n = 10;
echo "Sum of the series of " .
              "power 2 is : ",
             calculateSum($n);

// This code is contributed
// by Smitha
```

## java 描述语言

```
<script>

// Javascript program to calculate
// sum of series of power of 2

// function to calculate
// sum of series
function calculateSum(n)
{

    // calculate 2^(n+1)
    let sum = (1 << (n + 1));
    return sum - 1;
}

// Driver code
let n = 10;
document.write("Sum of the series of power 2 is : "
                           + calculateSum(n));

// This code is contributed by sravan kumar

</script>
```

**Output:** 

```
Sum of series of power of 2 is :2047
```

**时间复杂度:** O(1)