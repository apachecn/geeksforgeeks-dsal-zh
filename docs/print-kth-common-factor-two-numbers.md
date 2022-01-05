# 打印两个数的第 k 个公因子

> 原文:[https://www . geesforgeks . org/print-kth-common-factor-two-numbers/](https://www.geeksforgeeks.org/print-kth-common-factor-two-numbers/)

给定三个数字 x，y 和 k，求 x 和 y 的第 k 个公因数，如果 x 和 y 的公因数小于 k，则打印-1 .
**例:**

```
Input : x = 20, y = 24
        k = 3
Output : 4
Common factors are 1, 2, 4, ...

Input : x = 4, y = 24
        k = 2
Output : 2

Input : x = 22, y = 2
        k = 3
Output : -1
```

我们发现两个数中较小的一个作为公因数不能大于较小的一个数。然后我们运行一个从 1 到较小数字的循环。对于每个数字 I，我们检查它是否是一个共同因素。如果是，我们增加公共因子的计数。
下面是实现:

## C++

```
// C++ program to find kth common factor
// of two numbers
#include<iostream>
using namespace std;

// Returns k'th common factor of x and y.
int findKCF(int x, int y, int k)
{
   // Find smaller of two numbers
   int small = min(x, y);

   // Count common factors until we either
   // reach small or count becomes k.
   int count = 1;
   for (int i=2; i<=small; i++)
   {
      if (x % i==0 && y % i == 0)
         count++;
      if (count == k)
         return i;
   }

   // If we reached small
   return -1;
}

// Driver code
int main()
{
   int x = 4, y = 24, k = 3;
   cout << findKHCF(x, y, k);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find kth
// common factor of two numbers
import java.lang.*;

class GFG {

// Returns k'th common factor of x and y.
static int findKHCF(int x, int y, int k) {

    // Find smaller of two numbers
    int small = Math.min(x, y);

    // Count common factors until we either
    // reach small or count becomes k.
    int count = 1;
    for (int i = 2; i <= small; i++) {
    if (x % i == 0 && y % i == 0)
        count++;
    if (count == k)
        return i;
    }

    // If we reached small
    return -1;
}

// Driver code
public static void main(String[] args) {

    int x = 4, y = 24, k = 3;
    System.out.print(findKHCF(x, y, k));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find
# kth common factor
# of two numbers

# Returns k'th common
# factor of x and y.
def findKHCF(x,y,k):

    # Find smaller of two numbers
    small = min(x, y)

    # Count common factors
    # until we either
    # reach small or count
    # becomes k.
    count = 1
    for i in range(2,small+1):

        if (x % i==0 and y % i == 0):
            count=count + 1
        if (count == k):
            return i

    # If we reached small
    return -1

# Driver code

x = 4
y = 24
k = 3
print(findKHCF(x, y, k))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find kth
// common factor of two numbers
using System;

class GFG {

// Returns k'th common factor of x and y.
static int findKHCF(int x, int y, int k)
{

    // Find smaller of two numbers
    int small = Math.Min(x, y);

    // Count common factors until we either
    // reach small or count becomes k.
    int count = 1;
    for (int i = 2; i <= small; i++)
    {
        if (x % i == 0 && y % i == 0)
            count++;
        if (count == k)
            return i;
    }

    // If we reached small
    return -1;
}

// Driver code
public static void Main()
{
    int x = 4, y = 24, k = 3;
    Console.Write(findKHCF(x, y, k));
}
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find kth
// common factor of two numbers

// Returns k'th common
// factor of x and y.
function findKCF($x, $y, $k)
{
// Find smaller of two numbers
$small = min($x, $y);

// Count common factors until we either
// reach small or count becomes k.
$count = 1;
for ($i = 2; $i <= $small; $i++)
{
    if ($x % $i == 0 && $y % $i == 0)
        $count++;
    if ($count == $k)
        return $i;
}

// If we reached small
return -1;
}

// Driver code
$x = 4; $y = 24; $k = 3;
echo findKCF($x, $y, $k);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to find kth
// common factor of two numbers

// Returns k'th common factor of x and y.
function findKHCF(x, y, k) {

    // Find smaller of two numbers
    let small = Math.min(x, y);

    // Count common factors until we either
    // reach small or count becomes k.
    let count = 1;
    for (let i = 2; i <= small; i++) {
    if (x % i == 0 && y % i == 0)
        count++;
    if (count == k)
        return i;
    }

    // If we reached small
    return -1;
}

// Driver code   

    let x = 4, y = 24, k = 3;
    document.write(findKHCF(x, y, k));

</script>
```

**输出:**

```
4
```

本文由**阿夫扎尔·安萨里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。