# 一个数的倍数之和直到 N

> 原文:[https://www.geeksforgeeks.org/sum-multiples-number-n/](https://www.geeksforgeeks.org/sum-multiples-number-n/)

给定一个数 a 和极限 n，求 a 到 n 的倍数之和

**示例:**

```
Input : a = 4, N = 23
Output : sum = 60
[Multiples : 4, 8, 12, 16, 20]

Input :a = 7, N = 49
Output :sum = 196
[Multiples: 7, 14, 21, 28, 35, 42, 49]
```

基本思想是从 i = a 迭代到 i = n，i++并检查 i % a == 0 与否。如果为零，则将 I 加到 sum 上(最初 sum = 0)。这样我们就会得到总数。这需要时间。
我们可以将循环修改为 i = a，i < = n，i = i + a，以减少迭代次数。但是如果有 a 的 m 倍
也需要 O(m)时间，为了在 O(1)时间内得到结果，我们可以使用 n 个自然数求和的公式。对于上面的例子，
a = 4，N = 23，a 的倍数，m = N/a(整数除法)。倍数是 4，8，12，16，20。
我们可以写成 4 X [1，2，3，4，5]。所以我们可以得到倍数之和为:

```
 sum = a * (Summation of 1 to m [natural numbers from 1 to m]) 
 sum = 4 * (m*(m+1) / 2)
 sum = 4 * (5*6 / 2) = 4 * 15 = 60 

```

## C++

```
// C++ program to find sum of multiples of a number
// up to N efficiently
#include <iostream>
using namespace std;

// Function for calculating sum of multiples of
// a upto N
int calculate_sum(int a, int N)
{
    // Number of multiples
    int m = N / a;

    // sum of first m natural numbers
    int sum = m * (m + 1) / 2;

    // sum of multiples
    int ans = a * sum;

    return ans;
}

// Driver code
int main()
{
    int a = 7, N = 49;
    cout << "Sum of multiples of "
         << a << " up to " << N << " = "
         << calculate_sum(a, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of multiples
// of a number up to N efficiently

class GFG {

// Function for calculating sum
// of multiples of a upto N
static int calculate_sum(int a, int N) {

    // Number of multiples
    int m = N / a;

    // sum of first m natural numbers
    int sum = m * (m + 1) / 2;

    // sum of multiples
    int ans = a * sum;

    return ans;
}

// Driver code
public static void main(String[] args) {

    int a = 7, N = 49;
    System.out.println("Sum of multiples of " + a +
                       " up to " + N + " = " +
                               calculate_sum(a, N));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
"""Python program to find sum of
multiples of a number up to N"""

# Calculates sum of multiples of
# a number upto N
def calculate_sum(a, N):

    # Number of multiples
    m = N / a

    # sum of first m natural numbers
    sum = m * (m + 1) / 2

    # sum of multiples
    ans = a * sum

    print("Sum of multiples of ", a,
          " up to ", N, " = ", ans)

# Driver Code
calculate_sum(7, 49)

# This code is contributed by Abhishek Agrawal.
```

## C#

```
// C# program to find sum of multiples
// of a number up to N efficiently
using System;

class GFG {

    // Function for calculating sum
    // of multiples of a upto N
    static int calculate_sum(int a, int N)
    {

        // Number of multiples
        int m = N / a;

        // sum of first m natural numbers
        int sum = m * (m + 1) / 2;

        // sum of multiples
        int ans = a * sum;

        return ans;
    }

    // Driver code
    public static void Main()
    {

        int a = 7, N = 49;
        Console.WriteLine("Sum of multiples of " + a +
         " up to " + N + " = " + calculate_sum(a, N));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum
// of multiples of a number
// up to N efficiently

// Function for calculating sum
// of multiples of a upto N
function calculate_sum($a, $N)
{
    // Number of multiples
    $m = $N / $a;

    // sum of first m
    // natural numbers
    $sum = $m * ($m + 1) / 2;

    // sum of multiples
    $ans = $a * $sum;

    return $ans;
}

// Driver code
$a = 7;
$N = 49;
echo "Sum of multiples of ". $a ,
         " up to " . $N . " = " .
          calculate_sum($a, $N) ;

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum
// of multiples of a number
// up to N efficiently

// Function for calculating sum
// of multiples of a upto N
function calculate_sum(a, N)
{

    // Number of multiples
    m = N / a;

    // Sum of first m
    // natural numbers
    sum = m * (m + 1) / 2;

    // Sum of multiples
    ans = a * sum;

    return ans;
}

// Driver code
let a = 7;
let N = 49;

document.write("Sum of multiples of "+ a +
               " up to " + N + " = " +
               calculate_sum(a, N));

// This code is contributed by mohan1240760

</script>
```

**输出:**

```
Sum of multiples of 7 upto 49 = 196
```

本文由 [**苏坎塔南迪**](https://auth.geeksforgeeks.org/profile.php?user=Sukanta_it) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。