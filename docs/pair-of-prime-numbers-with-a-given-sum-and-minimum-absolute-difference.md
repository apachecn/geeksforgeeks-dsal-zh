# 给定和和最小绝对差的一对素数

> 原文:[https://www . geesforgeks . org/给定和与最小绝对差的素数对/](https://www.geeksforgeeks.org/pair-of-prime-numbers-with-a-given-sum-and-minimum-absolute-difference/)

给定一个整数‘和’(小于 10^8)，任务是从所有可能的对中找出一对和等于给定‘和’
的素数，所选对之间的绝对差必须最小。
如果‘和’不能表示为两个素数的和，则打印“不能表示为两个素数的和”。
**例:**

```
Input : Sum = 1002
Output : Primes: 499 503
Explanation
1002 can be represented as sum of many prime number pairs
such as
499 503
479 523
461 541
439 563
433 569
431 571
409 593
401 601...
But 499 and 503 is the only pair which has minimum difference 

Input :Sum = 2002
Output : Primes: 983 1019
```

**解**T2】

*   我们将创建一个厄拉多塞筛，它将存储所有的素数，并在 O(1)时间内检查一个数是否是素数。
*   现在，要找到两个和等于给定变量的质数，“和”。我们将从 sum/2 到 1 开始循环(以最小化绝对差)，并检查循环计数器“I”和“sum-i”是否都是质数。
*   如果它们是质数，那么我们将打印它们并打破循环。
*   如果‘和’不能表示为两个素数的和，那么我们将打印“不能表示为两个素数的和”。

以下是上述解决方案的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 100000000

// stores whether a number is prime or not
bool prime[MAX + 1];

// create the sieve of eratosthenes
void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    memset(prime, true, sizeof(prime));

    prime[1] = false;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p as non-prime
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// find the two prime numbers with minimum
// difference and whose sum is equal to
// variable sum
void find_Prime(int sum)
{

    // start from sum/2 such that
    // difference between i and sum-i will be
    // minimum
    for (int i = sum / 2; i > 1; i--) {

        // if both 'i' and 'sum - i' are prime then print
        // them and break the loop
        if (prime[i] && prime[sum - i]) {
            cout << i << " " << (sum - i) << endl;
            return;
        }
    }
    // if there is no prime
    cout << "Cannot be represented as sum of two primes" << endl;
}

// Driver code
int main()
{
    // create the sieve
    SieveOfEratosthenes();

    int sum = 1002;

    // find the primes
    find_Prime(sum);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the above approach

class GFG {

    static final int MAX = 100000000;

    // stores whether a number is prime or not
    static boolean prime[] = new boolean[MAX + 1];

    // create the sieve of eratosthenes
    static void SieveOfEratosthenes() {
        // Create a boolean array "prime[0..n]" and initialize
        // all entries it as true. A value in prime[i] will
        // finally be false if i is Not a prime, else true.
        for (int i = 0; i < prime.length; i++) {
            prime[i] = true;
        }
        prime[1] = false;

        for (int p = 2; p * p <= MAX; p++) {

            // If prime[p] is not changed, then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p as non-prime
                for (int i = p * 2; i <= MAX; i += p) {
                    prime[i] = false;
                }
            }
        }
    }

    // find the two prime numbers with minimum
    // difference and whose sum is equal to
    // variable sum
    static void find_Prime(int sum) {

        // start from sum/2 such that
        // difference between i and sum-i will be
        // minimum
        for (int i = sum / 2; i > 1; i--) {

            // if both 'i' and 'sum - i' are prime then print
            // them and break the loop
            if (prime[i] && prime[sum - i]) {
                System.out.println(i + " " + (sum - i));
                return;
            }
        }
        // if there is no prime
        System.out.println("Cannot be represented as sum of two primes");
    }
    public static void main(String []args) {
        // create the sieve
        SieveOfEratosthenes();
        int sum = 1002;
        // find the primes
        find_Prime(sum);
    }
}
/*This code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach
from math import sqrt

# stores whether a number is prime or not

# create the sieve of eratosthenes
def SieveOfEratosthenes():
    MAX = 1000001

    # Create a boolean array "prime[0..n]" and
    # initialize all entries it as true. A value
    # in prime[i] will finally be false if i is
    # Not a prime, else true.
    prime = [True for i in range(MAX + 1)]

    prime[1] = False

    for p in range(2, int(sqrt(MAX)) + 1, 1):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            # as non-prime
            for i in range(p * 2, MAX + 1, p):
                prime[i] = False

    return prime

# find the two prime numbers with minimum
# difference and whose sum is equal to
# variable sum
def find_Prime(sum):

    # start from sum/2 such that difference
    # between i and sum-i will be minimum
    # create the sieve
    prime = SieveOfEratosthenes()
    i = int(sum / 2)
    while(i > 1):

        # if both 'i' and 'sum - i' are prime
        # then print them and break the loop
        if (prime[i] and prime[sum - i]):
            print(i, (sum - i))
            return

        i -= 1

    # if there is no prime
    print("Cannot be represented as sum",
                         "of two primes")

# Driver code
if __name__ == '__main__':

    sum = 1002

    # find the primes
    find_Prime(sum)

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# implementation of the
// above approach
class GFG
{

static int MAX = 1000000;

// stores whether a number is
// prime or not
static bool[] prime = new bool[MAX + 1];

// create the sieve of eratosthenes
static void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally be
    // false if i is Not a prime, else true.
    for (int i = 0; i < prime.Length; i++)
    {
        prime[i] = true;
    }
    prime[1] = false;

    for (int p = 2; p * p <= MAX; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            // as non-prime
            for (int i = p * 2;
                     i <= MAX; i += p)
            {
                prime[i] = false;
            }
        }
    }
}

// find the two prime numbers with
// minimum difference and whose sum
// is equal to variable sum
static void find_Prime(int sum)
{

    // start from sum/2 such that
    // difference between i and sum-i
    // will be minimum
    for (int i = sum / 2; i > 1; i--)
    {

        // if both 'i' and 'sum - i'
        // are prime then print
        // them and break the loop
        if (prime[i] && prime[sum - i])
        {
            System.Console.WriteLine(i + " " +
                                    (sum - i));
            return;
        }
    }

    // if there is no prime
    System.Console.WriteLine("Cannot be represented " +   
                               "as sum of two primes");
}

// Driver Code
static void Main()
{
    // create the sieve
    SieveOfEratosthenes();
    int sum = 1002;

    // find the primes
    find_Prime(sum);
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach
var MAX = 1000001;

// stores whether a number is prime or not
var prime = Array(MAX+1).fill(true);

// create the sieve of eratosthenes
function SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    prime[1] = false;

    for (var p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p as non-prime
            for (var i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// find the two prime numbers with minimum
// difference and whose sum is equal to
// variable sum
function find_Prime(sum)
{

    // start from sum/2 such that
    // difference between i and sum-i will be
    // minimum
    for (var i = parseInt(sum / 2); i > 1; i--) {

        // if both 'i' and 'sum - i' are prime then print
        // them and break the loop
        if (prime[i] && prime[sum - i]) {
            document.write( i + " " + (sum - i) + "<br>");
            return;
        }
    }
    // if there is no prime
    document.write( "Cannot be represented as sum of two primes" + "<br>");
}

// Driver code
// create the sieve
SieveOfEratosthenes();
var sum = 1002;
// find the primes
find_Prime(sum);

</script>
```

**Output:** 

```
499 503
```