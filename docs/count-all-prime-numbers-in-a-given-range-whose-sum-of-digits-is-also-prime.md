# 计算给定范围内所有素数的个数总和也是素数

> 原文:[https://www . geeksforgeeks . org/count-给定范围内的所有质数-其数字总和也是质数/](https://www.geeksforgeeks.org/count-all-prime-numbers-in-a-given-range-whose-sum-of-digits-is-also-prime/)

给定两个整数 **L** 和 **R** ，任务是求[素数](https://www.geeksforgeeks.org/prime-numbers/)在**【L，R】**范围内的总数的计数，其位数之和也是素数。

**示例:**

> **输入:** L = 1，R = 10
> **输出:** 4
> **说明:**
> L = 1 到 R = 10 范围内的素数为{2，3，5，7}。
> 它们的位数之和是{2，3，5，7}。
> 因为所有的数字都是质数，所以这个问题的答案是 4。
> **输入:** L = 5，R = 20
> **输出:** 3
> **解释:**
> L = 5 到 R = 20 范围内的素数为{5，7，11，13，17，19}.1
> 它们的位数之和为{5，7，2，4，8，10}。
> 只有{5，7，2}是素数，因此查询的答案是 3。

**天真法:**天真法是对**【L，R】**范围内的每个数进行迭代，检查该数是否为素数。如果数是质数，求其位数的和，再次检查和是否是质数。如果总和是质数，则在范围**【L，R】**中增加当前元素的计数器。
***时间复杂度:**O((R–L)* log(log P))，其中 P 为**【L，R】**范围内的素数。*

**有效方法:**

1.  使用厄拉多塞的[筛将所有从 **1** 到**10<sup>6</sup>T5】的质数存储在一个数组中。**](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
2.  创建另一个数组，该数组将存储从 **1** 到 **10 <sup>6</sup>** 的所有数字的数字之和是否为素数。
3.  现在，计算一个[前缀数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)来存储计数，直到每个值都达到极限。
4.  一旦我们有了一个前缀数组，**前缀【R】–前缀【L-1】**的值给出了给定范围内素数并且其和也是素数的元素的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

int maxN = 1000000;

// Create an array for storing primes
int arr[1000001];

// Create a prefix array that will
// contain whether sum is prime or not
int prefix[1000001];

// Function to find primes in the range
// and check whether the sum of digits
// of a prime number is prime or not
void findPrimes()
{
    // Initialise Prime array arr[]
    for (int i = 1; i <= maxN; i++)
        arr[i] = 1;

    // Since 0 and 1 are not prime
    // numbers we mark them as '0'
    arr[0] = 0, arr[1] = 0;

    // Using Sieve Of Eratosthenes
    for (int i = 2; i * i <= maxN; i++) {

        // if the number is prime
        if (arr[i] == 1) {

            // Mark all the multiples
            // of i starting from square
            // of i with '0' ie. composite
            for (int j = i * i;
                 j <= maxN; j += i) {

                //'0' represents not prime
                arr[j] = 0;
            }
        }
    }

    // Initialise a sum variable as 0
    int sum = 0;
    prefix[0] = 0;

    for (int i = 1; i <= maxN; i++) {

        // Check if the number is prime
        if (arr[i] == 1) {

            // A temporary variable to
            // store the number
            int temp = i;
            sum = 0;

            // Loop to calculate the
            // sum of digits
            while (temp > 0) {
                int x = temp % 10;
                sum += x;
                temp = temp / 10;

                // Check if the sum of prime
                // number is prime
                if (arr[sum] == 1) {

                    // if prime mark 1
                    prefix[i] = 1;
                }

                else {

                    // If not prime mark 0
                    prefix[i] = 0;
                }
            }
        }
    }

    // computing prefix array
    for (int i = 1; i <= maxN; i++) {
        prefix[i]
            += prefix[i - 1];
    }
}

// Function to count the prime numbers
// in the range [L, R]
void countNumbersInRange(int l, int r)
{
    // Function Call to find primes
    findPrimes();
    int result = prefix[r]
                 - prefix[l - 1];

    // Print the result
    cout << result << endl;
}

// Driver Code
int main()
{
    // Input range
    int l, r;
    l = 5, r = 20;

    // Function Call
    countNumbersInRange(l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

static int maxN = 1000000;

// Create an array for storing primes
static int []arr = new int[1000001];

// Create a prefix array that will
// contain whether sum is prime or not
static int []prefix = new int[1000001];

// Function to find primes in the range
// and check whether the sum of digits
// of a prime number is prime or not
static void findPrimes()
{
    // Initialise Prime array arr[]
    for (int i = 1; i <= maxN; i++)
        arr[i] = 1;

    // Since 0 and 1 are not prime
    // numbers we mark them as '0'
    arr[0] = 0;
    arr[1] = 0;

    // Using Sieve Of Eratosthenes
    for (int i = 2; i * i <= maxN; i++)
    {

        // if the number is prime
        if (arr[i] == 1)
        {

            // Mark all the multiples
            // of i starting from square
            // of i with '0' ie. composite
            for (int j = i * i;
                     j <= maxN; j += i)
            {

                //'0' represents not prime
                arr[j] = 0;
            }
        }
    }

    // Initialise a sum variable as 0
    int sum = 0;
    prefix[0] = 0;

    for (int i = 1; i <= maxN; i++)
    {

        // Check if the number is prime
        if (arr[i] == 1)
        {

            // A temporary variable to
            // store the number
            int temp = i;
            sum = 0;

            // Loop to calculate the
            // sum of digits
            while (temp > 0)
            {
                int x = temp % 10;
                sum += x;
                temp = temp / 10;

                // Check if the sum of prime
                // number is prime
                if (arr[sum] == 1)
                {

                    // if prime mark 1
                    prefix[i] = 1;
                }

                else
                {

                    // If not prime mark 0
                    prefix[i] = 0;
                }
            }
        }
    }

    // computing prefix array
    for (int i = 1; i <= maxN; i++)
    {
        prefix[i] += prefix[i - 1];
    }
}

// Function to count the prime numbers
// in the range [L, R]
static void countNumbersInRange(int l, int r)
{
    // Function Call to find primes
    findPrimes();
    int result = prefix[r] - prefix[l - 1];

    // Print the result
    System.out.print(result + "\n");
}

// Driver Code
public static void main(String[] args)
{
    // Input range
    int l, r;
    l = 5;
    r = 20;

    // Function Call
    countNumbersInRange(l, r);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for the above approach
maxN = 1000000

# Create an array for storing primes
arr = [0] * (1000001)

# Create a prefix array that will
# contain whether sum is prime or not
prefix = [0] * (1000001)

# Function to find primes in the range
# and check whether the sum of digits
# of a prime number is prime or not
def findPrimes():

    # Initialise Prime array arr[]
    for i in range(1, maxN + 1):
        arr[i] = 1

    # Since 0 and 1 are not prime
    # numbers we mark them as '0'
    arr[0] = 0
    arr[1] = 0

    # Using Sieve Of Eratosthenes
    i = 2
    while i * i <= maxN:

        # If the number is prime
        if (arr[i] == 1):

            # Mark all the multiples
            # of i starting from square
            # of i with '0' ie. composite
            for j in range(i * i, maxN, i):

                # '0' represents not prime
                arr[j] = 0

        i += 1

    # Initialise a sum variable as 0
    sum = 0
    prefix[0] = 0

    for i in range(1, maxN + 1):

        # Check if the number is prime
        if (arr[i] == 1):

            # A temporary variable to
            # store the number
            temp = i
            sum = 0

            # Loop to calculate the
            # sum of digits
            while (temp > 0):
                x = temp % 10
                sum += x
                temp = temp // 10

                # Check if the sum of prime
                # number is prime
                if (arr[sum] == 1):

                    # If prime mark 1
                    prefix[i] = 1

                else:

                    # If not prime mark 0
                    prefix[i] = 0

    # Computing prefix array
    for i in range(1, maxN + 1):
        prefix[i] += prefix[i - 1]

# Function to count the prime numbers
# in the range [L, R]
def countNumbersInRange(l, r):

    # Function call to find primes
    findPrimes()
    result = (prefix[r] - prefix[l - 1])

    # Print the result
    print(result)

# Driver Code
if __name__ == "__main__":

    # Input range
    l = 5
    r = 20

    # Function call
    countNumbersInRange(l, r)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
class GFG{

static int maxN = 1000000;

// Create an array for storing primes
static int []arr = new int[1000001];

// Create a prefix array that will
// contain whether sum is prime or not
static int []prefix = new int[1000001];

// Function to find primes in the range
// and check whether the sum of digits
// of a prime number is prime or not
static void findPrimes()
{
    // Initialise Prime array arr[]
    for (int i = 1; i <= maxN; i++)
        arr[i] = 1;

    // Since 0 and 1 are not prime
    // numbers we mark them as '0'
    arr[0] = 0;
    arr[1] = 0;

    // Using Sieve Of Eratosthenes
    for (int i = 2; i * i <= maxN; i++)
    {

        // if the number is prime
        if (arr[i] == 1)
        {

            // Mark all the multiples
            // of i starting from square
            // of i with '0' ie. composite
            for (int j = i * i;
                     j <= maxN; j += i)
            {

                //'0' represents not prime
                arr[j] = 0;
            }
        }
    }

    // Initialise a sum variable as 0
    int sum = 0;
    prefix[0] = 0;

    for (int i = 1; i <= maxN; i++)
    {

        // Check if the number is prime
        if (arr[i] == 1)
        {

            // A temporary variable to
            // store the number
            int temp = i;
            sum = 0;

            // Loop to calculate the
            // sum of digits
            while (temp > 0)
            {
                int x = temp % 10;
                sum += x;
                temp = temp / 10;

                // Check if the sum of prime
                // number is prime
                if (arr[sum] == 1)
                {

                    // if prime mark 1
                    prefix[i] = 1;
                }

                else
                {

                    // If not prime mark 0
                    prefix[i] = 0;
                }
            }
        }
    }

    // computing prefix array
    for (int i = 1; i <= maxN; i++)
    {
        prefix[i] += prefix[i - 1];
    }
}

// Function to count the prime numbers
// in the range [L, R]
static void countNumbersInRange(int l, int r)
{
    // Function Call to find primes
    findPrimes();
    int result = prefix[r] - prefix[l - 1];

    // Print the result
    Console.Write(result + "\n");
}

// Driver Code
public static void Main()
{
    // Input range
    int l, r;
    l = 5;
    r = 20;

    // Function Call
    countNumbersInRange(l, r);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

let maxN = 1000000;

// Create an array for storing primes
let arr = Array.from({length: 1000001}, (_, i) => 0);
// Create a prefix array that will
// contain whether sum is prime or not
let prefix = Array.from({length: 1000001}, (_, i) => 0);

// Function to find primes in the range
// and check whether the sum of digits
// of a prime number is prime or not
function findPrimes()
{
    // Initialise Prime array arr[]
    for (let i = 1; i <= maxN; i++)
        arr[i] = 1;

    // Since 0 and 1 are not prime
    // numbers we mark them as '0'
    arr[0] = 0;
    arr[1] = 0;

    // Using Sieve Of Eratosthenes
    for (let i = 2; i * i <= maxN; i++)
    {

        // if the number is prime
        if (arr[i] == 1)
        {

            // Mark all the multiples
            // of i starting from square
            // of i with '0' ie. composite
            for (let j = i * i;
                     j <= maxN; j += i)
            {

                //'0' represents not prime
                arr[j] = 0;
            }
        }
    }

    // Initialise a sum variable as 0
    let sum = 0;
    prefix[0] = 0;

    for (let i = 1; i <= maxN; i++)
    {

        // Check if the number is prime
        if (arr[i] == 1)
        {

            // A temporary variable to
            // store the number
            let temp = i;
            sum = 0;

            // Loop to calculate the
            // sum of digits
            while (temp > 0)
            {
                let x = temp % 10;
                sum += x;
                temp = Math.floor(temp / 10);

                // Check if the sum of prime
                // number is prime
                if (arr[sum] == 1)
                {

                    // if prime mark 1
                    prefix[i] = 1;
                }

                else
                {

                    // If not prime mark 0
                    prefix[i] = 0;
                }
            }
        }
    }

    // computing prefix array
    for (let i = 1; i <= maxN; i++)
    {
        prefix[i] += prefix[i - 1];
    }
}

// Function to count the prime numbers
// in the range [L, R]
function countNumbersInRange(l, r)
{
    // Function Call to find primes
    findPrimes();
    let result = prefix[r] - prefix[l - 1];

    // Prlet the result
    document.write(result + "\n");
}

    // Driver Code

     // Input range
    let l, r;
    l = 5;
    r = 20;

    // Function Call
    countNumbersInRange(l, r);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N *(log(log)N))*
***辅助空间:** O(N)*