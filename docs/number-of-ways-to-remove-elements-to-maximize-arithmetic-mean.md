# 移除元素以最大化算术平均值的方法数量

> 原文:[https://www . geesforgeks . org/移除元素以最大化算术平均值的方式数/](https://www.geeksforgeeks.org/number-of-ways-to-remove-elements-to-maximize-arithmetic-mean/)

给定一个数组 **arr[]** ，任务是找到从数组中移除元素的方法数量，以便最大化剩余数组的算术平均值。
**例:**

> **输入:** arr[] = { 1，2，1，2 }
> **输出:** 3
> 移除索引处的元素:
> { 0，1，2 }
> { 0，2，3 }
> { 0，2 }
> **输入:** arr[] = { 1，2，3 }
> **输出:** 1

**方法:**当**只有最大元素保留在数组中时，数组的算术平均值最大化。**
现在考虑数组 arr[] = { 3，3，3，3 }
我们只需要确保**在移除其他元素后，最大元素的至少一个实例保留在数组中**。这将保证算术平均值的最大化。因此，我们最多需要从上面的数组中移除 3 个元素。移除最多 3 个元素的方式数量:

1.  删除了零个元素。路数= 1。
2.  删除了一个元素。路数= 4。
3.  删除了两个元素。路数= 6。
4.  删除了三个元素。路数= 4。

因此总计= 1+4+6+4 = 15 = 2<sup>4</sup>–1。
现在考虑数组= { 1，4，3，2，3，4，4 }
排序时，数组变成= { 1，2，3，3，4，4，4 }。在这种情况下，除了 4 之外还有其他元素。我们最多可以移除 2 个 4 的实例，当这些实例被移除时，其他元素(不是 4)应该总是被一起移除。因此，路的数量将与最多移除 2 个 4 实例的路的数量相同。
去除元素的各种方式:
{ 1、2、3、3 }
{ 1、2、3、3、4 }
{ 1、2、3、3、4 }
{ 1、2、3、3、4 }
{ 1、2、3、3、4、4 }
{ 1、2、3、3、4、4 }
{ 1、2、3、3、4、4 }
所以答案是

以下是上述办法的实施情况。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>

#define ll long long

using namespace std;
const int mod = 1000000007;

// Function to compute a^n
ll power(ll a, ll n)
{
    if (n == 0)
        return 1;

    ll p = power(a, n / 2) % mod;
    p = (p * p) % mod;
    if (n & 1)
        p = (p * a) % mod;

    return p;
}

// Function to return number of ways to maximize arithmetic mean
ll numberOfWays(int* arr, int n)
{

    int max_count = 0;
    int max_value = *max_element(arr, arr + n);
    for (int i = 0; i < n; i++) {
        if (arr[i] == max_value)
            max_count++;
    }
    return (power(2, max_count) - 1 + mod) % mod;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 1, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << numberOfWays(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.Arrays;

class GFG
{

static int mod = 1000000007;

// Function to compute a^n
static int power(int a, int n)
{
    if (n == 0)
        return 1;

    int p = power(a, n / 2) % mod;
    p = (p * p) % mod;
    if ((n & 1) > 0)
        p = (p * a) % mod;

    return p;
}

// Function to return number of
// ways to maximize arithmetic mean
static int numberOfWays(int []arr, int n)
{

    int max_count = 0;
    int max_value = Arrays.stream(arr).max().getAsInt();
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == max_value)
            max_count++;
    }
    return (power(2, max_count) - 1 + mod) % mod;
}

// Driver code
public static void main (String[] args)
{
    int []arr = { 1, 2, 1, 2 };
    int n = arr.length;
    System.out.println(numberOfWays(arr, n));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

mod = 1000000007;

# Function to compute a^n
def power(a, n) :

    if (n == 0) :
        return 1;

    p = power(a, n // 2) % mod;
    p = (p * p) % mod;
    if (n & 1) :
        p = (p * a) % mod;

    return p;

# Function to return number of ways
# to maximize arithmetic mean
def numberOfWays(arr, n) :

    max_count = 0;
    max_value = max(arr)

    for i in range(n) :
        if (arr[i] == max_value) :
            max_count += 1;

    return (power(2, max_count) - 1 + mod) % mod;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 1, 2 ];
    n = len(arr) ;

    print(numberOfWays(arr, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the above approach
using System;
using System.Linq;

class GFG
{

static int mod = 1000000007;

// Function to compute a^n
static int power(int a, int n)
{
    if (n == 0)
        return 1;

    int p = power(a, n / 2) % mod;
    p = (p * p) % mod;
    if ((n & 1)>0)
        p = (p * a) % mod;

    return p;
}

// Function to return number of
// ways to maximize arithmetic mean
static int numberOfWays(int []arr, int n)
{

    int max_count = 0;
    int max_value = arr.Max();
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == max_value)
            max_count++;
    }
    return (power(2, max_count) - 1 + mod) % mod;
}

// Driver code
static void Main()
{
    int []arr = { 1, 2, 1, 2 };
    int n = arr.Length;
    Console.WriteLine(numberOfWays(arr, n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to compute a^n
function power($x, $y, $p)
{

    // Initialize result
    $res = 1;

    // Update x if it is more
    // than or equal to p
    $x = $x % $p;

    while ($y > 0)
    {
        // If y is odd, multiply
        // x with result
        if ($y & 1)
            $res = ($res * $x) % $p;

        // y must be even now

        // y = $y/2
        $y = $y >> 1;
        $x = ($x * $x) % $p;
    }
    return $res;
}

// Function to return number of ways
// to maximize arithmetic mean
function numberOfWays($arr, $n)
{
    $mod = 1000000007;
    $max_count = 0;
    $max_value = $arr[0];
    for($i = 0; $i < $n; $i++)
    if($max_value < $arr[$i])
        $max_value = $arr[$i];

    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] == $max_value)
            $max_count++;
    }
    return (power(2, $max_count,
                     $mod) - 1 + $mod) % $mod;
}

// Driver code
$arr = array( 1, 2, 1, 2 );
$n = 4;
echo numberOfWays($arr, $n);

// This code is contributed
// by Arnab Kundu
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    let mod = 1000000007;

    // Function to compute a^n
    function power(a, n)
    {
        if (n == 0)
            return 1;

        let p = power(a, parseInt(n / 2, 10)) % mod;
        p = (p * p) % mod;
        if ((n & 1)>0)
            p = (p * a) % mod;

        return p;
    }

    // Function to return number of
    // ways to maximize arithmetic mean
    function numberOfWays(arr, n)
    {

        let max_count = 0;
        let max_value = Number.MIN_VALUE;
        for (let i = 0; i < n; i++)
        {
            max_value = Math.max(max_value, arr[i]);
        }
        for (let i = 0; i < n; i++)
        {
            if (arr[i] == max_value)
                max_count++;
        }
        return (power(2, max_count) - 1 + mod) % mod;
    }

    let arr = [ 1, 2, 1, 2 ];
    let n = arr.length;
    document.write(numberOfWays(arr, n));

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
3
```