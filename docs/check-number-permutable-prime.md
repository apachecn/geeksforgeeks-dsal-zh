# 检查可置换质数的数字

> 原文:[https://www . geesforgeks . org/check-number-permutable-prime/](https://www.geeksforgeeks.org/check-number-permutable-prime/)

给定一个数 N，任务是检查它是否是一个可置换的素数。

一个 **[可置换素数](https://en.wikipedia.org/wiki/Permutable_prime)** 数是通过任意置换变换数字位置后也是素数的数。一些可置换的质数是 2、3、5、7、11 等。

**先决条件:** [素性测试](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) | [CPP next_permute()](https://www.geeksforgeeks.org/permutations-of-a-given-string-using-stl/)

**示例:**

```
Input : 31
Output : Yes
Explanation : 
Both 13 and 31 are prime.

Input : 19
Output : No
Explanation : 
19 is prime but 91 is not

```

**逼近:**
1)构造厄拉多塞的[筛，高效寻找素数。
2)要么通过切换数字来生成数字的每个排列，要么使用内置的 C++函数](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[next _ replacement](https://www.geeksforgeeks.org/stdnext_permutation-prev_permutation-c/)来检查它是否是素数
3)如果数字的任何排列不是素数，只需回答 NO，否则回答 YES。

**以下是上述方法的实施。**

## C++

```
// CPP Program to check whether number is
// permutable prime or not
#include <bits/stdc++.h>
using namespace std;

#define MAX 1000001

// Sieve of Eratosthenes to find the
// prime numbers upto MAX efficiently
void sieveOfEratosthenes(bool* primes)
{
    // 1 is neither prime nor composite
    primes[1] = false;

    for (int i = 2; i * i < MAX; i++) {

        // If prime[i] is not changed,
        // then it is a prime
        if (primes[i] == true) {

            // Update all multiples of i
            for (int j = i * 2; j < MAX; j += i)
                primes[j] = false;
        }
    }
}

// Function returns 1 if the number N is
// permutable prime otherwise not
bool checkPermutablePrime(int N)
{
    // Boolean Array for prime numbers
    bool primes[MAX];

    // Initialize all entries as true.
    // A value in prime[i] will finally
    // be false if i is not a prime,
    // else true.
    memset(primes, true, sizeof(primes));

    sieveOfEratosthenes(primes);

    // Creating Array to store digits
    int num[7];

    // Convert the number into array of digits
    int pos = 0;
    while (N > 0) {
        num[pos++] = N % 10;
        N /= 10;
    }

    // Size of Array
    int SZ = pos;
    int flag = 0;

    sort(num, num + SZ);

    do {

        // Construct the number again
        // from array of digits
        int temp = 0;
        pos = 0;
        while (pos < SZ) {
            temp = temp * 10 + num[pos];
            pos++;
        }

        // check if it is prime of not
        if (primes[temp] == false) {
            flag = 1;
            break;
        }
    } while (next_permutation(num, num + SZ));

    // If flag is 1, number
    // is not permutable prime
    if (flag)
        return false;

    return true;
}

// Driver Code to check above functions
int main()
{
    int N = 31;
    cout << (checkPermutablePrime(N) == 1 ? 
                      "Yes" : "No") << endl;

    N = 19;
    cout << (checkPermutablePrime(N) == 1 ? 
                      "Yes" : "No") << endl;
    return 0;
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check 
// whether number is
// permutable prime or not
$MAX = 100001;
$zz;
$l = 0;

// to find all permutation
// of that number
function next_permutation($items, 
                          $perms = array( )) 
{
    global $zz, $l;
    if (empty($items)) 
    { 
        $zz[$l++] = join($perms);
    } 

    else 
    {
        for ($i = count($items) - 1; 
             $i >= 0; --$i) 
        {
            $newitems = $items;
            $newperms = $perms;
            list($foo) = array_splice($newitems, $i, 1);
            array_unshift($newperms, $foo);
            next_permutation($newitems, $newperms);
        }
    }
    return $zz;
}

// Sieve of Eratosthenes to 
// find the prime numbers 
// upto MAX efficiently
function sieveOfEratosthenes($primes)
{
    global $MAX;

    // 1 is neither prime 
    // nor composite
    $primes[1] = false;

    for ($i = 2; $i * $i < $MAX; $i++)
    {

        // If prime[i] is not changed,
        // then it is a prime
        if ($primes[$i] == true)
        {

            // Update all multiples of i
            for ($j = $i * 2; 
                 $j < $MAX; $j += $i)
                $primes[$j] = false;
        }
    }
    return $primes;
}

// Function returns 1 if the 
// number N is permutable
// prime otherwise not
function checkPermutablePrime($N)
{
    global $MAX, $zz, $l;

    // Boolean Array for
    // prime numbers

    // Initialize all entries 
    // as true. A value in 
    // prime[i] will finally
    // be false if i is not a 
    // prime, else true.
    $primes = array_fill(0, $MAX, true);

    $primes = sieveOfEratosthenes($primes);

    // Creating Array 
    // to store digits
    $num = array();

    // Convert the number 
    // into array of digits
    $pos = 0;
    while ($N > 0) 
    {
        $num[$pos++] = $N % 10;
        $N = (int)($N / 10);
    }

    // Size of Array
    $flag = 0;

    sort($num);
    $num1 = next_permutation($num);
    $i = 0;
    while ($i < count($num1))
    {

        // Construct the number again
        // from array of digits
        $temp = 0;
        $pos = 0;
        while ($pos < strlen($num1[$i])) 
        {
            $temp = $temp * 10 + 
                ord($num1[$i][$pos]) - 48;
            $pos++;
        }

        // check if it is
        // prime of not
        if ($primes[$temp] == false)
        {
            $flag = 1;
            break;
        }
        $i++;
    }

    $zz = array();
    $l = 0;

    // If flag is 1, number
    // is not permutable prime
    if ($flag)
        return false;

    return true;
}

// Driver Code
$N = 31;
echo (checkPermutablePrime($N) == 1 ? 
                              "Yes" : "No") . "\n";

$N = 19;
echo (checkPermutablePrime($N) == 1 ? 
                              "Yes" : "No") . "\n";

// This Code is contributed
// by mits
?>
```

**Output:**

```
Yes
No

```