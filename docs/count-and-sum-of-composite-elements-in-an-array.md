# 数组中复合元素的计数和总和

> 原文:[https://www . geesforgeks . org/数组中复合元素的计数和总和/](https://www.geeksforgeeks.org/count-and-sum-of-composite-elements-in-an-array/)

给定一个正整数数组“arr”，任务是计算数组中[复合数](https://www.geeksforgeeks.org/composite-number/)的个数。
**注:** 1 既不是 *Prime* 也不是 *Composite* 。
**举例:**

> **输入:** arr[] = {1，3，4，5，7}
> **输出:** 1
> 4 是唯一的复合数。
> **输入:** arr[] = {1，2，3，4，5，6，7}
> **输出:** 2

**天真方法:**一个简单的解决方案是遍历数组，对每个元素做素性测试。
**有效方法:**使用厄拉多塞的[筛生成一个布尔](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)达到数组中最大元素的大小，可用于检查一个数是否为素数。另外，将 0 和 1 相加作为质数，这样它们就不会被算作复合数。现在遍历数组，使用生成的布尔向量找到那些复合元素的数量。
以下是上述方法的实施:

## C++

```
// C++ program to count the
// number of composite numbers
// in the given array
#include <bits/stdc++.h>
using namespace std;

// Function that returns the
// the count of composite numbers
int compositeCount(int arr[], int n, int* sum)
{
    // Find maximum value in the array
    int max_val = *max_element(arr, arr + n);

    // Use sieve to find all prime numbers
    // less than or equal to max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    vector<bool> prime(max_val + 1, true);

    // Set 0 and 1 as primes as
    // they don't need to be
    // counted as composite numbers
    prime[0] = true;
    prime[1] = true;
    for (int p = 2; p * p <= max_val; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // Count all composite
    // numbers in the arr[]
    int count = 0;
    for (int i = 0; i < n; i++)
        if (!prime[arr[i]]) {
            count++;
            *sum = *sum + arr[i];
        }

    return count;
}

// Driver code
int main()
{

    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int sum = 0;

    cout << "Count of Composite Numbers = "
          << compositeCount(arr, n, &sum);

    cout << "\nSum of Composite Numbers = " << sum;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

// Java program to count the
// number of composite numbers
// in the given array

class GFG
{

    static int sum = 0;

    // Function that returns the
    // the count of composite numbers
    static int compositeCount(int arr[], int n)
    {
        // Find maximum value in the array
        int max_val = Arrays.stream(arr).max().getAsInt();

        // Use sieve to find all prime numbers
        // less than or equal to max_val
        // Create a boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        Vector<Boolean> prime = new Vector<Boolean>(max_val + 1);
        for (int i = 0; i < max_val + 1; i++)
        {
            prime.add(i, Boolean.TRUE);
        }
        // Set 0 and 1 as primes as
        // they don't need to be
        // counted as composite numbers
        prime.add(0, Boolean.TRUE);
        prime.add(1, Boolean.TRUE);
        for (int p = 2; p * p <= max_val; p++)
        {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime.get(p) == true)
            {

                // Update all multiples of p
                for (int i = p * 2; i <= max_val; i += p)
                {
                    prime.add(i, Boolean.FALSE);
                }
            }
        }

        // Count all composite
        // numbers in the arr[]
        int count = 0;
        for (int i = 0; i < n; i++)
        {
            if (!prime.get(arr[i]))
            {
                count++;
                sum = sum + arr[i];
            }
        }
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {1, 2, 3, 4, 5, 6, 7};
        int n = arr.length;

        System.out.print("Count of Composite Numbers = "
                + compositeCount(arr, n));

        System.out.print("\nSum of Composite Numbers = " + sum);
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to count the
# number of composite numbers
# in the given array

# Function that returns the
# the count of composite numbers
def compositeCount(arr, n):
    Sum = 0

    # Find maximum value in the array
    max_val = max(arr)

    # Use sieve to find all prime numbers
    # less than or equal to max_val
    # Create a boolean array "prime[0..n]".
    # A value in prime[i] will finally be
    # false if i is Not a prime, else True.
    prime = [True for i in range(max_val + 1)]

    # Set 0 and 1 as primes as
    # they don't need to be
    # counted as composite numbers
    prime[0] = True
    prime[1] = True
    for p in range(2, max_val + 1):

        if p * p > max_val:
            break

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, max_val + 1, p):
                prime[i] = False

    # Count all composite numbers
    # in the arr[]
    count = 0
    for i in range(n):
        if (prime[arr[i]] == False):
            count += 1
            Sum = Sum + arr[i]

    return count, Sum

# Driver code
arr = [1, 2, 3, 4, 5, 6, 7 ]
n = len(arr)
count, Sum = compositeCount(arr, n)

print("Count of Composite Numbers = ", count)

print("Sum of Composite Numbers = ", Sum)

// This code is contributed by Mohit Kumar
```

## C#

```
// C# program to count the
// number of composite numbers
// in the given array
using System;
using System.Linq;
using System.Collections;

class GFG
{

static int sum1=0;

// Function that returns the
// the count of composite numbers
static int compositeCount(int []arr, int n, int sum)
{
    // Find maximum value in the array
    int max_val = arr.Max();

    // Use sieve to find all prime numbers
    // less than or equal to max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    bool[] prime=new bool[max_val + 1];

    // Set 0 and 1 as primes as
    // they don't need to be
    // counted as composite numbers
    prime[0] = false;
    prime[1] = false;
    for (int p = 2; p * p <= max_val; p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == false)
        {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime[i] = true;
        }
    }

    // Count all composite
    // numbers in the arr[]
    int count = 0;
    for (int i = 0; i < n; i++)
        if (prime[arr[i]])
        {
            count++;
            sum = sum + arr[i];
        }
    sum1 = sum;
    return count;
}

// Driver code
static void Main()
{

    int []arr = { 1, 2, 3, 4, 5, 6, 7 };
    int n = arr.Length;
    int sum = 0;

    Console.Write("Count of Composite Numbers = "+
                    compositeCount(arr, n, sum));

    Console.Write("\nSum of Composite Numbers = "+sum1);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count the
// number of composite numbers
// in the given array

// Function that returns the
// the count of composite numbers
function compositeCount($arr, $n, &$sum)
{
    // Find maximum value in the array
    $max_val = max($arr);

    // Use sieve to find all prime numbers
    // less than or equal to max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    $prime=array_fill(0,$max_val + 1, true);

    // Set 0 and 1 as primes as
    // they don't need to be
    // counted as composite numbers
    $prime[0] = true;
    $prime[1] = true;
    for ($p = 2; $p * $p <= $max_val; $p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if ($prime[$p] == true)
        {

            // Update all multiples of p
            for ($i = $p * 2; $i <= $max_val; $i += $p)
                $prime[$i] = false;
        }
    }

    // Count all composite
    // numbers in the arr[]
    $count = 0;
    for ($i = 0; $i < $n; $i++)
        if (!$prime[$arr[$i]])
        {
            $count++;
            $sum = $sum + $arr[$i];
        }

    return $count;
}

// Driver code

$arr = array( 1, 2, 3, 4, 5, 6, 7 );
$n = count($arr);
$sum = 0;

echo "Count of Composite Numbers = ".compositeCount($arr, $n, $sum);

echo "\nSum of Composite Numbers = ".$sum;

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to count the
// number of composite numbers
// in the given array

// Function that returns the
// the count of composite numbers

let sum = 0;
function compositeCount(arr, n)
{

    // Find maximum value in the array
    let max_val = arr.sort((a, b) => b - a)[0];

    // Use sieve to find all prime numbers
    // less than or equal to max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    let prime = new Array(max_val + 1).fill(true);

    // Set 0 and 1 as primes as
    // they don't need to be
    // counted as composite numbers
    prime[0] = true;
    prime[1] = true;
    for (let p = 2; p * p <= max_val; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (let i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // Count all composite
    // numbers in the arr[]
    let count = 0;
    for (let i = 0; i < n; i++)
        if (!prime[arr[i]]) {
            count++;
            sum = sum + arr[i];
        }

    return count;
}

// Driver code

let arr = new Array(1, 2, 3, 4, 5, 6, 7);
let n = arr.length;

document.write("Count of Composite Numbers = " + compositeCount(arr, n, sum));

document.write("<br>Sum of Composite Numbers = " + sum);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
Count of Composite Numbers = 2
Sum of Composite Numbers = 10
```

**时间复杂度:** O(n)