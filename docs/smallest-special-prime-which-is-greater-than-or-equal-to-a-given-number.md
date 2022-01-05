# 大于或等于给定数的最小特殊素数

> 原文:[https://www . geesforgeks . org/minist-special-prime-哪个大于或等于给定的数字/](https://www.geeksforgeeks.org/smallest-special-prime-which-is-greater-than-or-equal-to-a-given-number/)

给定一个数 n，任务是找到大于或等于 n 的最小特殊素数
特殊素数是一个数，它可以通过把数字一个接一个地放在一起而产生，这样所有产生的数都是素数。
**例:**

```
Input: N = 379
Output: 379
379 can be created as => 3 => 37 => 379
Here, all the numbers ie. 3, 37, 379 are prime.

Input:N = 100
Output: 233
```

**方法:**思路是用厄拉多塞的筛子。构建 N*10 的筛阵列(假设该数字将存在于该范围内)。然后从数字 N 开始迭代检查这个数字是否是质数。如果它是质数，那么检查它是否是特殊质数。
现在，检查一个数是否是特殊素数。继续将数字除以 10，并在每一点检查剩余的数字是否是质数，这可以通过参考我们构建的筛数组来实现。
以下是上述办法的实施:

## C++

```
// CPP program to find the Smallest Special Prime
// which is greater than or equal to a given number
#include <bits/stdc++.h>
using namespace std;

// Function to check whether the number
// is a special prime or not
bool checkSpecialPrime(bool* sieve, int num)
{
    // While number is not equal to zero
    while (num) {
        // If the number is not prime
        // return false.
        if (!sieve[num]) {
            return false;
        }

        // Else remove the last digit
        // by dividing the number by 10.
        num /= 10;
    }

    // If the number has become zero
    // then the number is special prime,
    // hence return true
    return true;
}

// Function to find the Smallest Special Prime
// which is greater than or equal to a given number
void findSpecialPrime(int N)
{
    bool sieve[N*10];

    // Initially all numbers are considered Primes.
    memset(sieve, true, sizeof(sieve));
    sieve[0] = sieve[1] = false;
    for (long long i = 2; i <= N*10; i++) {
        if (sieve[i]) {

            for (long long j = i * i; j <= N*10; j += i) {
                sieve[j] = false;
            }
        }
    }

    // There is always an answer possible
    while (true) {
        // Checking if the number is a
        // special prime or not
        if (checkSpecialPrime(sieve, N)) {
            // If yes print the number
            // and break the loop.
            cout << N << '\n';
            break;
        }
        // Else increment the number.
        else
            N++;
    }
}

// Driver code
int main()
{
    int N = 379;

    findSpecialPrime(N);

    N = 100;
    findSpecialPrime(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Smallest Special Prime
// which is greater than or equal to a given number

class GFG
{

// Function to check whether the number
// is a special prime or not
static boolean checkSpecialPrime(boolean []sieve, int num)
{
    // While number is not equal to zero
    while (num > 0)
    {
        // If the number is not prime
        // return false.
        if (sieve[num])
        {
            return false;
        }

        // Else remove the last digit
        // by dividing the number by 10.
        num /= 10;
    }

    // If the number has become zero
    // then the number is special prime,
    // hence return true
    return true;
}

// Function to find the Smallest Special Prime
// which is greater than or equal to a given number
static void findSpecialPrime(int N)
{
    boolean[] sieve = new boolean[N * 10 + 1];

    // Initially all numbers are considered Primes.
    sieve[0] = sieve[1] = true;
    for (int i = 2; i <= N * 10; i++)
    {
        if (!sieve[i])
        {
            for (int j = i * i; j <= N * 10; j += i)
            {
                sieve[j] = true;
            }
        }
    }

    // There is always an answer possible
    while (true)
    {
        // Checking if the number is a
        // special prime or not
        if (checkSpecialPrime(sieve, N))
        {
            // If yes print the number
            // and break the loop.
            System.out.println(N);
            break;
        }

        // Else increment the number.
        else
            N++;
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 379;

    findSpecialPrime(N);

    N = 100;
    findSpecialPrime(N);
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to find the Smallest
# Special Prime which is greater than or
# equal to a given number

# Function to check whether the number
# is a special prime or not
def checkSpecialPrime(sieve, num):

    # While number is not equal to zero
    while (num):

        # If the number is not prime
        # return false.
        if (sieve[num] == False):
            return False

        # Else remove the last digit
        # by dividing the number by 10.
        num = int(num / 10)

    # If the number has become zero
    # then the number is special prime,
    # hence return true
    return True

# Function to find the Smallest Special
# Prime which is greater than or equal
# to a given number
def findSpecialPrime(N):
    sieve = [True for i in range(N * 10 + 1)]

    sieve[0] = False
    sieve[1] = False

    # sieve for finding the Primes
    for i in range(2, N * 10 + 1):
        if (sieve[i]):
            for j in range(i * i, N * 10 + 1, i):
                sieve[j] = False

    # There is always an answer possible
    while (True):

        # Checking if the number is a
        # special prime or not
        if (checkSpecialPrime(sieve, N)):

            # If yes print the number
            # and break the loop.
            print(N)
            break

        # Else increment the number.
        else:
            N += 1

# Driver code
if __name__ == '__main__':
    N = 379

    findSpecialPrime(N)

    N = 100
    findSpecialPrime(N)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the Smallest Special Prime
// which is greater than or equal to a given number
using System;

class GFG
{

// Function to check whether the number
// is a special prime or not
static bool checkSpecialPrime(bool []sieve, int num)
{
    // While number is not equal to zero
    while (num > 0)
    {
        // If the number is not prime
        // return false.
        if (sieve[num])
        {
            return false;
        }

        // Else remove the last digit
        // by dividing the number by 10.
        num /= 10;
    }

    // If the number has become zero
    // then the number is special prime,
    // hence return true
    return true;
}

// Function to find the Smallest Special Prime
// which is greater than or equal to a given number
static void findSpecialPrime(int N)
{
    bool[] sieve = new bool[N * 10 + 1];

    // Initially all numbers are considered Primes.
    sieve[0] = sieve[1] = true;
    for (int i = 2; i <= N * 10; i++)
    {
        if (!sieve[i])
        {
            for (int j = i * i; j <= N * 10; j += i)
            {
                sieve[j] = true;
            }
        }
    }

    // There is always an answer possible
    while (true)
    {
        // Checking if the number is a
        // special prime or not
        if (checkSpecialPrime(sieve, N))
        {
            // If yes print the number
            // and break the loop.
            Console.WriteLine(N);
            break;
        }

        // Else increment the number.
        else
            N++;
    }
}

// Driver code
static void Main()
{
    int N = 379;

    findSpecialPrime(N);

    N = 100;
    findSpecialPrime(N);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the Smallest Special
// Prime which is greater than or equal
// to a given number

// Function to check whether the number
// is a special prime or not
function checkSpecialPrime($sieve, $num)
{
    // While number is not equal to zero
    while ($num)
    {
        // If the number is not prime
        // return false.
        if (!$sieve[$num])
        {
            return false;
        }

        // Else remove the last digit
        // by dividing the number by 10.
        $num = floor($num / 10);
    }

    // If the number has become zero
    // then the number is special prime,
    // hence return true
    return true;
}

// Function to find the Smallest Special 
// Prime which is greater than or equal
// to a given number
function findSpecialPrime($N)
{
    // Initially all numbers are
    // considered Primes.
    $sieve = array_fill(0, $N * 10, true);

    $sieve[0] = $sieve[1] = false;
    for ($i = 2; $i <= $N * 10; $i++)
    {
        if ($sieve[$i])
        {

            for ($j = $i * $i;
                 $j <= $N * 10; $j += $i)
            {
                $sieve[$j] = false;
            }
        }
    }

    // There is always an answer possible
    while (true)
    {
        // Checking if the number is a
        // special prime or not
        if (checkSpecialPrime($sieve, $N))
        {

            // If yes print the number
            // and break the loop.
            echo $N, "\n";
            break;
        }

        // Else increment the number.
        else
            $N++;
    }
}

// Driver code
$N = 379;

findSpecialPrime($N);

$N = 100;
findSpecialPrime($N);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// javascript program to find the Smallest Special Prime
// which is greater than or equal to a given number  
// Function to check whether the number
// is a special prime or not
function checkSpecialPrime(sieve , num)
{

    // While number is not equal to zero
    while (num > 0)
    {

        // If the number is not prime
        // return false.
        if (sieve[num])
        {
            return false;
        }

        // Else remove the last digit
        // by dividing the number by 10.
        num = parseInt(num / 10);
    }

    // If the number has become zero
    // then the number is special prime,
    // hence return true
    return true;
}

// Function to find the Smallest Special Prime
// which is greater than or equal to a given number
function findSpecialPrime(N)
{
    var sieve = Array.from({length: N * 10 + 1}, (_, i) => false);

    // Initially all numbers are considered Primes.
    sieve[0] = true;
    sieve[1] = true;
    var i = 0, j = 0;
    for (i = 2; i <= N * 10; i++)
    {
        if (!sieve[i])
        {
            for (j = i * i; j <= N * 10; j += i)
            {
                sieve[j] = true;
            }
        }
    }

    // There is always an answer possible
    while (true)
    {

        // Checking if the number is a
        // special prime or not
        if (checkSpecialPrime(sieve, N))
        {

            // If yes print the number
            // and break the loop.
            document.write(N+"<br>");
            break;
        }

        // Else increment the number.
        else
            N++;
    }
}

// Driver code
var N = 379;
findSpecialPrime(N);
N = 100;
findSpecialPrime(N);

// This code is contributed by shikhasingrajput
</script>
```

**Output:** 

```
379
233
```