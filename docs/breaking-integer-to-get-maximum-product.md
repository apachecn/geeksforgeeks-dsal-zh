# 打破一个整数得到最大乘积

> 原文:[https://www . geesforgeks . org/breaking-integer-to-get-max-product/](https://www.geeksforgeeks.org/breaking-integer-to-get-maximum-product/)

给定一个数字 n，任务是分解 n，使其各部分的乘法最大化。

```
Input : n = 10
Output : 36
10 = 4 + 3 + 3 and 4 * 3 * 3 = 36
is maximum possible product.

Input : n = 8
Output : 18
8 = 2 + 3 + 3 and 2 * 3 * 3 = 18
is maximum possible product.
```

数学上，我们被给定 n，我们需要最大化 a1 * a2 * a3 …* aK，使得 n = a1 + a2 + a3 … + aK 和 a1，a2，… ak > 0。
注意，为了使乘积最大化，我们需要在这个问题中至少将给定的 Integer 分成两部分。

**方法 1–**

现在我们从极大极小概念中知道，如果一个整数需要分成两部分，那么为了最大化它们的乘积，这两部分应该相等。利用这个概念，让 n 分解成(n/x) x，那么它们的乘积将是 x <sup>(n/x)</sup> ，现在，如果我们取这个乘积的导数，使它等于 0，对于最大乘积，我们将知道 x 的值应该是 e(自然对数的底)。我们知道 2 < e < 3，所以我们应该把每个整数分解成 2 或 3，只求最大乘积。
接下来的事情是 6 = 3 + 3 = 2 + 2 + 2，但是 3 * 3 > 2 * 2 * 2，也就是每一个三元组 2 都可以用三元组 3 来代替最大乘积，所以我们将继续只用 3 来打破这个数，直到这个数保持为 4 或 2，我们将分别被打破为 2*2 (2*2 > 3*1)和 2，我们将得到我们的最大乘积。
简而言之，获得最大乘积的程序如下——尝试仅用 3 的幂破开整数，当整数保持小时(< 5)，然后使用蛮力。
下面程序的复杂度为 O(log N)，因为[重复平方幂法](https://www.geeksforgeeks.org/write-a-c-program-to-calculate-powxn/)。

下面是上述方法的实现:

## C++

```
// C/C++ program to find maximum product by breaking
// the Integer
#include <bits/stdc++.h>
using namespace std;

// method return x^a in log(a) time
int power(int x, int a)
{
    int res = 1;
    while (a) {
        if (a & 1)
            res = res * x;
        x = x * x;
        a >>= 1;
    }
    return res;
}

// Method returns maximum product obtained by
// breaking N
int breakInteger(int N)
{
    //  base case 2 = 1 + 1
    if (N == 2)
        return 1;

    //  base case 3 = 2 + 1
    if (N == 3)
        return 2;

    int maxProduct;

    //  breaking based on mod with 3
    switch (N % 3) {
    // If divides evenly, then break into all 3
    case 0:
        maxProduct = power(3, N / 3);
        break;

    // If division gives mod as 1, then break as
    // 4 + power of 3 for remaining part
    case 1:
        maxProduct = 2 * 2 * power(3, (N / 3) - 1);
        break;

    // If division gives mod as 2, then break as
    // 2 + power of 3 for remaining part
    case 2:
        maxProduct = 2 * power(3, N / 3);
        break;
    }
    return maxProduct;
}

//  Driver code to test above methods
int main()
{
    int maxProduct = breakInteger(10);
    cout << maxProduct << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum product by breaking
// the Integer

class GFG {
    // method return x^a in log(a) time
    static int power(int x, int a)
    {
        int res = 1;
        while (a > 0) {
            if ((a & 1) > 0)
                res = res * x;
            x = x * x;
            a >>= 1;
        }
        return res;
    }

    // Method returns maximum product obtained by
    // breaking N
    static int breakInteger(int N)
    {
        // base case 2 = 1 + 1
        if (N == 2)
            return 1;

        // base case 3 = 2 + 1
        if (N == 3)
            return 2;

        int maxProduct = -1;

        // breaking based on mod with 3
        switch (N % 3) {
        // If divides evenly, then break into all 3
        case 0:
            maxProduct = power(3, N / 3);
            break;

        // If division gives mod as 1, then break as
        // 4 + power of 3 for remaining part
        case 1:
            maxProduct = 2 * 2 * power(3, (N / 3) - 1);
            break;

        // If division gives mod as 2, then break as
        // 2 + power of 3 for remaining part
        case 2:
            maxProduct = 2 * power(3, N / 3);
            break;
        }
        return maxProduct;
    }

    // Driver code to test above methods
    public static void main(String[] args)
    {
        int maxProduct = breakInteger(10);
        System.out.println(maxProduct);
    }
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find maximum product by breaking
# the Integer

# method return x^a in log(a) time

def power(x, a):

    res = 1
    while (a):
        if (a & 1):
            res = res * x
        x = x * x
        a >>= 1

    return res

# Method returns maximum product obtained by
# breaking N

def breakInteger(N):
    #  base case 2 = 1 + 1
    if (N == 2):
        return 1

    #  base case 3 = 2 + 1
    if (N == 3):
        return 2

    maxProduct = 0

    #  breaking based on mod with 3
    if(N % 3 == 0):
        # If divides evenly, then break into all 3
        maxProduct = power(3, int(N/3))
        return maxProduct
    elif(N % 3 == 1):
        # If division gives mod as 1, then break as
        # 4 + power of 3 for remaining part
        maxProduct = 2 * 2 * power(3, int(N/3) - 1)
        return maxProduct
    elif(N % 3 == 2):
        # If division gives mod as 2, then break as
        # 2 + power of 3 for remaining part
        maxProduct = 2 * power(3, int(N/3))
        return maxProduct

#  Driver code to test above methods

maxProduct = breakInteger(10)
print(maxProduct)

# This code is contributed by mits
```

## C#

```
// C# program to find maximum product by breaking
// the Integer

class GFG {
    // method return x^a in log(a) time
    static int power(int x, int a)
    {
        int res = 1;
        while (a > 0) {
            if ((a & 1) > 0)
                res = res * x;
            x = x * x;
            a >>= 1;
        }
        return res;
    }

    // Method returns maximum product obtained by
    // breaking N
    static int breakInteger(int N)
    {
        // base case 2 = 1 + 1
        if (N == 2)
            return 1;

        // base case 3 = 2 + 1
        if (N == 3)
            return 2;

        int maxProduct = -1;

        // breaking based on mod with 3
        switch (N % 3) {
        // If divides evenly, then break into all 3
        case 0:
            maxProduct = power(3, N / 3);
            break;

        // If division gives mod as 1, then break as
        // 4 + power of 3 for remaining part
        case 1:
            maxProduct = 2 * 2 * power(3, (N / 3) - 1);
            break;

        // If division gives mod as 2, then break as
        // 2 + power of 3 for remaining part
        case 2:
            maxProduct = 2 * power(3, N / 3);
            break;
        }
        return maxProduct;
    }

    // Driver code to test above methods
    public static void Main()
    {
        int maxProduct = breakInteger(10);
        System.Console.WriteLine(maxProduct);
    }
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum product by breaking
// the Integer

// method return x^a in log(a) time
function power($x, $a)
{
    $res = 1;
    while ($a)
    {
        if ($a & 1)
            $res = $res * $x;
        $x = $x * $x;
        $a >>= 1;
    }
    return $res;
}

// Method returns maximum product obtained by
// breaking N
function breakInteger($N)
{
    //  base case 2 = 1 + 1
    if ($N == 2)
        return 1;

    //  base case 3 = 2 + 1
    if ($N == 3)
        return 2;

    $maxProduct=0;

    //  breaking based on mod with 3
    switch ($N % 3)
    {
        // If divides evenly, then break into all 3
        case 0:
            $maxProduct = power(3, $N/3);
            break;

        // If division gives mod as 1, then break as
        // 4 + power of 3 for remaining part
        case 1:
            $maxProduct = 2 * 2 * power(3, ($N/3) - 1);
            break;

        // If division gives mod as 2, then break as
        // 2 + power of 3 for remaining part
        case 2:
            $maxProduct = 2 * power(3, $N/3);
            break;
    }
    return $maxProduct;
}

//  Driver code to test above methods

    $maxProduct = breakInteger(10);
    echo $maxProduct;

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find maximum
// product by breaking the Integer

// Method return x^a in log(a) time
function power(x, a)
{
    let res = 1;

    while (a > 0)
    {
        if ((a & 1) > 0)
            res = res * x;

        x = x * x;
        a >>= 1;
    }
    return res;
}

// Method returns maximum product obtained by
// breaking N
function breakInteger(N)
{

    // Base case 2 = 1 + 1
    if (N == 2)
        return 1;

    // Base case 3 = 2 + 1
    if (N == 3)
        return 2;

    let maxProduct;

    // Breaking based on mod with 3
    switch (N % 3)
    {

        // If divides evenly, then break into all 3
        case 0:
            maxProduct = power(3, N / 3);
            break;

        // If division gives mod as 1, then break as
        // 4 + power of 3 for remaining part
        case 1:
            maxProduct = 2 * 2 * power(3, (N / 3) - 1);
            break;

        // If division gives mod as 2, then break as
        // 2 + power of 3 for remaining part
        case 2:
            maxProduct = 2 * power(3, N / 3);
            break;
    }
    return maxProduct;
}

// Driver code
let maxProduct = breakInteger(10);
document.write(maxProduct);

// This code is contributed by rameshtravel07 

</script>
```

**Output**

```
36
```

**方法 2–**

如果我们看到这个问题的一些例子，我们可以很容易地观察到以下模式。
当尺寸大于 4 时，重复切割尺寸为 3 的零件，保持最后一个零件的尺寸为 2 或 3 或 4，可以获得最大的产品。例如，n = 10，最大乘积由 3，3，4 得到。对于 n = 11，最大乘积由 3，3，3，2 得到。下面是这种方法的实现。

## C++

```
#include <iostream>
using namespace std;

/* The main function that returns the max possible product */
int maxProd(int n)
{
   // n equals to 2 or 3 must be handled explicitly
   if (n == 2 || n == 3) return (n-1);

   // Keep removing parts of size 3 while n is greater than 4
   int res = 1;
   while (n > 4)
   {
       n -= 3;
       res *= 3; // Keep multiplying 3 to res
   }
   return (n * res); // The last part multiplied by previous parts
}

/* Driver program to test above functions */
int main()
{
    cout << "Maximum Product is " << maxProd(45);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
public class GFG
{
  /* The main function that returns the max possible product */
  static int maxProd(int n)
  {

    // n equals to 2 or 3 must be handled explicitly
    if (n == 2 || n == 3) return (n - 1);

    // Keep removing parts of size 3 while n is greater than 4
    int res = 1;
    while (n > 4)
    {
      n -= 3;
      res *= 3; // Keep multiplying 3 to res
    }
    return (n * res); // The last part multiplied by previous parts
  }

  // Driver code
  public static void main(String[] args) {
    System.out.println("Maximum Product is " + maxProd(45));
  }
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```

''' The main function that returns the max possible product '''
def maxProd(n):

   # n equals to 2 or 3 must be handled explicitly
   if (n == 2 or n == 3):
       return (n - 1);

   # Keep removing parts of size 3 while n is greater than 4
   res = 1;
   while (n > 4):

       n -= 3;
       res *= 3; # Keep multiplying 3 to res

   return (n * res); # The last part multiplied by previous parts

''' Driver program to test above functions '''
if __name__=='__main__':
    print("Maximum Product is", maxProd(45))

    # This code is contributed by rutvik_56.
```

## C#

```
using System;
class GFG {

  /* The main function that returns the max possible product */
  static int maxProd(int n)
  {

    // n equals to 2 or 3 must be handled explicitly
    if (n == 2 || n == 3) return (n - 1);

    // Keep removing parts of size 3 while n is greater than 4
    int res = 1;
    while (n > 4)
    {
      n -= 3;
      res *= 3; // Keep multiplying 3 to res
    }
    return (n * res); // The last part multiplied by previous parts
  }

  // Driver code
  static void Main()
  {
    Console.WriteLine("Maximum Product is " + maxProd(45));
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

    /* The main function that returns the max possible product */
    function maxProd(n)
    {

      // n equals to 2 or 3 must be handled explicitly
      if (n == 2 || n == 3) return (n - 1);

      // Keep removing parts of size 3 while n is greater than 4
      let res = 1;
      while (n > 4)
      {
        n -= 3;
        res *= 3; // Keep multiplying 3 to res
      }
      return (n * res); // The last part multiplied by previous parts
    }

    document.write("Maximum Product is " + maxProd(45));

</script>
```

**Output**

```
Maximum Product is 14348907
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。