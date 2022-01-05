# 将给定阵列减少到其 LCM 所需的最小 LCM 替换对数

> 原文:[https://www . geeksforgeeks . org/按其 lcm 最小替换对-要求减少给定阵列到其 lcm/](https://www.geeksforgeeks.org/minimum-replacement-of-pairs-by-their-lcm-required-to-reduce-given-array-to-its-lcm/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是从给定数组中找到需要用它们的 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 替换的最小对数 **(arr[i]，arr[j])** ，这样数组就被简化为一个与初始数组的 LCM 相等的单个元素。
**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 3
> **解释:**
> 数组的 LCM = 12
> 第一步:LCM(3，4) = 12。因此，数组被修改为{1，2，12}
> 步骤 2: LCM(1，12) = 12。因此，数组被修改为{2，12}
> 步骤 3: LCM(2，12) = 12。因此数组修改为{12}
> **输入:** arr[] = {7，9，3}
> **输出:** 2
> **解释:**
> 数组的 LCM = 63
> 第 1 步:LCM(7，9) = 63。因此数组被修改为{63，3}
> 步骤 2: LCM(63，3) = 63。因此数组被修改为{63}

**天真方法:**想法是[生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，对于每个对，用它们的 **LCM** 替换它们，并计算将它们减少到等于它们的 LCM 的单个数组元素所需的步数。打印所需的最小操作数。
***时间复杂度:** O((N！)*log N)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以基于以下观察进行优化:

*   一个数组的 LCM 等于数组中所有[素数](https://www.geeksforgeeks.org/prime-numbers/)的乘积。
*   在**(X–1)**步中，所有 **X** 素数的 LCM 可以用两个数成对得到。
*   在接下来的**(N–2)**步骤中，将剩余的**(N–2)**元素转换为数组的 LCM。
*   因此，总步数由下式给出:

> (N–2)+(X–1)表示 N > 2

*   对于 **N = 1** ，操作次数简单为 **0** ，对于 **N = 2** ，操作次数为 **1** 。

**步骤:**

1.  如果 N = 1，则步数为 **0** 。
2.  如果 N = 2，则步数为 **1** 。
3.  [使用厄拉多塞](https://www.geeksforgeeks.org/print-all-prime-numbers-less-than-or-equal-to-n/)的[筛生成所有直到**N**T3 的素数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
4.  将质数存储在一个变量中，比如 **X** 。
5.  操作总数由下式给出:

> (N–2)+(X–1)表示 N > 2

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

const int maxm = 10001;

// Boolean array to set or unset
// prime non-prime indices
bool prime[maxm];

// Stores the prefix sum of the count
// of prime numbers
int prime_number[maxm];

// Function to check if a number
// is prime or not from 0 to N
void SieveOfEratosthenes()
{
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p < maxm; p++) {

        // If p is a prime
        if (prime[p] == true) {

            // Set its multiples as
            // non-prime
            for (int i = p * p; i < maxm;
                i += p)
                prime[i] = false;
        }
    }

    prime[0] = false;
    prime[1] = false;
}

// Function to store the count of
// prime numbers
void num_prime()
{
    prime_number[0] = 0;

    for (int i = 1; i <= maxm; i++)

        prime_number[i]
            = prime_number[i - 1]
            + prime[i];
}

// Function to count the operations
// to reduce the array to one element
// by replacing each pair with its LCM
void min_steps(int arr[], int n)
{
    // Generating Prime Number
    SieveOfEratosthenes();

    num_prime();

    // Corner Case
    if (n == 1)
        cout << "0\n";

    else if (n == 2)
        cout << "1\n";

    else
        cout << prime_number[n] - 1
                    + (n - 2);
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 5, 4, 3, 2, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    min_steps(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

static final int maxm = 10001;

// Boolean array to set or unset
// prime non-prime indices
static boolean prime[];

// Stores the prefix sum of the count
// of prime numbers
static int prime_number[];

// Function to check if a number
// is prime or not from 0 to N
static void SieveOfEratosthenes()
{
    Arrays.fill(prime,true);

    for(int p = 2; p * p < maxm; p++)
    {

        // If p is a prime
        if (prime[p] == true)
        {

            // Set its multiples as
            // non-prime
            for(int i = p * p; i < maxm; i += p)
                prime[i] = false;
        }
    }
    prime[0] = false;
    prime[1] = false;
}

// Function to store the count of
// prime numbers
static void num_prime()
{
    prime_number[0] = 0;

    for(int i = 1; i <= maxm; i++)
    {
        int tmp;
        if(prime[i] == true)
        {
            tmp = 1;
        }
        else
        {
            tmp = 0;
        }
        prime_number[i] = prime_number[i - 1] + tmp;
    }
}

// Function to count the operations
// to reduce the array to one element
// by replacing each pair with its LCM
static void min_steps(int arr[], int n)
{

    // Generating Prime Number
    SieveOfEratosthenes();

    num_prime();

    // Corner Case
    if (n == 1)
    {
        System.out.println("0");
    }
    else if (n == 2)
    {
        System.out.println("1");
    }
    else
    {
        System.out.println(prime_number[n] - 1 +
                                        (n - 2));
    }
}

// Driver code   
public static void main(String[] args)
{
    prime = new boolean[maxm + 1];

    // Stores the prefix sum of the count
    // of prime numbers
    prime_number = new int[maxm + 1];

    // Given array arr[]
    int arr[] = { 5, 4, 3, 2, 1 };
    int N = arr.length;

    // Function call
    min_steps(arr, N);
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program for
# the above approach
maxm = 10001;

# Boolean array to set or unset
# prime non-prime indices
prime = [True] * (maxm + 1);

# Stores the prefix sum of the count
# of prime numbers
prime_number = [0] * (maxm + 1);

# Function to check if a number
# is prime or not from 0 to N
def SieveOfEratosthenes():

    for p in range(2, (int(maxm ** 1 / 2))):

        # If p is a prime
        if (prime[p] == True):

            # Set its multiples as
            # non-prime
            for i in range(p * p, maxm, p):
                prime[i] = False;

    prime[0] = False;
    prime[1] = False;

# Function to store the count of
# prime numbers
def num_prime():
    prime_number[0] = 0;

    for i in range(1, maxm + 1):
        tmp = -1;
        if (prime[i] == True):
            tmp = 1;
        else:
            tmp = 0;

        prime_number[i] = prime_number[i - 1] + tmp;

# Function to count the operations
# to reduce the array to one element
# by replacing each pair with its LCM
def min_steps(arr, n):

    # Generating Prime Number
    SieveOfEratosthenes();

    num_prime();

    # Corner Case
    if (n == 1):
        print("0");
    elif (n == 2):
        print("1");
    else:
        print(prime_number[n] - 1 + (n - 2));

# Driver code
if __name__ == '__main__':

    # Given array arr
    arr = [5, 4, 3, 2, 1];
    N = len(arr);

    # Function call
    min_steps(arr, N);

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program for the above approach
using System;
class GFG{

static readonly int maxm = 10001;

// Boolean array to set or unset
// prime non-prime indices
static bool []prime;

// Stores the prefix sum of the count
// of prime numbers
static int []prime_number;

// Function to check if a number
// is prime or not from 0 to N
static void SieveOfEratosthenes()
{
    for(int i = 0; i < prime.Length; i++)
        prime[i] = true;
    for(int p = 2; p * p < maxm; p++)
    {       
        // If p is a prime
        if (prime[p] == true)
        {           
            // Set its multiples as
            // non-prime
            for(int i = p * p; i < maxm;
                i += p)
                prime[i] = false;
        }
    }
    prime[0] = false;
    prime[1] = false;
}

// Function to store the count of
// prime numbers
static void num_prime()
{
    prime_number[0] = 0;

    for(int i = 1; i <= maxm; i++)
    {
        int tmp;
        if(prime[i] == true)
        {
            tmp = 1;
        }
        else
        {
            tmp = 0;
        }
        prime_number[i] = prime_number[i - 1] +
                          tmp;
    }
}

// Function to count the operations
// to reduce the array to one element
// by replacing each pair with its LCM
static void min_steps(int []arr, int n)
{   
    // Generating Prime Number
    SieveOfEratosthenes();

    num_prime();

    // Corner Case
    if (n == 1)
    {
        Console.WriteLine("0");
    }
    else if (n == 2)
    {
        Console.WriteLine("1");
    }
    else
    {
        Console.WriteLine(prime_number[n] - 1 +
                          (n - 2));
    }
}

// Driver code   
public static void Main(String[] args)
{
    prime = new bool[maxm + 1];

    // Stores the prefix sum of the count
    // of prime numbers
    prime_number = new int[maxm + 1];

    // Given array []arr
    int []arr = {5, 4, 3, 2, 1};
    int N = arr.Length;

    // Function call
    min_steps(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program for the above approach
     const maxm = 10001;

    // Boolean array to set or unset
    // prime non-prime indices
    var prime = Array();

    // Stores the prefix sum of the count
    // of prime numbers
    var prime_number = Array();

    // Function to check if a number
    // is prime or not from 0 to N
    function SieveOfEratosthenes()
    {
        for(i = 0; i < maxm; i++)
        prime[i] = true;
        for (p = 2; p * p < maxm; p++)
        {

            // If p is a prime
            if (prime[p] == true)
            {

                // Set its multiples as
                // non-prime
                for (i = p * p; i < maxm; i += p)
                    prime[i] = false;
            }
        }
        prime[0] = false;
        prime[1] = false;
    }

    // Function to store the count of
    // prime numbers
    function num_prime() {
        prime_number[0] = 0;

        for (i = 1; i <= maxm; i++) {
            var tmp;
            if (prime[i] == true) {
                tmp = 1;
            } else {
                tmp = 0;
            }
            prime_number[i] = prime_number[i - 1] + tmp;
        }
    }

    // Function to count the operations
    // to reduce the array to one element
    // by replacing each pair with its LCM
    function min_steps(arr , n) {

        // Generating Prime Number
        SieveOfEratosthenes();

        num_prime();

        // Corner Case
        if (n == 1) {
            document.write("0");
        } else if (n == 2) {
            document.write("1");
        } else {
            document.write(prime_number[n] - 1 + (n - 2));
        }
    }

    // Driver code

        // Stores the prefix sum of the count
        // of prime numbers
        prime_number.fill(0);

        // Given array arr
        var arr = [ 5, 4, 3, 2, 1 ];
        var N = arr.length;

        // Function call
        min_steps(arr, N);

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N+log(log(maxm))*
***辅助空间:** O(maxm)*