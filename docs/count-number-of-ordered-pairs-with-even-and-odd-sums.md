# 计算奇数和偶数的有序对的数量

> 原文:[https://www . geeksforgeeks . org/count-带奇偶和的有序对数/](https://www.geeksforgeeks.org/count-number-of-ordered-pairs-with-even-and-odd-sums/)

给定一个 n 个正数的数组，任务是计算奇数和偶数的有序对的数量。
**例:**

> **输入:** arr[] = {1，2，4}
> **输出:**偶和对= 2，奇和对= 4
> 有序对是(1，2)，(1，4)，(2，1)，(4，1)，(2，4)，(4，2)
> 偶和对:(2，4)，(4，2)
> 奇和对:(1，2)，(1，4)，(2，1)，(4，1)
> **输入:** arr[]

**方法:**
如果一个数是奇数，另一个数是偶数，那么两个数之和就是奇数。所以现在我们要数偶数和奇数。由于顺序对(a，b)和(b，a)都被视为不同的对，因此

> **奇数对和数=(偶数计数)*(奇数计数)* 2**

这是因为每个偶数可以和每个奇数配对，每个奇数可以和每个偶数配对。这样，在答案中乘 2 就完成了。
偶数和对的数量将是奇数和对的数量的倒数。因此:

> **偶和对的数量=对的总数–奇和对的数量**

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// function to count odd sum pair
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
    int ans = odd * even * 2;

    return ans;
}

// function to count even sum pair
int count_even_pair(int odd_sum_pairs, int n)
{
    int total_pairs = (n * (n - 1));
    int ans = total_pairs - odd_sum_pairs;

    return ans;
}

// Driver code
int main()
{

    int n = 6;
    int a[] = { 2, 4, 5, 9, 1, 8 };

    int odd_sum_pairs = count_odd_pair(n, a);

    int even_sum_pairs = count_even_pair(
        odd_sum_pairs, n);

    cout << "Even Sum Pairs = "
         << even_sum_pairs
         << endl;
    cout << "Odd Sum Pairs= "
         << odd_sum_pairs
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
{
    // function to count odd sum pair
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
        int ans = odd * even * 2;

        return ans;
    }

    // function to count even sum pair
    static int count_even_pair(int odd_sum_pairs, int n)
    {
        int total_pairs = (n * (n - 1));
        int ans = total_pairs - odd_sum_pairs;

        return ans;
    }

    // Driver code
    public static void main(String []args)
    {

        int n = 6;
        int []a = { 2, 4, 5, 9, 1, 8 };

        int odd_sum_pairs = count_odd_pair(n, a);

        int even_sum_pairs = count_even_pair( odd_sum_pairs, n);

        System.out.println("Even Sum Pairs = " + even_sum_pairs);

        System.out.println("Odd Sum Pairs= " + odd_sum_pairs);

    }

}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Pytho3 implementation of the above approach

# function to count odd sum pair
def count_odd_pair( n,  a):

    odd = 0
    even = 0

    for i in range(0,n):

        # if number is even
        if ( a[ i] % 2 == 0):
             even=even+1

        # if number is odd
        else:
             odd=odd+1

    # count of ordered pairs
    ans =  odd *  even * 2

    return  ans

# function to count even sum pair
def count_even_pair( odd_sum_pairs,  n):

    total_pairs = ( n * ( n - 1))
    ans =  total_pairs -  odd_sum_pairs
    return ans

# Driver code

n = 6
a = [2, 4, 5, 9, 1, 8]

odd_sum_pairs = count_odd_pair( n,  a)

even_sum_pairs = count_even_pair( odd_sum_pairs,  n)

print("Even Sum Pairs =", even_sum_pairs)
print("Odd Sum Pairs=", odd_sum_pairs)

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the above approach

using System;
class GFG
{
    // function to count odd sum pair
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
        int ans = odd * even * 2;

        return ans;
    }

    // function to count even sum pair
    static int count_even_pair(int odd_sum_pairs, int n)
    {
        int total_pairs = (n * (n - 1));
        int ans = total_pairs - odd_sum_pairs;

        return ans;
    }

    // Driver code
    public static void Main()
    {

        int n = 6;
        int []a = { 2, 4, 5, 9, 1, 8 };

        int odd_sum_pairs = count_odd_pair(n, a);

        int even_sum_pairs = count_even_pair( odd_sum_pairs, n);

        Console.WriteLine("Even Sum Pairs = " + even_sum_pairs);

        Console.WriteLine("Odd Sum Pairs= " + odd_sum_pairs);

    }

}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// function to count odd sum pair
function count_odd_pair($n, $a)
{
    $odd = 0;
    $even = 0;

    for ($i = 0; $i < $n; $i++) {

        // if number is even
        if ($a[$i] % 2 == 0)
            $even++;

        // if number is odd
        else
            $odd++;
    }

    // count of ordered pairs
    $ans = $odd * $even * 2;

    return $ans;
}

// function to count even sum pair
function count_even_pair($odd_sum_pairs, $n)
{
    $total_pairs = ($n * ($n - 1));
    $ans = $total_pairs - $odd_sum_pairs;
    return $ans;
}

// Driver code

$n = 6;
$a = array( 2, 4, 5, 9, 1, 8 );

$odd_sum_pairs = count_odd_pair($n, $a);

$even_sum_pairs = count_even_pair($odd_sum_pairs, $n);

echo "Even Sum Pairs = $even_sum_pairs \n";
echo "Odd Sum Pairs=  $odd_sum_pairs \n";

// This code is contributed by ihritik   
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// function to count odd sum pair
function count_odd_pair(n, a)
{
    var odd = 0, even = 0;

    for (var i = 0; i < n; i++) {

        // if number is even
        if (a[i] % 2 == 0)
            even++;

        // if number is odd
        else
            odd++;
    }

    // count of ordered pairs
    var ans = odd * even * 2;

    return ans;
}

// function to count even sum pair
function count_even_pair(odd_sum_pairs, n)
{
    var total_pairs = (n * (n - 1));
    var ans = total_pairs - odd_sum_pairs;

    return ans;
}

// Driver code
var n = 6;
var a = [2, 4, 5, 9, 1, 8];
var odd_sum_pairs = count_odd_pair(n, a);
var even_sum_pairs = count_even_pair(
    odd_sum_pairs, n);

document.write( "Even Sum Pairs = "
     + even_sum_pairs + "<br>");

document.write( "Odd Sum Pairs = "
     + odd_sum_pairs + "<br>");

</script>
```

**Output:** 

```
Even Sum Pairs = 12
Odd Sum Pairs= 18
```