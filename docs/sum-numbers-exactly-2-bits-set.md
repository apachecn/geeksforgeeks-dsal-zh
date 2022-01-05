# 正好设置了 2 位的数字之和

> 原文:[https://www . geeksforgeeks . org/sum-numbers-just-2-bit-set/](https://www.geeksforgeeks.org/sum-numbers-exactly-2-bits-set/)

给定一个数 n，求 2 位被置位的所有数 n 的和。

**示例:**

```
Input : 10
Output : 33
3 + 5 + 6 + 9 + 10 = 33

Input : 100
Output : 762
```

**天真方法:**找出每个最多 n 个的数字，其 2 位被设置。如果它的 2 位被设置，把它加到和上。

## C++

```
// CPP program to find sum of numbers
// upto n whose 2 bits are set
#include <bits/stdc++.h>
using namespace std;

// To count number of set bits
int countSetBits(int n)
{
    int count = 0;
    while (n) {
        n &= (n - 1);
        count++;
    }
    return count;
}

// To calculate sum of numbers
int findSum(int n)
{
    int sum = 0;

    // To count sum of number
    // whose 2 bit are set
    for (int i = 1; i <= n; i++)
        if (countSetBits(i) == 2)
            sum += i;

    return sum;
}

// Driver program to test above function
int main()
{
    int n = 10;
    cout << findSum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of numbers
// upto n whose 2 bits are set
public class Main {

    // To count number of set bits
    static int countSetBits(int n)
    {
        int count = 0;
        while (n > 0) {
            n &= (n - 1);
            count++;
        }
        return count;
    }

    // To calculate sum of numbers
    static int findSum(int n)
    {
        int sum = 0;

        // To count sum of number
        // whose 2 bit are set
        for (int i = 1; i <= n; i++)
            if (countSetBits(i) == 2)
                sum += i;

        return sum;
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        int n = 10;

        System.out.println(findSum(n));
    }
}
```

## 蟒蛇 3

```
# Python program to find
# sum of numbers
# upto n whose 2 bits are set

# To count number of set bits
def countSetBits(n):

    count = 0
    while (n):
        n =n & (n - 1)
        count=count + 1

    return count

# To calculate sum of numbers
def findSum(n):

    sum = 0

    # To count sum of number
    # whose 2 bit are set
    for i in range(1,n+1):
        if (countSetBits(i) == 2):
            sum =sum + i

    return sum

# Driver code
n = 10
print(findSum(n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find sum of
// numbers upto n whose 2
// bits are set
using System;

class GFG
{

    // To count number
    // of set bits
    static int countSetBits(int n)
    {
        int count = 0;
        while (n > 0)
        {
            n = n & (n - 1);
            count++;
        }
        return count;
    }

    // To calculate
    // sum of numbers
    static int findSum(int n)
    {
        int sum = 0;

        // To count sum of number
        // whose 2 bit are set
        for (int i = 1; i <= n; i++)
            if (countSetBits(i) == 2)
                sum += i;

        return sum;
    }

    // Driver Code
    static public void Main ()
    {
        int n = 10;

        Console.WriteLine(findSum(n));
    }
}

// This code is contributed by aj_36
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of numbers
// upto n whose 2 bits are set

// To count number of set bits
function countSetBits($n)
{
    $count = 0;
    while ($n)
    {
        $n &= ($n - 1);
        $count++;
    }
    return $count;
}

// To calculate sum of numbers
function findSum($n)
{
    $sum = 0;

    // To count sum of number
    // whose 2 bit are set
    for ($i = 1; $i <= $n; $i++)
        if (countSetBits($i) == 2)
            $sum += $i;

    return $sum;
}

    // Driver Code
    $n = 10;
    echo findSum($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of numbers
// upto n whose 2 bits are set

// To count number of set bits
function countSetBits(n)
{
    let count = 0;
    while (n) {
        n &= (n - 1);
        count++;
    }
    return count;
}

// To calculate sum of numbers
function findSum(n)
{
    let sum = 0;

    // To count sum of number
    // whose 2 bit are set
    for (let i = 1; i <= n; i++)
        if (countSetBits(i) == 2)
            sum += i;

    return sum;
}

// Driver program to test above function

    let n = 10;
    document.write(findSum(n));

// This code is contributed by Mayank Tyagi
</script>
```

**输出:**

```
33
```

**有效的方法:**其 2 位被设置的数字是 2^x + 2^y 的形式，并且这个数字小于 n。因此我们必须只找到范围直到 n 的数字，其是 2^i + 2^j 的形式，其中 i > 0 和 2^i < n 和 0 < = j < i.

## C++

```
// C++ program to find sum of numbers
// upto n whose 2 bits are set
#include <bits/stdc++.h>
using namespace std;

// To calculate sum of numbers
int findSum(int n)
{
    int sum = 0;

    // Find numbers whose 2 bits are set
    for (int i = 1; (1 << i) < n; i++) {
        for (int j = 0; j < i; j++) {
            int num = (1 << i) + (1 << j);

            // If number is greater then n
            // we don't include this in sum
            if (num <= n)
                sum += num;
        }
    }

    // Return sum of numbers
    return sum;
}

// Driver program to test findSum()
int main()
{
    int n = 10;
    cout << findSum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of numbers
// upto n whose 2 bits are set
public class Main {

    // To calculate sum of numbers
    static int findSum(int n)
    {
        int sum = 0;

        // Find numbers whose 2 bits are set
        for (int i = 1; 1 << i < n; i++) {
            for (int j = 0; j < i; j++) {
                int num = (1 << i) + (1 << j);

                // If number is greater then n
                // we don't include this in sum
                if (num <= n)
                    sum += num;
            }
        }

        // Return sum of numbers
        return sum;
    }

    // Driver program to test findSum()
    public static void main(String[] args)
    {
        int n = 10;
        System.out.println(findSum(n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find sum of
# numbers upto n whose 2 bits are set

# To calculate sum of numbers
def findSum(n) :

    sum = 0

    # Find numbers whose 2
    # bits are set
    i = 1
    while((1 << i) < n ) :
        for j in range(0, i) :
            num = (1 << i) + (1 << j)

            # If number is greater then n
            # we don't include this in sum
            if (num <= n) :
                sum += num

        i += 1

    # Return sum of numbers
    return sum

# Driver Code
n = 10
print(findSum(n))

# This code is contributed
# by Smitha
```

## C#

```
// C# program to find sum of numbers
// upto n whose 2 bits are set
using System;

public class main {

    // To calculate sum of numbers
    static int findSum(int n)
    {
        int sum = 0;

        // Find numbers whose 2 bits are set
        for (int i = 1; 1 << i < n; i++)
        {
            for (int j = 0; j < i; j++)
            {
                int num = (1 << i) + (1 << j);

                // If number is greater then n
                // we don't include this in sum
                if (num <= n)
                    sum += num;
            }
        }

        // Return sum of numbers
        return sum;
    }

    // Driver Code
    public static void Main(String []args)
    {
        int n = 10;
        Console.WriteLine(findSum(n));
    }
}

// This Code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
<?php
// PHP program to find sum of numbers
// upto n whose 2 bits are set

// To calculate sum of numbers
function findSum($n)
{
    $sum = 0;

    // Find numbers whose 2 bits are set
    for ($i = 1; (1 << $i) < $n; $i++)
    {
        for ($j = 0; $j < $i; $j++)
        {
            $num = (1 << $i) + (1 << $j);

            // If number is greater then n
            // we don't include this in sum
            if ($num <= $n)
                $sum += $num;
        }
    }

    // Return sum of numbers
    return $sum;
}

// Driver Code
$n = 10;
echo findSum($n);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to find sum of numbers
    // upto n whose 2 bits are set

    // To calculate sum of numbers
    function findSum(n)
    {
        let sum = 0;

        // Find numbers whose 2 bits are set
        for (let i = 1; 1 << i < n; i++)
        {
            for (let j = 0; j < i; j++)
            {
                let num = (1 << i) + (1 << j);

                // If number is greater then n
                // we don't include this in sum
                if (num <= n)
                    sum += num;
            }
        }

        // Return sum of numbers
        return sum;
    }

    let n = 10;
      document.write(findSum(n));

</script>
```

**输出:**

```
33
```

本文由**核素**投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。