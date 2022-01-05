# 给定数字与给定幂的位数之和

> 原文:[https://www . geesforgeks . org/sum-digits-given-number-given-power/](https://www.geeksforgeeks.org/sum-digits-given-number-given-power/)

给定一个数，我们需要求一个数的所有数字的和，这个数是我们把这个数升到指定的幂之后得到的。
示例:

```
Input: number = 5, power = 4 
Output: 13
Explanation:
Raising 5 to the power 4 we get 625.
Now adding all the digits = 6 + 2 + 5

Input: number = 9, power = 5
Output: 27
Explanation:
Raising 9 to the power 5 we get 59049.
Now adding all the digits = 5 + 9 + 0 + 4 + 9
```

解释了 Python 的方法。我们使用了 pow()函数来计算功率值的基数。然后我们使用 str()方法将每个数字提取为字符串。由于我们无法计算字符串的总和，所以我们使用 int()方法将每个字符串数字转换回整数。最后，我们用 sum()函数得到所有数字的和。这个解决方案在 Python 中看起来非常简单，但在其他语言中就不会这么短了。在运行这两个代码后，可以比较给定语言(即 Python 和 Java)中所用的时间和内存。
以下是上述思路的实现:

## C++

```
// CPP program to illustrate the given problem
#include<bits/stdc++.h>
using namespace std;

int calculate(int n, int power)
{
    int sum = 0;
    int bp = (int)pow(n, power);
    while (bp != 0) {
        int d = bp % 10;
        sum += d;
        bp /= 10;
    }
    return sum;
}

// Driver Code
int main()
{
    int n = 5;
    int power = 4;
    cout << calculate(n, power);
}

// This code is contributed by Nikita Tiwari
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate the given problem
public class base_power {
    static int calculate(int n, int power)
    {
        int sum = 0;
        int bp = (int)Math.pow(n, power);
        while (bp != 0) {
            int d = bp % 10;
            sum += d;
            bp /= 10;
        }
        return sum;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 5;
        int power = 4;
        System.out.println(calculate(n, power));
    }
}
```

## 蟒蛇 3

```
# Python program to illustrate the given problem
def calculate(n, power):
    return sum([int(i) for i in str(pow(n, power))])

# Driver Code
n = 5
power = 4
print (calculate(n, power))
```

## C#

```
// C# program to find sum of digits of
// a given number to a given power
using System;

public class base_power
{

    // Function to calculate sum
    static int calculate(int n, int power)
    {
        int sum = 0;
        int bp = (int)Math.Pow(n, power);
        while (bp != 0)
        {
            int d = bp % 10;
            sum += d;
            bp /= 10;
        }
        return sum;
    }

    // Driver Code
    public static void Main()
    {
        int n = 5;
        int power = 4;
        Console.WriteLine(calculate(n, power));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to illustrate
// the given problem

function calculate($n, $power)
{

    $sum = 0;
    $bp = (int)pow($n, $power);
    while ($bp != 0)
    {
        $d = $bp % 10;
        $sum += $d;
        $bp /= 10;
    }
    return $sum;
}

// Driver Code
$n = 5;
$power = 4;
echo(calculate($n, $power));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Program to illustrate the given problem

   function calculate( n,  power)
{
     sum = 0;
     bp = Math.pow(n, power);
    while (bp != 0) {
         d = bp % 10;
        sum =sum+ d;
        bp = Math.floor(bp/ 10);
    }
    return sum;
}

// Driver Code

     n = 5;
     power = 4;
    document.write(calculate(n, power));

// This code is contributed by simranarora5sos

</script>
```

**输出:**

```
13
```

本文由 [**【钦莫伊蕾恩卡】**](https://www.linkedin.com/in/lenkachinmoy/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。