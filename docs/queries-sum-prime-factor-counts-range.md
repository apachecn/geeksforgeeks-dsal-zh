# 查询某范围内质因数计数之和

> 原文:[https://www . geesforgeks . org/query-sum-prime-factor-counts-range/](https://www.geeksforgeeks.org/queries-sum-prime-factor-counts-range/)

有 **Q** 查询。每个查询都是 **L** 和 **R** 的形式。任务是在每个查询的给定范围内输出每个数的质因数的和。
**举例:**

```
Input : Q = 2
        L = 6, R = 10
        L = 1, R = 5        
Output : 7 
         4
For query 1,
6 => 2  [Prime factors are 2 and 3]
7 => 1
8 => 1
9 => 1
10 => 2
Sum = 2 + 1 + 1 + 1 + 2 = 7
For query 2,
1 => 0
2 => 1
3 => 1
4 => 1
5 => 1
Sum = 0 + 1 + 1 + 1 + 1 = 4.
```

**方法 1(蛮力):**
思路是对于每个查询从 L 遍历到 R，对于每个数字找到质因数的个数并加入到答案中。
**方法二(高效途径):**
思路是用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)法计算合成数的质因数个数。就像，厄拉多塞筛的内环用来标记复合数。我们可以用它来增加数的质因数。我们可以存储该索引的质数，而不是将每个数组单元标记为 0 或 1。然后对于每个查询，找到从 L 到 r 的数组之和
下面是这个方法的实现:

## C++

```
// C++ program to find sum prime factors
// in given range.
#include <bits/stdc++.h>
#define MAX 1000006
using namespace std;

// using sieve method to evaluating
// the prime factor of numbers
void sieve(int count[])
{
    for (int i = 2; i * i <= MAX; i++) {
        // if i is prime
        if (count[i] == 0) {
            for (int j = 2 * i; j < MAX; j += i)
                count[j]++;

            // setting number of prime
            // factor of a prime number.
            count[i] = 1;
        }
    }
}

// Returns sum of counts of prime factors in
// range from l to r. This function mainly
// uses count[] which is filled by Sieve()
int query(int count[], int l, int r)
{
    int sum = 0;

    // finding the sum of number of prime
    // factor of numbers in a range.
    for (int i = l; i <= r; i++)
        sum += count[i];

    return sum;
}

// Driven Program
int main()
{
    int count[MAX];
    memset(count, 0, sizeof count);
    sieve(count);

    cout << query(count, 6, 10) << endl
         << query(count, 1, 5);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum prime
// factors in given range.

class GFG {

    static final int MAX = 1000006;

    // using sieve method to evaluating
    // the prime factor of numbers
    static void sieve(int count[])
    {
        for (int i = 2; i * i <= MAX; i++) {
            // if i is prime
            if (count[i] == 0) {
                for (int j = 2 * i; j < MAX; j += i)
                    count[j]++;

                // setting number of prime
                // factor of a prime number.
                count[i] = 1;
            }
        }
    }

    // Returns sum of counts of prime factors in
    // range from l to r. This function mainly
    // uses count[] which is filled by Sieve()
    static int query(int count[], int l, int r)
    {
        int sum = 0;

        // finding the sum of number of prime
        // factor of numbers in a range.
        for (int i = l; i <= r; i++)
            sum += count[i];

        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int count[] = new int[MAX];
        sieve(count);

        System.out.println(query(count, 6, 10) + " " + query(count, 1, 5));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find sum prime factors
# in given range.
MAX = 100006;
count = [0] * MAX;

# using sieve method to evaluating
# the prime factor of numbers
def sieve():
    i = 2;
    while (i * i <= MAX):

        # if i is prime
        if (count[i] == 0):
            for j in range(2 * i, MAX, i):
                count[j] += 1;

            # setting number of prime
            # factor of a prime number.
            count[i] = 1;

        i += 1;

# Returns sum of counts of prime factors in
# range from l to r. This function mainly
# uses count[] which is filled by Sieve()
def query(l, r):
    sum = 0;

    # finding the sum of number of prime
    # factor of numbers in a range.
    for i in range(l, r + 1):
        sum += count[i];

    return sum;

# Driver Code
sieve();
print(query(6, 10), query(1, 5));

# This code is contributed by mits
```

## C#

```
// C# program to find sum prime
// factors in given range.
using System;

class GFG {

    static int MAX = 1000006;

    // using sieve method to evaluating
    // the prime factor of numbers
    static void sieve(int[] count)
    {
        for (int i = 2; i * i <= MAX; i++)
        {

            // if i is prime
            if (count[i] == 0) {
                for (int j = 2 * i; j < MAX;
                                     j += i)
                    count[j]++;

                // setting number of prime
                // factor of a prime number.
                count[i] = 1;
            }
        }
    }

    // Returns sum of counts of prime factors
    // in range from l to r. This function
    // mainly uses count[] which is filled by
    // Sieve()
    static int query(int[] count, int l, int r)
    {

        int sum = 0;

        // finding the sum of number of prime
        // factor of numbers in a range.
        for (int i = l; i <= r; i++)
            sum += count[i];

        return sum;
    }

    // Driver code
    public static void Main()
    {

        int[] count = new int[MAX];
        sieve(count);

        Console.Write(query(count, 6, 10) +
                " " + query(count, 1, 5));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum prime factors
// in given range.
$MAX = 100006;

// using sieve method to evaluating
// the prime factor of numbers
function sieve(&$count)
{
    global $MAX;
    for ($i = 2; $i * $i <= $MAX; $i++)
    {
        // if i is prime
        if ($count[$i] == 0)
        {
            for ($j = 2 * $i; $j < $MAX; $j += $i)
                $count[$j]++;

            // setting number of prime
            // factor of a prime number.
            $count[$i] = 1;
        }
    }
}

// Returns sum of counts of prime factors in
// range from l to r. This function mainly
// uses count[] which is filled by Sieve()
function query($count, $l, $r)
{
    $sum = 0;

    // finding the sum of number of prime
    // factor of numbers in a range.
    for ($i = $l; $i <= $r; $i++)
        $sum += $count[$i];

    return $sum;
}

// Driver Code
$count = array_fill(0, $MAX, 0);
sieve($count);

echo query($count, 6, 10) . " " .
     query($count, 1, 5);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum prime
// factors in given range.
var MAX = 1000006;

    // using sieve method to evaluating
// the prime factor of numbers
function sieve(count)
{
    for (i = 2; i * i <= MAX; i++) {
        // if i is prime
        if (count[i] == 0) {
            for (j = 2 * i; j < MAX; j += i)
                count[j]++;

            // setting number of prime
            // factor of a prime number.
            count[i] = 1;
        }
    }
}

// Returns sum of counts of prime factors in
// range from l to r. This function mainly
// uses count which is filled by Sieve()
function query(count , l , r)
{
    var sum = 0;

    // finding the sum of number of prime
    // factor of numbers in a range.
    for (i = l; i <= r; i++)
        sum += count[i];

    return sum;
}

// Driver code
var count = Array.from({length: MAX},
(_, i) => 0);
sieve(count);

document.write(query(count, 6, 10) + " " +
query(count, 1, 5));

// This code contributed by shikhasingrajput

</script>
```

**输出:**

```
7 4
```

本文由 **Anuj chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。