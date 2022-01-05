# 小于 N 的数，正好是两个不同质数的乘积

> 原文:[https://www . geesforgeks . org/numbers-小于 n-这是两个不同质数的乘积/](https://www.geeksforgeeks.org/numbers-less-than-n-which-are-product-of-exactly-two-distinct-prime-numbers/)

给定一个数字![N    ](img/1fd8df8dc909b8fac6a91ad5463da0b0.png "Rendered by QuickLaTeX.com")。任务是找出所有小于 N 的这样的数，它们是两个截然不同的质数的乘积。
例如，33 是两个不同素数的乘积，即 11 * 3，而像 60 这样的数字有三个不同的素数因子，即 2 * 2 * 3 * 5。
**注**:这些数字不可能是一个完美的正方形。
**例:**

> **输入** : N = 30
> **输出** : 6、10、14、15、21、22、26
> **输入** : N = 50
> **输出** : 6、10、14、15、21、22、26、33、34、35、38、39、46

**算法** :

1.  遍历到 N，检查每个数字是否正好有两个质因数。
2.  现在为了避免像 49 有两个质数的 7 * 7 乘积的情况，检查这个数是否是一个完美的正方形，以确保它有两个不同的质数。
3.  如果步骤 1 和步骤 2 满足，那么在向量列表中添加数字。
4.  遍历向量并打印其中的所有元素。

以下是上述方法的实现:

## C++

```
// C++ program to find numbers that are product
// of exactly two distinct prime numbers

#include <bits/stdc++.h>
using namespace std;

// Function to check whether a number
// is a PerfectSquare or not
bool isPerfectSquare(long double x)
{

    long double sr = sqrt(x);

    return ((sr - floor(sr)) == 0);
}

// Function to check if a number is a
// product of exactly two distinct primes
bool isProduct(int num)
{
    int cnt = 0;

    for (int i = 2; cnt < 2 && i * i <= num; ++i) {
        while (num % i == 0) {
            num /= i;
            ++cnt;
        }
    }

    if (num > 1)
        ++cnt;

    return cnt == 2;
}

// Function to find numbers that are product
// of exactly two distinct prime numbers.
void findNumbers(int N)
{
    // Vector to store such numbers
    vector<int> vec;

    for (int i = 1; i <= N; i++) {
        if (isProduct(i) && !isPerfectSquare(i)) {

            // insert in the vector
            vec.push_back(i);
        }
    }

    // Print all numbers till n from the vector
    for (int i = 0; i < vec.size(); i++) {
        cout << vec[i] << " ";
    }
}

// Driver function
int main()
{
    int N = 30;

    findNumbers(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find numbers that are product
// of exactly two distinct prime numbers
import java.util.*; 

class GFG{
// Function to check whether a number
// is a PerfectSquare or not
static boolean isPerfectSquare(double x)
{

    double sr = Math.sqrt(x);

    return ((sr - Math.floor(sr)) == 0);
}

// Function to check if a number is a
// product of exactly two distinct primes
static boolean isProduct(int num)
{
    int cnt = 0;

    for (int i = 2; cnt < 2 && i * i <= num; ++i) {
        while (num % i == 0) {
            num /= i;
            ++cnt;
        }
    }

    if (num > 1)
        ++cnt;

    return cnt == 2;
}

// Function to find numbers that are product
// of exactly two distinct prime numbers.
static void findNumbers(int N)
{
    // Vector to store such numbers
    Vector<Integer> vec = new Vector<Integer>();

    for (int i = 1; i <= N; i++) {
        if (isProduct(i) && !isPerfectSquare(i)) {

            // insert in the vector
            vec.add(i);
        }
    }

    // Print all numbers till n from the vector
    Iterator<Integer> itr = vec.iterator(); 
            while(itr.hasNext()){ 
                 System.out.print(itr.next()+" "); 
            } 
}

// Driver function
public static void main(String[] args)
{
    int N = 30;

    findNumbers(N);
}
}
// This Code is Contributed by mits
```

## 蟒蛇 3

```
# Python 3 program to find numbers that are product
# of exactly two distinct prime numbers

import math
# Function to check whether a number
# is a PerfectSquare or not
def isPerfectSquare(x):

    sr = math.sqrt(x)

    return ((sr - math.floor(sr)) == 0)

# Function to check if a number is a
# product of exactly two distinct primes
def isProduct( num):
    cnt = 0

    i = 2
    while cnt < 2 and i * i <= num:
        while (num % i == 0) :
            num //= i
            cnt += 1
        i += 1

    if (num > 1):
        cnt += 1

    return cnt == 2

# Function to find numbers that are product
# of exactly two distinct prime numbers.
def findNumbers(N):
    # Vector to store such numbers
    vec = []

    for i in range(1,N+1) :
        if (isProduct(i) and not isPerfectSquare(i)) :

            # insert in the vector
            vec.append(i)

    # Print all numbers till n from the vector
    for i in range(len( vec)):
        print(vec[i] ,end= " ")

# Driver function
if __name__=="__main__":

    N = 30
    findNumbers(N)
```

## C#

```
// C# program to find numbers that are product
// of exactly two distinct prime numbers
using System;
using System.Collections.Generic;

class GFG
{
    // Function to check whether a number
    // is a PerfectSquare or not
    static bool isPerfectSquare(double x)
    {

        double sr = Math.Sqrt(x);

        return ((sr - Math.Floor(sr)) == 0);
    }

    // Function to check if a number is a
    // product of exactly two distinct primes
    static bool isProduct(int num)
    {
        int cnt = 0;

        for (int i = 2; cnt < 2 && i * i <= num; ++i)
        {
            while (num % i == 0)
            {
                num /= i;
                ++cnt;
            }
        }

        if (num > 1)
            ++cnt;

        return cnt == 2;
    }

    // Function to find numbers that are product
    // of exactly two distinct prime numbers.
    static void findNumbers(int N)
    {
        // Vector to store such numbers
        List<int> vec = new List<int>();

        for (int i = 1; i <= N; i++)
        {
            if (isProduct(i) && !isPerfectSquare(i))
            {

                // insert in the vector
                vec.Add(i);
            }
        }

        // Print all numbers till n from the vector
        foreach(var a in vec)
                    Console.Write(a + " ");
    }

    // Driver code
    public static void Main(String[] args)
    {
        int N = 30;

        findNumbers(N);
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find numbers that are product
// of exactly two distinct prime numbers

// Function to check whether a number
// is a PerfectSquare or not
function isPerfectSquare($x)
{
    $sr = sqrt($x);

    return (($sr - floor($sr)) == 0);
}

// Function to check if a number is a
// product of exactly two distinct primes
function isProduct($num)
{
    $cnt = 0;

    for ($i = 2; $cnt < 2 &&
         $i * $i <= $num; ++$i)
    {
        while ($num % $i == 0)
        {
            $num /= $i;
            ++$cnt;
        }
    }

    if ($num > 1)
        ++$cnt;

    return $cnt == 2;
}

// Function to find numbers that are product
// of exactly two distinct prime numbers.
function findNumbers($N)
{
    // Vector to store such numbers
    $vec = array();

    for ($i = 1; $i <= $N; $i++)
    {
        if (isProduct($i) &&
           !isPerfectSquare($i))
        {

            // insert in the vector
            array_push($vec, $i);
        }
    }

    // Print all numbers till n from the vector
    for ($i = 0; $i < sizeof($vec); $i++)
    {
        echo $vec[$i] . " ";
    }
}

// Driver Code
$N = 30;

findNumbers($N);

// This code is contributed by ita_c
```

## java 描述语言

```
<script>

// Javascript program to find numbers that are product
// of exactly two distinct prime numbers

// Function to check whether a number
// is a PerfectSquare or not
function isPerfectSquare(x)
{
    sr = Math.sqrt(x);
    return ((sr - Math.floor(sr)) == 0);
}

// Function to check if a number is a
// product of exactly two distinct primes
function isProduct(num)
{
    var cnt = 0;

    for(var i = 2; cnt < 2 && (i * i) <= num; ++i)
    {
        while (num % i == 0)
        {
            num = parseInt(num / i);
            ++cnt;
        }
    }

    if (num > 1)
        ++cnt;

    return cnt == 2;
}

// Function to find numbers that are product
// of exactly two distinct prime numbers.
function findNumbers( N)
{
    // Vector to store such numbers
    vec = [];

    for (var i = 1; i <= N; i++)
    {
        if (isProduct(i) && !isPerfectSquare(i))
        {

            // insert in the vector
            vec.push(i);
        }
    }

    // Print all numbers till n from the vector
    for (var i = 0; i < vec.length; i++) {
        document.write(vec[i] + " ");
    }
}

// Driver function
var N = 30;
findNumbers(N);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
6 10 14 15 21 22 26
```

**时间复杂度:** O( ![n    ](img/493367f432400add124059588b6d9677.png "Rendered by QuickLaTeX.com") * ![$\sqrt{n}$    ](img/7061c9821b7fe108a89d1215a08df99c.png "Rendered by QuickLaTeX.com") )
**辅助空间:** O(n)