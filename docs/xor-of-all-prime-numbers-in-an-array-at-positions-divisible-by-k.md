# 在可被 K 整除的位置对数组中的所有素数进行异或运算

> 原文:[https://www . geeksforgeeks . org/数组中所有质数的异或位置可被 k 整除/](https://www.geeksforgeeks.org/xor-of-all-prime-numbers-in-an-array-at-positions-divisible-by-k/)

给定一个由大小为 **N** 的整数和一个整数 **K** 组成的数组**，任务是找出所有素数的[异或](https://www.geeksforgeeks.org/tag/xor/)且位于可被**K**整除的位置**

**示例:**

> **输入:** arr[] = {2，3，5，7，11，8}，K = 2
> **输出:** 4
> **说明:**
> 可被 K 整除的位置是 2，4，6，元素是 3，7，8。
> 3 和 7 是其中的素数。
> 因此 XOR = 3 ^ 7 = 4
> 
> **输入:** arr[] = {1，2，3，4，5}，K = 3
> T3】输出: 3

**天真方法:**遍历数组，对于每个可以被 **k** 整除的位置 **i** ，检查它是否是素数。如果它是一个素数，那么计算这个数与前面答案的异或。

**有效方法:**有效方法是使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)。在 **O(1)** 时间内，可以用筛阵检查一个数是否为素数。

下面是上述方法的实现:

## C++

```
// C++ program to find XOR of
// all Prime numbers in an Array
// at positions divisible by K

#include <bits/stdc++.h>
using namespace std;
#define MAX 1000005

void SieveOfEratosthenes(vector<bool>& prime)
{
    // 0 and 1 are not prime numbers
    prime[1] = false;
    prime[0] = false;

    for (int p = 2; p * p < MAX; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2;
                 i < MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to find the required XOR
void prime_xor(int arr[], int n, int k)
{

    vector<bool> prime(MAX, true);

    SieveOfEratosthenes(prime);

    // To store XOR of the primes
    long long int ans = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If the number is a prime
        if (prime[arr[i]]) {

            // If index is divisible by k
            if ((i + 1) % k == 0) {
                ans ^= arr[i];
            }
        }
    }

    // Print the xor
    cout << ans << endl;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 5, 7, 11, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int K = 2;

    // Function call
    prime_xor(arr, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find XOR of
// all Prime numbers in an Array
// at positions divisible by K
class GFG {

    static int MAX = 1000005;
    static boolean prime[] = new boolean[MAX];

    static void SieveOfEratosthenes(boolean []prime)
    {
        // 0 and 1 are not prime numbers
        prime[1] = false;
        prime[0] = false;

        for (int p = 2; p * p < MAX; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2;i < MAX; i += p)
                    prime[i] = false;
            }
        }
    }

    // Function to find the required XOR
    static void prime_xor(int arr[], int n, int k)
    {

        for(int i = 0; i < MAX; i++)
            prime[i] = true;

        SieveOfEratosthenes(prime);

        // To store XOR of the primes
        int ans = 0;

        // Traverse the array
        for (int i = 0; i < n; i++) {

            // If the number is a prime
            if (prime[arr[i]]) {

                // If index is divisible by k
                if ((i + 1) % k == 0) {
                    ans ^= arr[i];
                }
            }
        }

        // Print the xor
        System.out.println(ans);
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 2, 3, 5, 7, 11, 8 };
        int n = arr.length;
        int K = 2;

        // Function call
        prime_xor(arr, n, K);

    }
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python3 program to find XOR of
# all Prime numbers in an Array
# at positions divisible by K
MAX = 1000005

def SieveOfEratosthenes(prime) :

    # 0 and 1 are not prime numbers
    prime[1] = False;
    prime[0] = False;

    for p in range(2, int(MAX ** (1/2))) :

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True) :

            # Update all multiples of p
            for i in range(p * 2, MAX, p) :
                prime[i] = False;

# Function to find the required XOR
def prime_xor(arr, n, k) :

    prime = [True]*MAX ;

    SieveOfEratosthenes(prime);

    # To store XOR of the primes
    ans = 0;

    # Traverse the array
    for i in range(n) :

        # If the number is a prime
        if (prime[arr[i]]) :

            # If index is divisible by k
            if ((i + 1) % k == 0) :
                ans ^= arr[i];

    # Print the xor
    print(ans);

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 3, 5, 7, 11, 8 ];
    n = len(arr);
    K = 2;

    # Function call
    prime_xor(arr, n, K);

# This code is contributed by Yash_R
```

## C#

```
// C# program to find XOR of
// all Prime numbers in an Array
// at positions divisible by K
using System;

class GFG {

    static int MAX = 1000005;
    static bool []prime = new bool[MAX];

    static void SieveOfEratosthenes(bool []prime)
    {
        // 0 and 1 are not prime numbers
        prime[1] = false;
        prime[0] = false;

        for (int p = 2; p * p < MAX; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2;i < MAX; i += p)
                    prime[i] = false;
            }
        }
    }

    // Function to find the required XOR
    static void prime_xor(int []arr, int n, int k)
    {

        for(int i = 0; i < MAX; i++)
            prime[i] = true;

        SieveOfEratosthenes(prime);

        // To store XOR of the primes
        int ans = 0;

        // Traverse the array
        for (int i = 0; i < n; i++) {

            // If the number is a prime
            if (prime[arr[i]]) {

                // If index is divisible by k
                if ((i + 1) % k == 0) {
                    ans ^= arr[i];
                }
            }
        }

        // Print the xor
        Console.WriteLine(ans);
    }

    // Driver code
    public static void Main (string[] args)
    {
        int []arr = { 2, 3, 5, 7, 11, 8 };
        int n = arr.Length;
        int K = 2;

        // Function call
        prime_xor(arr, n, K);

    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>

// Javascript program to find XOR of
// all Prime numbers in an Array
// at positions divisible by K
const MAX = 1000005;

function SieveOfEratosthenes(prime)
{

    // 0 and 1 are not prime numbers
    prime[1] = false;
    prime[0] = false;

    for(let p = 2; p * p < MAX; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for(let i = p * 2; i < MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to find the required XOR
function prime_xor(arr, n, k)
{
    let prime = new Array(MAX).fill(true);

    SieveOfEratosthenes(prime);

    // To store XOR of the primes
    let ans = 0;

    // Traverse the array
    for(let i = 0; i < n; i++)
    {

        // If the number is a prime
        if (prime[arr[i]])
        {

            // If index is divisible by k
            if ((i + 1) % k == 0)
            {
                ans ^= arr[i];
            }
        }
    }

    // Print the xor
    document.write(ans);
}

// Driver code
let arr = [ 2, 3, 5, 7, 11, 8 ];
let n = arr.length;
let K = 2;

// Function call
prime_xor(arr, n, K);

// This code is contributed by subham348

</script>
```

**时间复杂度:** O(N log (log N))

**辅助空间:** O(√n)