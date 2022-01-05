# 第 n 个平方自由数

> 原文:[https://www.geeksforgeeks.org/nth-square-free-number/](https://www.geeksforgeeks.org/nth-square-free-number/)

给定一个数 n，求第 n 个无平方数。如果一个数不能被 1 以外的完美平方整除，它就是无平方数。
**例:**

```
Input : n = 2
Output : 2

Input : 5
Output : 6
There is one number (in range from 1 to 6) 
that is divisible by a square. The number
is 4.
```

**方法 1(蛮力):**
想法是迭代检查每个数是否能被任何完美平方数整除，每当遇到平方自由数时增加计数，并返回第 n 个平方自由数。
执行如下:

## C++

```
// Program to find the nth square free number
#include<bits/stdc++.h>
using namespace std;

// Function to find nth square free number
int squareFree(int n)
{
    // To maintain count of square free number
    int cnt = 0;

    // Loop for square free numbers
    for (int i=1;; i++)
    {
        bool isSqFree = true;
        for (int j=2; j*j<=i; j++)
        {
            // Checking whether square of a number
            // is divisible by any number which is
            // a perfect square
            if (i % (j*j) == 0)
            {
                isSqFree = false;
                break;
            }
        }

        // If number is square free
        if (isSqFree == true)
        {
           cnt++;

           // If the cnt becomes n, return
           // the number
           if (cnt == n)
              return i;
        }
    }
    return 0;
}

// Driver Program
int main()
{
    int n = 10;
    cout << squareFree(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the nth square
// free number
import java.io.*;

class GFG {

    // Function to find nth square free
    // number
    public static int squareFree(int n)
    {

        // To maintain count of square
        // free number
        int cnt = 0;

        // Loop for square free numbers
        for (int i = 1; ; i++) {

            boolean isSqFree = true;

            for (int j = 2; j * j <= i; j++)
            {

                // Checking whether square
                // of a number is divisible
                // by any number which is
                // a perfect square
                if (i % (j * j) == 0) {
                    isSqFree = false;
                    break;
                }
            }

            // If number is square free
            if (isSqFree == true) {
                cnt++;

                // If the cnt becomes n,
                // return the number
                if (cnt == n)
                    return i;
            }
        }
    }

    // driven code
    public static void main(String[] args) {

        int n = 10;

        System.out.println("" + squareFree(n));
    }
}

// This code is contributed by sunnysingh
```

## 蟒蛇 3

```
# Python3 Program to find the nth
# square free number

# Function to find nth square
# free number
def squareFree(n):

    # To maintain count of
    # square free number
    cnt = 0;

    # Loop for square free numbers
    i = 1;
    while (True):
        isSqFree = True;
        j = 2;
        while (j * j <= i):

            # Checking whether square of a number
            # is divisible by any number which is
            # a perfect square
            if (i % (j * j) == 0):
                isSqFree = False;
                break;
            j += 1;

        # If number is square free
        if (isSqFree == True):
            cnt += 1;

            # If the cnt becomes n, return the number
            if (cnt == n):
                return i;
        i += 1;

    return 0;

# Driver Code
n = 10;
print(squareFree(n));

# This code is contributed by mits
```

## C#

```
// C# Program to find the
// nth square free number
using System;

class GFG {

    // Function to find nth
    // square free number
    public static int squareFree(int n)
    {
        // To maintain count of
        // square free number
        int cnt = 0;

        // Loop for square free numbers
        for (int i = 1; ; i++)
        {
            bool isSqFree = true;

            for (int j = 2; j * j <= i; j++)
            {
                // Checking whether square
                // of a number is divisible
                // by any number which is
                // a perfect square
                if (i % (j * j) == 0) {
                    isSqFree = false;
                    break;
                }
            }

            // If number is square free
            if (isSqFree == true) {
                cnt++;

                // If the cnt becomes n,
                // return the number
                if (cnt == n)
                    return i;
            }
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 10;
        Console.Write("" + squareFree(n));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// nth square free number

// Function to find nth
// square free number
function squareFree($n)
{

    // To maintain count of
    // square free number
    $cnt = 0;

    // Loop for square
    // free numbers
    for ($i = 1; ; $i++)
    {
        $isSqFree = true;
        for ($j = 2; $j * $j <= $i; $j++)
        {

            // Checking whether square of a number
            // is divisible by any number which is
            // a perfect square
            if ($i % ($j * $j) == 0)
            {
                $isSqFree = false;
                break;
            }
        }

        // If number is square free
        if ($isSqFree == true)
        {
            $cnt++;

            // If the cnt becomes n,
            // return the number
            if ($cnt == $n)
                return $i;
        }
    }
    return 0;
}

// Driver Code
$n = 10;
echo(squareFree($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to find nth square free
    // number
    function squareFree(n)
    {

        // To maintain count of square
        // free number
        let cnt = 0;

        // Loop for square free numbers
        for (let i = 1; ; i++) {

            let isSqFree = true;

            for (let j = 2; j * j <= i; j++)
            {

                // Checking whether square
                // of a number is divisible
                // by any number which is
                // a perfect square
                if (i % (j * j) == 0) {
                    isSqFree = false;
                    break;
                }
            }

            // If number is square free
            if (isSqFree == true) {
                cnt++;

                // If the cnt becomes n,
                // return the number
                if (cnt == n)
                    return i;
            }
        }
    }

// Driver Code
    let n = 10;
    document.write("" + squareFree(n));

// This code is contributed by susmitakundugoaldanga.
</script>
```

**输出:**

```
14
```

**方法二(更好的方法):**
思路是先统计小于等于上限' k '的平方自由数，然后应用二分搜索法求第 n 个平方自由数。首先，我们计算到“k”的平方数(以平方为因子的数)，然后从总数中减去这个数，得到到“k”的平方自由数。
**说明:**

1.  如果任何整数都有一个完美的平方作为因子，那么保证它也有一个素数的平方作为因子。所以我们需要计算小于或等于 k 的整数，这些整数有素数的平方作为因子。
    例如，找出具有 4 或 9 的整数数作为因子，直到“k”。可以使用[包含-排除原则](https://en.wikipedia.org/wiki/Inclusion%E2%80%93exclusion_principle)来完成。利用[包含-排除原理](https://en.wikipedia.org/wiki/Inclusion%E2%80%93exclusion_principle)，整数总数为[k/4] + [k/9] -[k/36]，其中[]为最大整数函数。
2.  递归应用包含和排除，直到最大整数值变为零。这一步将返回以正方形为因子的数字计数。
3.  应用二分搜索法求第 n 个平方自由数。

以下是上述算法的实现:

## C++

```
// Program to find the nth square free number
#include<bits/stdc++.h>
using namespace std;

// Maximum prime number to be considered for square
// divisibility
const int MAX_PRIME = 100000;

// Maximum value of result. We do binary search from 1
// to MAX_RES
const int MAX_RES = 2000000000l;

void SieveOfEratosthenes(vector<long long> &a)
{
    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    bool prime[MAX_PRIME + 1];
    memset(prime, true, sizeof(prime));

    for (long long p=2; p*p<=MAX_PRIME; p++)
    {
        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p
            for (long long i=p*2; i<=MAX_PRIME; i += p)
                prime[i] = false;
        }
    }

    // Store all prime numbers in a[]
    for (long long p=2; p<=MAX_PRIME; p++)
        if (prime[p])
            a.push_back(p);
}

// Function to count integers upto k which are having
// perfect squares as factors. i is index of next
// prime number whose square needs to be checked.
// curr is current number whos square to be checked.
long long countSquares(long long i, long long cur,
                       long long k, vector<long long> &a)
{
    // variable to store square of prime
    long long square = a[i]*a[i];

    long long newCur = square*cur;

    // If value of greatest integer becomes zero
    if (newCur > k)
        return 0;

    // Applying inclusion-exclusion principle

    // Counting integers with squares as factor
    long long cnt = k/(newCur);

    // Inclusion (Recur for next prime number)
    cnt += countSquares(i+1, cur, k, a);

    // Exclusion (Recur for next prime number)
    cnt -= countSquares(i+1, newCur, k, a);

    // Final count
    return cnt;
}

// Function to return nth square free number
long long squareFree(long long n)
{
    // Computing primes and storing it in an array a[]
    vector <long long> a;
    SieveOfEratosthenes(a);

    // Applying binary search
    long long low = 1;
    long long high = MAX_RES;

    while (low < high)
    {
        long long mid = low + (high - low)/2;

        // 'c' contains Number of square free numbers
        // less than or equal to 'mid'
        long long c = mid - countSquares(0, 1, mid, a);

        // If c < n, then search right side of mid
        // else search left side of mid
        if (c < n)
            low = mid+1;
        else
            high = mid;
    }

    // nth square free number
    return low;
}

// Driver Program
int main()
{
    int n = 10;
    cout << squareFree(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the nth square free number
import java.util.*;

class GFG
{

// Maximum prime number to be considered for square
// divisibility
static int MAX_PRIME = 100000;

// Maximum value of result. We do
// binary search from 1 to MAX_RES
static int MAX_RES = 2000000000;

static void SieveOfEratosthenes(Vector<Long> a)
{
    // Create a boolean array "prime[0..n]"
    // and initialize all entries it as
    // true. A value in prime[i] will
    // finally be false if i is Not
    // a prime, else true.
    boolean prime[] = new boolean[MAX_PRIME + 1];
    Arrays.fill(prime, true);

    for (int p = 2; p * p <= MAX_PRIME; p++)
    {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p
            for (int i = p * 2; i <= MAX_PRIME; i += p)
                prime[i] = false;
        }
    }

    // Store all prime numbers in a[]
    for (int p = 2; p <= MAX_PRIME; p++)
        if (prime[p])
            a.add((long)p);
}

// Function to count integers upto k which are having
// perfect squares as factors. i is index of next
// prime number whose square needs to be checked.
// curr is current number whos square to be checked.
static long countSquares(long i, long cur,
                    long k, Vector<Long> a)
{
    // variable to store square of prime
    long square = a.get((int) i)*a.get((int)(i));

    long newCur = square*cur;

    // If value of greatest integer becomes zero
    if (newCur > k)
        return 0;

    // Applying inclusion-exclusion principle

    // Counting integers with squares as factor
    long cnt = k/(newCur);

    // Inclusion (Recur for next prime number)
    cnt += countSquares(i + 1, cur, k, a);

    // Exclusion (Recur for next prime number)
    cnt -= countSquares(i + 1, newCur, k, a);

    // Final count
    return cnt;
}

// Function to return nth square free number
static long squareFree(long n)
{
    // Computing primes and storing it in an array a[]
    Vector <Long> a = new Vector<>();
    SieveOfEratosthenes(a);

    // Applying binary search
    long low = 1;
    long high = MAX_RES;

    while (low < high)
    {
        long mid = low + (high - low)/2;

        // 'c' contains Number of square free numbers
        // less than or equal to 'mid'
        long c = mid - countSquares(0, 1, mid, a);

        // If c < n, then search right side of mid
        // else search left side of mid
        if (c < n)
            low = mid+1;
        else
            high = mid;
    }

    // nth square free number
    return low;
}

// Driver code
public static void main(String[] args)
{
    int n = 10;
    System.out.println(squareFree(n));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 Program to find the nth square free number
import sys
sys.setrecursionlimit(15000)

# Maximum prime number to be considered for square
# divisibility
MAX_PRIME = 100000;

# Maximum value of result. We do binary search from 1
# to MAX_RES
MAX_RES = 2000000000

def SieveOfEratosthenes(a):

    # Create a boolean array "prime[0..n]" and initialize
    # all entries it as true. A value in prime[i] will
    # finally be false if i is Not a prime, else true.
    prime = [True for i in range(MAX_PRIME + 1)];
    p = 2

    while(p * p <= MAX_PRIME):

        # If prime[p] is not changed, then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, MAX_PRIME + 1, p):           
                prime[i] = False;
        p += 1

    # Store all prime numbers in a[]
    for p in range(2, MAX_PRIME + 1):  
        if (prime[p]):
            a.append(p);   
    return a

# Function to count integers upto k which are having
# perfect squares as factors. i is index of next
# prime number whose square needs to be checked.
# curr is current number whos square to be checked.
def countSquares(i, cur, k, a):

    # variable to store square of prime
    square = a[i]*a[i];
    newCur = square*cur;

    # If value of greatest integer becomes zero
    if (newCur > k):
        return 0, a;

    # Applying inclusion-exclusion principle

    # Counting integers with squares as factor
    cnt = k//(newCur);

    # Inclusion (Recur for next prime number)
    tmp, a = countSquares(i + 1, cur, k, a);

    cnt += tmp

    # Exclusion (Recur for next prime number)
    tmp, a = countSquares(i + 1, newCur, k, a);
    cnt -= tmp

    # Final count
    return cnt,a;

# Function to return nth square free number
def squareFree(n):

    # Computing primes and storing it in an array a[]
    a = SieveOfEratosthenes([]);

    # Applying binary search
    low = 1;
    high = MAX_RES;
    while (low < high): 
        mid = low + (high - low)//2;

        # 'c' contains Number of square free numbers
        # less than or equal to 'mid'
        c,a = countSquares(0, 1, mid, a);
        c = mid - c

        # If c < n, then search right side of mid
        # else search left side of mid
        if (c < n):
            low = mid + 1;
        else:
            high = mid;

    # nth square free number
    return low;

# Driver Program
if __name__=='__main__':

    n = 10;
    print(squareFree(n))

# This code is contributed by rohitsingh07052.
```

## C#

```
// C# Program to find the nth square free number
using System;
using System.Collections.Generic;

class GFG
{

// Maximum prime number to be considered
// for square divisibility
static int MAX_PRIME = 100000;

// Maximum value of result. We do
// binary search from 1 to MAX_RES
static int MAX_RES = 2000000000;

static void SieveOfEratosthenes(List<long> a)
{
    // Create a boolean array "prime[0..n]"
    // and initialize all entries it as
    // true. A value in prime[i] will
    // finally be false if i is Not
    // a prime, else true.
    bool []prime = new bool[MAX_PRIME + 1];
    for(int i = 0; i < MAX_PRIME + 1; i++)
        prime[i] = true;

    for (int p = 2; p * p <= MAX_PRIME; p++)
    {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p
            for (int i = p * 2; i <= MAX_PRIME; i += p)
                prime[i] = false;
        }
    }

    // Store all prime numbers in a[]
    for (int p = 2; p <= MAX_PRIME; p++)
        if (prime[p])
            a.Add((long)p);
}

// Function to count integers upto k which are having
// perfect squares as factors. i is index of next
// prime number whose square needs to be checked.
// curr is current number whos square to be checked.
static long countSquares(long i, long cur,
                    long k, List<long> a)
{
    // variable to store square of prime
    long square = a[(int) i]*a[(int)(i)];

    long newCur = square * cur;

    // If value of greatest integer becomes zero
    if (newCur > k)
        return 0;

    // Applying inclusion-exclusion principle

    // Counting integers with squares as factor
    long cnt = k/(newCur);

    // Inclusion (Recur for next prime number)
    cnt += countSquares(i + 1, cur, k, a);

    // Exclusion (Recur for next prime number)
    cnt -= countSquares(i + 1, newCur, k, a);

    // Final count
    return cnt;
}

// Function to return nth square free number
static long squareFree(long n)
{
    // Computing primes and storing it in an array a[]
    List<long> a = new List<long>();
    SieveOfEratosthenes(a);

    // Applying binary search
    long low = 1;
    long high = MAX_RES;

    while (low < high)
    {
        long mid = low + (high - low)/2;

        // 'c' contains Number of square free numbers
        // less than or equal to 'mid'
        long c = mid - countSquares(0, 1, mid, a);

        // If c < n, then search right side of mid
        // else search left side of mid
        if (c < n)
            low = mid + 1;
        else
            high = mid;
    }

    // nth square free number
    return low;
}

// Driver code
public static void Main()
{
    int n = 10;
    Console.WriteLine(squareFree(n));
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript Program to find the nth square free number

// Maximum prime number to be considered for square
// divisibility
let MAX_PRIME = 100000;

// Maximum value of result. We do
// binary search from 1 to MAX_RES
let MAX_RES = 2000000000;

function SieveOfEratosthenes(a)
{
    // Create a boolean array "prime[0..n]"
    // and initialize all entries it as
    // true. A value in prime[i] will
    // finally be false if i is Not
    // a prime, else true.
    let prime = new Array(MAX_PRIME + 1);
    for(let i=0;i<(MAX_PRIME + 1);i++)
    {
        prime[i]=true;
    }

    for (let p = 2; p * p <= MAX_PRIME; p++)
    {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p
            for (let i = p * 2; i <= MAX_PRIME; i += p)
                prime[i] = false;
        }
    }

    // Store all prime numbers in a[]
    for (let p = 2; p <= MAX_PRIME; p++)
        if (prime[p])
            a.push(p);
}

// Function to count integers upto k which are having
// perfect squares as factors. i is index of next
// prime number whose square needs to be checked.
// curr is current number whos square to be checked.
function countSquares(i,cur,k,a)
{
    // variable to store square of prime
    let square = a[i]*a[i];

    let newCur = square*cur;

    // If value of greatest integer becomes zero
    if (newCur > k)
        return 0;

    // Applying inclusion-exclusion principle

    // Counting integers with squares as factor
    let cnt = Math.floor(k/(newCur));

    // Inclusion (Recur for next prime number)
    cnt += countSquares(i + 1, cur, k, a);

    // Exclusion (Recur for next prime number)
    cnt -= countSquares(i + 1, newCur, k, a);

    // Final count
    return cnt;
}

// Function to return nth square free number
function squareFree(n)
{
    // Computing primes and storing it in an array a[]
    let a = [];
    SieveOfEratosthenes(a);

    // Applying binary search
    let low = 1;
    let high = MAX_RES;

    while (low < high)
    {
        let mid = low + Math.floor((high - low)/2);

        // 'c' contains Number of square free numbers
        // less than or equal to 'mid'
        let c = mid - countSquares(0, 1, mid, a);

        // If c < n, then search right side of mid
        // else search left side of mid
        if (c < n)
            low = mid+1;
        else
            high = mid;
    }

    // nth square free number
    return low;
}

// Driver code
let n = 10;   
document.write(squareFree(n));

// This code is contributed by rag2127

</script>
```

**输出:**

```
14
```

本文由**拉胡尔·阿格沃尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。