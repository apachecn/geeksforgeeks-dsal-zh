# 计数偶数和奇数乘积的有序对的数量

> 原文:[https://www . geesforgeks . org/count-带偶数和奇数乘积的有序对数/](https://www.geeksforgeeks.org/count-number-of-ordered-pairs-with-even-and-odd-product/)

给定一个 n 个正数的数组，任务是计算具有偶数和奇数乘积的有序对的数量。有序对意味着(a，b)和(b，a)将被认为是不同的。
**例:**

> **输入:** n = 3，arr[] = {1，2，7}
> **输出:**偶积对= 4，奇积对= 2
> 有序对是(1，2)，(1，7)，(2，1)，(7，1)，(2，7)，(7，2)
> 偶积对:(1，7)，(7，1)
> 偶积对:(1，2)，(2，7)，(2，1)，(7，2)
> **输入:**

**方法:**
两个数的乘积只有都是奇数时才是奇数。因此:

> **奇数乘积对的数量=(奇数计数)*(奇数计数–1)**

偶数乘积对的数量将是奇数乘积对的数量的倒数。因此:

> **偶数产品对的数量=对的总数–奇数产品对的数量**

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// function to count odd product pair
int count_odd_pair(int n, int a[])
{
    int odd = 0, even = 0;

    for (int i = 0; i < n; i++) {

        // if number is even
        if (a[i] % 2 == 0)
            even++;

        // if number is odd
        else
            odd++;
    }

    // count of ordered pairs
    int ans = odd * (odd - 1);

    return ans;
}

// function to count even product pair
int count_even_pair(int odd_product_pairs, int n)
{
    int total_pairs = (n * (n - 1));
    int ans = total_pairs - odd_product_pairs;
    return ans ;
}

// Driver code
int main()
{

    int n = 6;
    int a[] = { 2, 4, 5, 9, 1, 8 };

    int odd_product_pairs = count_odd_pair(n, a);

    int even_product_pairs = count_even_pair(
        odd_product_pairs, n);

    cout << "Even Product Pairs = "
         << even_product_pairs
         << endl;
    cout << "Odd Product Pairs= "
         << odd_product_pairs
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  implementation of the above approach
import java.io.*;

class GFG {

// function to count odd product pair
static int count_odd_pair(int n, int a[])
{
    int odd = 0, even = 0;

    for (int i = 0; i < n; i++) {

        // if number is even
        if (a[i] % 2 == 0)
            even++;

        // if number is odd
        else
            odd++;
    }

    // count of ordered pairs
    int ans = odd * (odd - 1);

    return ans;
}

// function to count even product pair
static int count_even_pair(int odd_product_pairs, int n)
{
    int total_pairs = (n * (n - 1));
    int ans = total_pairs - odd_product_pairs;
    return ans;
}

// Driver code
    public static void main (String[] args) {

        int n = 6;
        int []a = { 2, 4, 5, 9, 1, 8 };

        int odd_product_pairs = count_odd_pair(n, a);

        int even_product_pairs = count_even_pair(
            odd_product_pairs, n);

        System.out.println( "Even Product Pairs = "+
            even_product_pairs );

        System.out.println("Odd Product Pairs= "+
             odd_product_pairs );

    }
}
//This Code is Contributed by ajit
```

## 蟒蛇 3

```
# Python3 implementation of
# above approach

# function to count odd product pair
def count_odd_pair(n, a):
    odd = 0
    even = 0
    for i in range(0,n):

        # if number is even
        if a[i] % 2==0:
            even=even+1
        # if number is odd
        else:
            odd=odd+1

    # count of ordered pairs
    ans = odd * (odd - 1)
    return ans

# function to count even product pair
def count_even_pair(odd_product_pairs, n):
    total_pairs = (n * (n - 1))
    ans = total_pairs - odd_product_pairs
    return ans

#Driver code
if __name__=='__main__':
    n = 6
    a = [2, 4, 5, 9, 1 ,8]

    odd_product_pairs = count_odd_pair(n, a)
    even_product_pairs = (count_even_pair
                       (odd_product_pairs, n))

    print("Even Product Pairs = "
          ,even_product_pairs)
    print("Odd Product Pairs= "
          ,odd_product_pairs)

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C#  implementation of the above approach
using System;

public class GFG{

// function to count odd product pair
static int count_odd_pair(int n, int []a)
{
    int odd = 0, even = 0;

    for (int i = 0; i < n; i++) {

        // if number is even
        if (a[i] % 2 == 0)
            even++;

        // if number is odd
        else
            odd++;
    }

    // count of ordered pairs
    int ans = odd * (odd - 1);

    return ans;
}

// function to count even product pair
static int count_even_pair(int odd_product_pairs, int n)
{
    int total_pairs = (n * (n - 1));
    int ans = total_pairs - odd_product_pairs;
    return ans;
}

// Driver code

static public void Main (){
        int n = 6;
        int []a = { 2, 4, 5, 9, 1, 8 };

        int odd_product_pairs = count_odd_pair(n, a);

        int even_product_pairs = count_even_pair(
            odd_product_pairs, n);

        Console.WriteLine( "Even Product Pairs = "+
            even_product_pairs );

        Console.WriteLine("Odd Product Pairs= "+
            odd_product_pairs );
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// function to count odd product pair
function count_odd_pair($n, $a)
{
    $odd = 0 ;
    $even = 0 ;

    for ($i = 0; $i < $n; $i++)
    {

        // if number is even
        if ($a[$i] % 2 == 0)
            $even++;

        // if number is odd
        else
            $odd++;
    }

    // count of ordered pairs
    $ans = $odd * ($odd - 1);

    return $ans;
}

// function to count even product pair
function count_even_pair($odd_product_pairs, $n)
{
    $total_pairs = ($n * ($n - 1));
    $ans = $total_pairs - $odd_product_pairs;

    return $ans ;
}

// Driver code
$n = 6;
$a = array( 2, 4, 5, 9, 1, 8 );

$odd_product_pairs = count_odd_pair($n, $a);

$even_product_pairs =
      count_even_pair($odd_product_pairs, $n);

echo "Even Product Pairs = ",
      $even_product_pairs, "\n";
echo "Odd Product Pairs = ",
      $odd_product_pairs, "\n";

// This code is contributed
// by ANKITRAI1
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// function to count odd product pair
function count_odd_pair(n, a)
{
    let odd = 0, even = 0;

    for (let i = 0; i < n; i++) {

        // if number is even
        if (a[i] % 2 == 0)
            even++;

        // if number is odd
        else
            odd++;
    }

    // count of ordered pairs
    let ans = odd * (odd - 1);

    return ans;
}

// function to count even product pair
function count_even_pair(odd_product_pairs, n)
{
    let total_pairs = (n * (n - 1));
    let ans = total_pairs - odd_product_pairs;
    return ans ;
}

// Driver code
    let n = 6;
    let a = [ 2, 4, 5, 9, 1, 8 ];

    let odd_product_pairs = count_odd_pair(n, a);

    let even_product_pairs = count_even_pair(
        odd_product_pairs, n);

    document.write("Even Product Pairs = "
        + even_product_pairs
        + "<br>");
    document.write("Odd Product Pairs= "
        + odd_product_pairs
        + "<br>");

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
Even Product Pairs = 24
Odd Product Pairs= 6
```