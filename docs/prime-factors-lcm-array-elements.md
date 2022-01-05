# 阵元 LCM 的素因子

> 原文:[https://www . geesforgeks . org/prime-factors-LCM-array-elements/](https://www.geeksforgeeks.org/prime-factors-lcm-array-elements/)

给定一个数组 arr[,使得 1 <= arr[i] <= 10^12，任务是找到数组元素 LCM 的素因子。

**示例:**

```
Input  : arr[] = {1, 2, 3, 4, 5, 6, 7, 8}
Output : 2 3 5 7
// LCM of n elements is 840 and 840 = 2*2*2*3*5*7 
// so prime factors would be 2, 3, 5, 7

Input  : arr[] = {20, 10, 15, 60}
Output : 2 3 5
// LCM of n elements is 60 and 60 = 2*2*3*5,
// so prime factors would be 2,3,5
```

这个问题的一个**简单解法**就是求数组中 n 个元素的 LCM。首先初始化 lcm = 1，然后对数组中的每个元素进行迭代，使用公式 **lcm(a，b) = (a * b) / gcd(a，b)** 即 lcm = (lcm * arr[i]) / gcd(lcm，arr[i])，用新元素找到之前结果的 LCM。找到所有 n 个元素的 LCM 后，我们可以计算出 LCM 的[所有质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。
由于这里的约束很大，我们无法实现上述方法来解决这个问题，因为在计算 LCM(a，b)时，我们需要计算 a*b，如果 a，b 都是 10^12 值，那么它将超过整数大小的限制。我们用另一种方法来处理这个问题，使用 sundaram 的[筛](https://www.geeksforgeeks.org/sieve-sundaram-print-primes-smaller-n/)和一个数的**素因子分解**。我们知道，如果 LCM(a，b) = k，那么 a 或 b 的任何质因数也将是‘k’的质因数。

*   取一个大小为 10^6 的数组因子[]并用 0 初始化它，因为任何数的质因数总是小于等于它的平方根，在我们的约束 arr[i] <= 10^12.中
*   生成所有小于等于 10^6 的素数，并将它们存储在另一个数组中。
*   现在逐一计算数组中每个数的所有质因数，并在 factor[]数组中标记为 1。
*   现在遍历 factor[]数组并打印所有标记为 1 的索引，因为这些索引是给定数组中 n 个数的 lcm 的质因数。

以下是上述想法的实现。

## C++

```
// C++ program to find prime factors of LCM of array elements
#include <bits/stdc++.h>
using namespace std;

const int MAX  = 1000000;
typedef long long int ll;

// array to store all prime less than and equal to 10^6
vector <int> primes;

// utility function for sieve of sundaram
void sieve()
{
    int n = MAX;

    // In general Sieve of Sundaram, produces primes smaller
    // than (2*x + 2) for a number given number x. Since
    // we want primes smaller than n, we reduce n to half
    int nNew = (n)/2;

    // This array is used to separate numbers of the form
    // i+j+2ij from others where 1 <= i <= j
    bool marked[nNew + 100];

    // Initialize all elements as not marked
    memset(marked, false, sizeof(marked));

    // Main logic of Sundaram. Mark all numbers which do not
    // generate prime number by doing 2*i+1
    int tmp=sqrt(n);
    for (int i=1; i<=(tmp-1)/2; i++)
        for (int j=(i*(i+1))<<1; j<=nNew; j=j+2*i+1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.push_back(2);

    // Print other primes. Remaining primes are of the form
    // 2*i + 1 such that marked[i] is false.
    for (int i=1; i<=nNew; i++)
        if (marked[i] == false)
            primes.push_back(2*i + 1);
}

// Function to find prime factors of n elements of
// given array
void primeLcm(ll arr[], int n )
{
    // factors[] --> array to mark all prime factors of
    // lcm of array elements
    int factors[MAX] = {0};

    // One by one calculate prime factors of number
    // and mark them in factors[] array
    for (int i=0; i<n; i++)
    {
        // copy --> duplicate of original element to
        //          perform operation
        ll copy = arr[i];

        // sqr --> square root of current number 'copy'
        // because all prime factors are always less
        // than and equal to square root of given number
        int sqr = sqrt(copy);

        // check divisibility with prime factor
        for (int j=0; primes[j]<=sqr; j++)
        {
            // if current prime number is factor of 'copy'
            if (copy%primes[j] == 0)
            {
                // divide with current prime factor until
                // it can divide the number
                while (copy%primes[j] == 0)
                    copy = copy/primes[j];

                // mark current prime factor as 1 in
                // factors[] array
                factors[primes[j]] = 1;
            }
        }

        // After calculating exponents of all prime factors
        // either value of 'copy' will be 1 because of
        // complete divisibility or remaining value of
        // 'copy' will be surely a prime , so we will
        // also mark this prime as a factor
        if (copy > 1)
            factors[copy] = 1;
    }

    // if 2 is prime factor of lcm of all elements
    // in given array
    if (factors[2] == 1)
        cout << 2 << " ";

    // traverse to print all prime factors of lcm of
    // all elements in given array
    for (int i=3; i<=MAX; i=i+2)
        if (factors[i] == 1)
            cout << i << " ";
}

// Driver program to run the case
int main()
{
    sieve();
    ll arr[] = {20, 10, 15, 60};
    int n = sizeof(arr)/sizeof(arr[0]);
    primeLcm(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find prime
// factors of LCM of array elements
import java.util.*;

class GFG
{

static int MAX = 1000000;

// array to store all prime less
// than and equal to 10^6
static ArrayList<Integer> primes = new ArrayList<Integer>();

// utility function for sieve of sundaram
static void sieve()
{
    int n = MAX;

    // In general Sieve of Sundaram,
    // produces primes smaller than
    // (2*x + 2) for a number given
    // number x. Since we want primes
    // smaller than n, we reduce n to half
    int nNew = (n) / 2;

    // This array is used to separate
    // numbers of the form i+j+2ij
    // from others where 1 <= i <= j
    boolean[] marked = new boolean[nNew + 100];

    // Main logic of Sundaram. Mark all
    // numbers which do not generate
    // prime number by doing 2*i+1
    int tmp = (int)Math.sqrt(n);
    for (int i = 1; i <= (tmp - 1) / 2; i++)
        for (int j = (i * (i + 1)) << 1;
                j <= nNew; j = j + 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.add(2);

    // Print other primes. Remaining
    // primes are of the form 2*i + 1
    // such that marked[i] is false.
    for (int i = 1; i <= nNew; i++)
        if (marked[i] == false)
            primes.add(2 * i + 1);
}

// Function to find prime factors
// of n elements of given array
static void primeLcm(int[] arr, int n )
{
    // factors[] --> array to mark all prime
    // factors of lcm of array elements
    int[] factors = new int[MAX];

    // One by one calculate prime factors of number
    // and mark them in factors[] array
    for (int i = 0; i < n; i++)
    {
        // copy --> duplicate of original element to
        //  perform operation
        int copy = arr[i];

        // sqr --> square root of current number 'copy'
        // because all prime factors are always less
        // than and equal to square root of given number
        int sqr = (int)Math.sqrt(copy);

        // check divisibility with prime factor
        for (int j = 0; primes.get(j) <= sqr; j++)
        {
            // if current prime number is factor of 'copy'
            if (copy % primes.get(j) == 0)
            {
                // divide with current prime factor until
                // it can divide the number
                while (copy % primes.get(j) == 0)
                    copy = copy / primes.get(j);

                // mark current prime factor as 1 in
                // factors[] array
                factors[primes.get(j)] = 1;
            }
        }

        // After calculating exponents of all prime factors
        // either value of 'copy' will be 1 because of
        // complete divisibility or remaining value of
        // 'copy' will be surely a prime , so we will
        // also mark this prime as a factor
        if (copy > 1)
            factors[copy] = 1;
    }

    // if 2 is prime factor of lcm of all elements
    // in given array
    if (factors[2] == 1)
        System.out.print("2 ");

    // traverse to print all prime factors of lcm of
    // all elements in given array
    for (int i = 3; i <= MAX; i = i + 2)
        if (factors[i] == 1)
            System.out.print(i+" ");
}

// Driver code
public static void main (String[] args)
{
    sieve();
    int[] arr = {20, 10, 15, 60};
    int n = arr.length;
    primeLcm(arr, n);
}
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 program to find prime factors
# of LCM of array elements
import math;
MAX = 10000;

# array to store all prime less than
# and equal to 10^6
primes = [];

# utility function for sieve of sundaram
def sieve():

    n = MAX;

    # In general Sieve of Sundaram, produces
    # primes smaller than (2*x + 2) for a
    # number given number x. Since we want
    # primes smaller than n, we reduce n to half
    nNew = int(n / 2);

    # This array is used to separate numbers of
    # the form i+j+2ij from others where 1 <= i <= j
    marked = [False] * (nNew + 100);

    # Main logic of Sundaram. Mark all numbers
    # which do not generate prime number by
    # doing 2*i+1
    tmp = int(math.sqrt(n));
    for i in range(1, int((tmp - 1) / 2) + 1):
        for j in range((i * (i + 1)) << 1,
                        nNew + 1, 2 * i + 1):
            marked[j] = True;

    # Since 2 is a prime number
    primes.append(2);

    # Print other primes. Remaining primes
    # are of the form 2*i + 1 such that
    # marked[i] is false.
    for i in range(1, nNew + 1):
        if (marked[i] == False):
            primes.append(2 * i + 1);

# Function to find prime factors of
# n elements of given array
def primeLcm(arr, n ):

    # factors[] --> array to mark all prime
    # factors of lcm of array elements
    factors = [0] * (MAX);

    # One by one calculate prime factors of
    # number and mark them in factors[] array
    for i in range(n):

        # copy --> duplicate of original
        # element to perform operation
        copy = arr[i];

        # sqr --> square root of current number
        # 'copy' because all prime factors are
        # always less than and equal to square
        # root of given number
        sqr = int(math.sqrt(copy));

        # check divisibility with prime factor
        j = 0;
        while (primes[j] <= sqr):

            # if current prime number is
            # factor of 'copy'
            if (copy % primes[j] == 0):

                # divide with current prime factor
                # until it can divide the number
                while (copy % primes[j] == 0):
                    copy = int(copy / primes[j]);

                # mark current prime factor as 1
                # in factors[] array
                factors[primes[j]] = 1;
            j += 1;

        # After calculating exponents of all prime
        # factors either value of 'copy' will be 1
        # because of complete divisibility or
        # remaining value of 'copy' will be surely
        # a prime, so we will also mark this prime
        # as a factor
        if (copy > 1):
            factors[copy] = 1;

    # if 2 is prime factor of lcm of
    # all elements in given array
    if (factors[2] == 1):
        print("2 ", end = "");

    # traverse to print all prime factors of
    # lcm of all elements in given array
    for i in range(3, MAX + 1, 2):
        if (factors[i] == 1):
            print(i, end = " ");

# Driver Code
sieve();
arr = [20, 10, 15, 60];
n = len(arr);
primeLcm(arr, n);

# This code is contributed by chandan_jnu
```

## C#

```
// C# program to find prime
// factors of LCM of array elements
using System;
using System.Collections;

class GFG
{

static int MAX = 1000000;

// array to store all prime less
// than and equal to 10^6
static ArrayList primes = new ArrayList();

// utility function for sieve of sundaram
static void sieve()
{
    int n = MAX;

    // In general Sieve of Sundaram,
    // produces primes smaller than
    // (2*x + 2) for a number given
    // number x. Since we want primes
    // smaller than n, we reduce n to half
    int nNew = (n) / 2;

    // This array is used to separate
    // numbers of the form i+j+2ij
    // from others where 1 <= i <= j
    bool[] marked = new bool[nNew + 100];

    // Main logic of Sundaram. Mark all
    // numbers which do not generate
    // prime number by doing 2*i+1
    int tmp = (int)Math.Sqrt(n);
    for (int i = 1; i <= (tmp - 1) / 2; i++)
        for (int j = (i * (i + 1)) << 1;
                j <= nNew; j = j + 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.Add(2);

    // Print other primes. Remaining
    // primes are of the form 2*i + 1
    // such that marked[i] is false.
    for (int i = 1; i <= nNew; i++)
        if (marked[i] == false)
            primes.Add(2 * i + 1);
}

// Function to find prime factors
// of n elements of given array
static void primeLcm(int[] arr, int n )
{
    // factors[] --> array to
    // mark all prime factors
    // of lcm of array elements
    int[] factors = new int[MAX];

    // One by one calculate prime
    // factors of number and mark
    // them in factors[] array
    for (int i = 0; i < n; i++)
    {
        // copy --> duplicate of original
        // element to perform operation
        int copy = arr[i];

        // sqr --> square root of current
        // number 'copy' because all prime
        // factors are always less than and
        // equal to square root of given number
        int sqr = (int)Math.Sqrt(copy);

        // check divisibility with prime factor
        for (int j = 0; (int)primes[j] <= sqr; j++)
        {
            // if current prime number is factor of 'copy'
            if (copy % (int)primes[j] == 0)
            {
                // divide with current prime factor until
                // it can divide the number
                while (copy % (int)primes[j] == 0)
                    copy = copy / (int)primes[j];

                // mark current prime factor as 1 in
                // factors[] array
                factors[(int)primes[j]] = 1;
            }
        }

        // After calculating exponents of all prime factors
        // either value of 'copy' will be 1 because of
        // complete divisibility or remaining value of
        // 'copy' will be surely a prime , so we will
        // also mark this prime as a factor
        if (copy > 1)
            factors[copy] = 1;
    }

    // if 2 is prime factor of lcm of all elements
    // in given array
    if (factors[2] == 1)
        Console.Write("2 ");

    // traverse to print all prime factors of lcm of
    // all elements in given array
    for (int i = 3; i <= MAX; i = i + 2)
        if (factors[i] == 1)
            Console.Write(i+" ");
}

// Driver code
static void Main()
{
    sieve();
    int[] arr = {20, 10, 15, 60};
    int n = arr.Length;
    primeLcm(arr, n);
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find prime factors of
// LCM of array elements

$MAX = 10000;

// array to store all prime less than
// and equal to 10^6
$primes = array();

// utility function for sieve of sundaram
function sieve()
{
    global $MAX, $primes;
    $n = $MAX;

    // In general Sieve of Sundaram, produces
    // primes smaller than (2*x + 2) for a number
    // given number x. Since we want primes smaller
    // than n, we reduce n to half
    $nNew = (int)($n / 2);

    // This array is used to separate numbers of
    // the form i+j+2ij from others where 1 <= i <= j
    $marked = array_fill(0, $nNew + 100, false);

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    $tmp = (int)sqrt($n);
    for ($i = 1; $i <= (int)(($tmp - 1) / 2); $i++)
        for ($j = ($i * ($i + 1)) << 1;
             $j <= $nNew; $j = $j + 2 * $i + 1)
            $marked[$j] = true;

    // Since 2 is a prime number
    array_push($primes, 2);

    // Print other primes. Remaining primes are of
    // the form 2*i + 1 such that marked[i] is false.
    for ($i = 1; $i <= $nNew; $i++)
        if ($marked[$i] == false)
            array_push($primes, 2 * $i + 1);
}

// Function to find prime factors of n
// elements of given array
function primeLcm($arr, $n )
{
    global $MAX, $primes;

    // factors[] --> array to mark all prime
    // factors of lcm of array elements
    $factors = array_fill(0, $MAX, 0);

    // One by one calculate prime factors of
    // number and mark them in factors[] array
    for ($i = 0; $i < $n; $i++)
    {
        // copy --> duplicate of original
        // element to perform operation
        $copy = $arr[$i];

        // sqr --> square root of current number
        // 'copy' because all prime factors are
        // always less than and equal to square
        // root of given number
        $sqr = (int)sqrt($copy);

        // check divisibility with prime factor
        for ($j = 0; $primes[$j] <= $sqr; $j++)
        {
            // if current prime number is factor
            // of 'copy'
            if ($copy % $primes[$j] == 0)
            {
                // divide with current prime factor
                // until it can divide the number
                while ($copy % $primes[$j] == 0)
                    $copy = (int)($copy / $primes[$j]);

                // mark current prime factor as 1
                // in factors[] array
                $factors[$primes[$j]] = 1;
            }
        }

        // After calculating exponents of all prime
        // factors either value of 'copy' will be 1
        // because of complete divisibility or remaining
        // value of 'copy' will be surely a prime , so
        // we will also mark this prime as a factor
        if ($copy > 1)
            $factors[$copy] = 1;
    }

    // if 2 is prime factor of lcm of all
    // elements in given array
    if ($factors[2] == 1)
        echo "2 ";

    // traverse to print all prime factors of
    // lcm of all elements in given array
    for ($i = 3; $i <= $MAX; $i = $i + 2)
        if ($factors[$i] == 1)
            echo $i . " ";
}

// Driver Code
sieve();
$arr = array(20, 10, 15, 60);
$n = count($arr);
primeLcm($arr, $n);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find prime
    // factors of LCM of array elements

    let MAX = 1000000;

    // array to store all prime less
    // than and equal to 10^6
    let primes = [];

    // utility function for sieve of sundaram
    function sieve()
    {
        let n = MAX;

        // In general Sieve of Sundaram,
        // produces primes smaller than
        // (2*x + 2) for a number given
        // number x. Since we want primes
        // smaller than n, we reduce n to half
        let nNew = parseInt((n) / 2, 10);

        // This array is used to separate
        // numbers of the form i+j+2ij
        // from others where 1 <= i <= j
        let marked = new Array(nNew + 100);
        marked.fill(false);

        // Main logic of Sundaram. Mark all
        // numbers which do not generate
        // prime number by doing 2*i+1
        let tmp = parseInt(Math.sqrt(n), 10);
        for (let i = 1; i <= parseInt((tmp - 1) / 2, 10); i++)
            for (let j = (i * (i + 1)) << 1; j <= nNew;
            j = j + 2 * i + 1)
                marked[j] = true;

        // Since 2 is a prime number
        primes.push(2);

        // Print other primes. Remaining
        // primes are of the form 2*i + 1
        // such that marked[i] is false.
        for (let i = 1; i <= nNew; i++)
            if (marked[i] == false)
                primes.push(2 * i + 1);
    }

    // Function to find prime factors
    // of n elements of given array
    function primeLcm(arr, n)
    {
        // factors[] --> array to
        // mark all prime factors
        // of lcm of array elements
        let factors = new Array(MAX);

        // One by one calculate prime
        // factors of number and mark
        // them in factors[] array
        for (let i = 0; i < n; i++)
        {
            // copy --> duplicate of original
            // element to perform operation
            let copy = arr[i];

            // sqr --> square root of current
            // number 'copy' because all prime
            // factors are always less than and
            // equal to square root of given number
            let sqr = parseInt(Math.sqrt(copy), 10);

            // check divisibility with prime factor
            for (let j = 0; primes[j] <= sqr; j++)
            {
                // if current prime number is factor of 'copy'
                if (copy % primes[j] == 0)
                {
                    // divide with current prime factor until
                    // it can divide the number
                    while (copy % primes[j] == 0)
                        copy = parseInt(copy / primes[j], 10);

                    // mark current prime factor as 1 in
                    // factors[] array
                    factors[primes[j]] = 1;
                }
            }

            // After calculating exponents of all prime factors
            // either value of 'copy' will be 1 because of
            // complete divisibility or remaining value of
            // 'copy' will be surely a prime , so we will
            // also mark this prime as a factor
            if (copy > 1)
                factors[copy] = 1;
        }

        // if 2 is prime factor of lcm of all elements
        // in given array
        if (factors[2] == 1)
            document.write("2 ");

        // traverse to print all prime factors of lcm of
        // all elements in given array
        for (let i = 3; i <= MAX; i = i + 2)
            if (factors[i] == 1)
                document.write(i+" ");
    }

    sieve();
    let arr = [20, 10, 15, 60];
    let n = arr.length;
    primeLcm(arr, n);

</script>
```

**输出:**

```
2 3 5
```

本文由 [**沙莎克·米什拉(古卢)**](https://www.facebook.com/shashank.mishra.92167) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。