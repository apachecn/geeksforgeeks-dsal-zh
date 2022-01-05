# 打印所有质因数及其功率

> 原文:[https://www . geesforgeks . org/print-all-prime-factors-and-power/](https://www.geeksforgeeks.org/print-all-prime-factors-and-their-powers/)

给定一个数字 N，在 N 中打印其所有唯一质因数及其幂。
**示例:**

```
Input: N = 100
Output: Factor Power
          2      2
          5      2

Input: N = 35
Output: Factor  Power
          5      1
          7      1
```

一个**简单的解决方法**是首先[找到 N](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/) 的素因子。然后对于每一个质因数，找到它除以 N 的最高幂并打印出来。
一个**高效解决方案**就是使用厄拉多塞的[筛。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

```
1) First compute an array s[N+1] using Sieve of Eratosthenes.

s[i] = Smallest prime factor of "i" that
       divides "i".

For example let N  = 10
  s[2] = s[4] = s[6] = s[8] = s[10] = 2;
  s[3] = s[9] = 3;
  s[5] = 5;
  s[7] = 7;

2) Using the above computed array s[],
   we can find all powers in O(Log N) time.

    curr = s[N];  // Current prime factor of N
    cnt = 1;   // Power of current prime factor

    // Printing prime factors and their powers
    while (N > 1)
    {
        N /= s[N];

        // N is now N/s[N].  If new N also has its 
        // smallest prime factor as curr, increment 
        // power and continue
        if (curr == s[N])
        {
            cnt++;
            continue;
        }

        // Print prime factor and its power
        print(curr, cnt);

        // Update current prime factor as s[N] and
        // initializing count as 1.
        curr = s[N];
        cnt = 1;
    }
```

下面是以上步骤的实现。

## C++

```
// C++ Program to print prime factors and their
// powers using Sieve Of Eratosthenes
#include<bits/stdc++.h>
using namespace std;

// Using SieveOfEratosthenes to find smallest prime
// factor of all the numbers.
// For example, if N is 10,
// s[2] = s[4] = s[6] = s[10] = 2
// s[3] = s[9] = 3
// s[5] = 5
// s[7] = 7
void sieveOfEratosthenes(int N, int s[])
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries in it as false.
    vector <bool> prime(N+1, false);

    // Initializing smallest factor equal to 2
    // for all the even numbers
    for (int i=2; i<=N; i+=2)
        s[i] = 2;

    // For odd numbers less then equal to n
    for (int i=3; i<=N; i+=2)
    {
        if (prime[i] == false)
        {
            // s(i) for a prime is the number itself
            s[i] = i;

            // For all multiples of current prime number
            for (int j=i; j*i<=N; j+=2)
            {
                if (prime[i*j] == false)
                {
                    prime[i*j] = true;

                    // i is the smallest prime factor for
                    // number "i*j".
                    s[i*j] = i;
                }
            }
        }
    }
}

// Function to generate prime factors and its power
void generatePrimeFactors(int N)
{
    // s[i] is going to store smallest prime factor
    // of i.
    int s[N+1];

    // Filling values in s[] using sieve
    sieveOfEratosthenes(N, s);

    printf("Factor Power\n");

    int curr = s[N];  // Current prime factor of N
    int cnt = 1;   // Power of current prime factor

    // Printing prime factors and their powers
    while (N > 1)
    {
        N /= s[N];

        // N is now N/s[N].  If new N als has smallest
        // prime factor as curr, increment power
        if (curr == s[N])
        {
            cnt++;
            continue;
        }

        printf("%d\t%d\n", curr, cnt);

        // Update current prime factor as s[N] and
        // initializing count as 1.
        curr = s[N];
        cnt = 1;
    }
}

//Driver Program
int main()
{
    int N = 360;
    generatePrimeFactors(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print prime
// factors and their powers using
// Sieve Of Eratosthenes
class GFG
{
// Using SieveOfEratosthenes
// to find smallest prime
// factor of all the numbers.
// For example, if N is 10,
// s[2] = s[4] = s[6] = s[10] = 2
// s[3] = s[9] = 3
// s[5] = 5
// s[7] = 7
static void sieveOfEratosthenes(int N,
                                int s[])
{
    // Create a boolean array
    // "prime[0..n]"  and initialize
    // all entries in it as false.
    boolean[] prime = new boolean[N + 1];

    // Initializing smallest
    // factor equal to 2
    // for all the even numbers
    for (int i = 2; i <= N; i += 2)
        s[i] = 2;

    // For odd numbers less
    // then equal to n
    for (int i = 3; i <= N; i += 2)
    {
        if (prime[i] == false)
        {
            // s(i) for a prime is
            // the number itself
            s[i] = i;

            // For all multiples of
            // current prime number
            for (int j = i; j * i <= N; j += 2)
            {
                if (prime[i * j] == false)
                {
                    prime[i * j] = true;

                    // i is the smallest prime
                    // factor for number "i*j".
                    s[i * j] = i;
                }
            }
        }
    }
}

// Function to generate prime
// factors and its power
static void generatePrimeFactors(int N)
{
    // s[i] is going to store
    // smallest prime factor of i.
    int[] s = new int[N + 1];

    // Filling values in s[] using sieve
    sieveOfEratosthenes(N, s);

    System.out.println("Factor Power");

    int curr = s[N]; // Current prime factor of N
    int cnt = 1; // Power of current prime factor

    // Printing prime factors
    // and their powers
    while (N > 1)
    {
        N /= s[N];

        // N is now N/s[N]. If new N
        // also has smallest prime
        // factor as curr, increment power
        if (curr == s[N])
        {
            cnt++;
            continue;
        }

        System.out.println(curr + "\t" + cnt);

        // Update current prime factor
        // as s[N] and initializing
        // count as 1.
        curr = s[N];
        cnt = 1;
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 360;
    generatePrimeFactors(N);
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to print prime
# factors and their powers
# using Sieve Of Eratosthenes

# Using SieveOfEratosthenes to
# find smallest prime factor
# of all the numbers.

# For example, if N is 10,
# s[2] = s[4] = s[6] = s[10] = 2
# s[3] = s[9] = 3
# s[5] = 5
# s[7] = 7
def sieveOfEratosthenes(N, s):

    # Create a boolean array
    # "prime[0..n]" and initialize
    # all entries in it as false.
    prime = [False] * (N+1)

    # Initializing smallest factor
    # equal to 2 for all the even
    # numbers
    for i in range(2, N+1, 2):
        s[i] = 2

    # For odd numbers less then
    # equal to n
    for i in range(3, N+1, 2):
        if (prime[i] == False):

            # s(i) for a prime is
            # the number itself
            s[i] = i

            # For all multiples of
            # current prime number
            for j in range(i, int(N / i) + 1, 2):
                if (prime[i*j] == False):
                    prime[i*j] = True

                    # i is the smallest
                    # prime factor for
                    # number "i*j".
                    s[i * j] = i

# Function to generate prime
# factors and its power
def generatePrimeFactors(N):

    # s[i] is going to store
    # smallest prime factor
    # of i.
    s = [0] * (N+1)

    # Filling values in s[]
    # using sieve
    sieveOfEratosthenes(N, s)

    print("Factor Power")

    # Current prime factor of N
    curr = s[N]

    # Power of current prime factor
    cnt = 1

    # Printing prime factors and
    #their powers
    while (N > 1):
        N //= s[N]

        # N is now N/s[N]. If new N
        # als has smallest prime
        # factor as curr, increment
        # power
        if (curr == s[N]):
            cnt += 1
            continue

        print(str(curr) + "\t" + str(cnt))

        # Update current prime factor
        # as s[N] and initializing
        # count as 1.
        curr = s[N]
        cnt = 1

#Driver Program
N = 360
generatePrimeFactors(N)

# This code is contributed by Ansu Kumari
```

## C#

```
// C# Program to print prime
// factors and their powers using
// Sieve Of Eratosthenes
class GFG
{
// Using SieveOfEratosthenes
// to find smallest prime
// factor of all the numbers.
// For example, if N is 10,
// s[2] = s[4] = s[6] = s[10] = 2
// s[3] = s[9] = 3
// s[5] = 5
// s[7] = 7
static void sieveOfEratosthenes(int N, int[] s)
{
    // Create a boolean array
    // "prime[0..n]" and initialize
    // all entries in it as false.
    bool[] prime = new bool[N + 1];

    // Initializing smallest
    // factor equal to 2
    // for all the even numbers
    for (int i = 2; i <= N; i += 2)
        s[i] = 2;

    // For odd numbers less
    // then equal to n
    for (int i = 3; i <= N; i += 2)
    {
        if (prime[i] == false)
        {
            // s(i) for a prime is
            // the number itself
            s[i] = i;

            // For all multiples of
            // current prime number
            for (int j = i; j * i <= N; j += 2)
            {
                if (prime[i * j] == false)
                {
                    prime[i * j] = true;

                    // i is the smallest prime
                    // factor for number "i*j".
                    s[i * j] = i;
                }
            }
        }
    }
}

// Function to generate prime
// factors and its power
static void generatePrimeFactors(int N)
{
    // s[i] is going to store
    // smallest prime factor of i.
    int[] s = new int[N + 1];

    // Filling values in s[] using sieve
    sieveOfEratosthenes(N, s);

    System.Console.WriteLine("Factor Power");

    int curr = s[N]; // Current prime factor of N
    int cnt = 1; // Power of current prime factor

    // Printing prime factors
    // and their powers
    while (N > 1)
    {
        N /= s[N];

        // N is now N/s[N]. If new N
        // also has smallest prime
        // factor as curr, increment power
        if (curr == s[N])
        {
            cnt++;
            continue;
        }

        System.Console.WriteLine(curr + "\t" + cnt);

        // Update current prime factor
        // as s[N] and initializing
        // count as 1.
        curr = s[N];
        cnt = 1;
    }
}

// Driver Code
static void Main()
{
    int N = 360;
    generatePrimeFactors(N);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to print prime factors and
// their powers using Sieve Of Eratosthenes

// Using SieveOfEratosthenes to find smallest
// prime factor of all the numbers.
// For example, if N is 10,
// s[2] = s[4] = s[6] = s[10] = 2
// s[3] = s[9] = 3
// s[5] = 5
// s[7] = 7
function sieveOfEratosthenes($N, &$s)
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries in it as false.
    $prime = array_fill(0, $N + 1, false);

    // Initializing smallest factor equal
    // to 2 for all the even numbers
    for ($i = 2; $i <= $N; $i += 2)
        $s[$i] = 2;

    // For odd numbers less then equal to n
    for ($i = 3; $i <= $N; $i += 2)
    {
        if ($prime[$i] == false)
        {
            // s(i) for a prime is the
            // number itself
            $s[$i] = $i;

            // For all multiples of current
            // prime number
            for ($j = $i; $j * $i <= $N; $j += 2)
            {
                if ($prime[$i * $j] == false)
                {
                    $prime[$i * $j] = true;

                    // i is the smallest prime factor
                    // for number "i*j".
                    $s[$i * $j] = $i;
                }
            }
        }
    }
}

// Function to generate prime factors
// and its power
function generatePrimeFactors($N)
{
    // s[i] is going to store smallest
    // prime factor of i.
    $s = array_fill(0, $N + 1, 0);

    // Filling values in s[] using sieve
    sieveOfEratosthenes($N, $s);

    print("Factor Power\n");

    $curr = $s[$N]; // Current prime factor of N
    $cnt = 1; // Power of current prime factor

    // Printing prime factors and their powers
    while ($N > 1)
    {
        if($s[$N])
        $N = (int)($N / $s[$N]);

        // N is now N/s[N]. If new N als has smallest
        // prime factor as curr, increment power
        if ($curr == $s[$N])
        {
            $cnt++;
            continue;
        }

        print($curr . "\t" . $cnt . "\n");

        // Update current prime factor as s[N]
        // and initializing count as 1.
        $curr = $s[$N];
        $cnt = 1;
    }
}

// Driver Code
$N = 360;
generatePrimeFactors($N);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript Program to print prime
// factors and their powers using
// Sieve Of Eratosthenes

// Using SieveOfEratosthenes
// to find smallest prime
// factor of all the numbers.
// For example, if N is 10,
// s[2] = s[4] = s[6] = s[10] = 2
// s[3] = s[9] = 3
// s[5] = 5
// s[7] = 7
function sieveOfEratosthenes(N,  s)
{
    // Create a boolean array
    // "prime[0..n]"  and initialize
    // all entries in it as false.
    prime = Array.from({length: N+1}, (_, i) => false);

    // Initializing smallest
    // factor equal to 2
    // for all the even numbers
    for (i = 2; i <= N; i += 2)
        s[i] = 2;

    // For odd numbers less
    // then equal to n
    for (i = 3; i <= N; i += 2)
    {
        if (prime[i] == false)
        {
            // s(i) for a prime is
            // the number itself
            s[i] = i;

            // For all multiples of
            // current prime number
            for (j = i; j * i <= N; j += 2)
            {
                if (prime[i * j] == false)
                {
                    prime[i * j] = true;

                    // i is the smallest prime
                    // factor for number "i*j".
                    s[i * j] = i;
                }
            }
        }
    }
}

// Function to generate prime
// factors and its power
function generatePrimeFactors(N)
{
    // s[i] is going to store
    // smallest prime factor of i.
    var s = Array.from({length: N+1}, (_, i) => 0);

    // Filling values in s using sieve
    sieveOfEratosthenes(N, s);

    document.write("Factor Power");

    var curr = s[N]; // Current prime factor of N
    var cnt = 1; // Power of current prime factor

    // Printing prime factors
    // and their powers
    while (N > 1)
    {
        N /= s[N];

        // N is now N/s[N]. If new N
        // also has smallest prime
        // factor as curr, increment power
        if (curr == s[N])
        {
            cnt++;
            continue;
        }

        document.write("<br>"+curr + "\t" + cnt);

        // Update current prime factor
        // as s[N] and initializing
        // count as 1.
        curr = s[N];
        cnt = 1;
    }
}

// Driver Code
var N = 360;
generatePrimeFactors(N);

// This code contributed by Princi Singh
</script>
```

**输出:**

```
Factor  Power
  2      3
  3      2
  5      1
```

上面的算法在我们填充 s[]后，在 O(Log N)时间内找到所有幂。这在竞争环境中非常有用，在竞争环境中，我们有一个上限，我们需要为许多测试用例计算质因数及其功率。在这种情况下，数组只需要填充一次。
本文由**拉胡尔·阿格沃尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。