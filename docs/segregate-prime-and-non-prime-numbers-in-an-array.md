# 在一个数组中分隔质数和非质数

> 原文:[https://www . geeksforgeeks . org/将质数和非质数分隔在一个数组中/](https://www.geeksforgeeks.org/segregate-prime-and-non-prime-numbers-in-an-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是重新排列数组元素，使得所有[素数](https://www.geeksforgeeks.org/prime-numbers/)位于非素数之前。

**示例:**

> **输入:** arr[] = {1，8，2，3，4，5，7，20}
> **输出:** 7 5 2 3 4 8 1 20
> **解释:**
> 输出由所有质数 7 5 2 3 组成，后跟非质数 4 8 1 20。
> 
> **输入:** arr[] = {2，3，4，5，6，7，8，9，10}
> **输出:**2 3 7 5 6 8 9 10

**天真法:**解决这个问题最简单的方法就是制作两个数组分别存储**质数**和**非质数**数组元素，并打印质数后跟非质数。

***时间复杂度:** O(N*sqrt(N))*
***辅助空间:** O(N)*

**交替法:**为了优化上述方法的辅助空间，解决这个问题的思路是使用[双指针法](https://www.geeksforgeeks.org/two-pointers-technique/)。按照以下步骤解决问题:

*   将两个指向数组末尾的指针**左**初始化为 **0** 和**右**为**(N–1)**。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)直到**左**小于**右**并执行以下操作:
    *   继续增加左边的**指针，直到指向左边索引的元素是质数。**
    *   **继续递减**右边的**指针，直到指向左边索引的元素是非质数。**
    *   **如果**左**小于**右**，则**将 arr【左】**和 **arr【右】**互换，并将**左**递增**右**递减 **1** 。**
*   **完成上述步骤后，[打印更新数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **arr[]** 。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to swap two numbers a and b
void swap(int* a, int* b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Function to check if a number n
// is a prime number of not
bool isPrime(int n)
{
    // Edges Cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return true;

    // To skip middle five numbers
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Checks for prime or non prime
    for (int i = 5;
         i * i <= n; i = i + 6) {

        // If n is divisible by i
        // or i + 2, return false
        if (n % i == 0
            || n % (i + 2) == 0)
            return false;
    }

    // Otherwise, the
    // number is prime
    return true;
}

// Function to segregate the primes
// and non-primes present in an array
void segregatePrimeNonPrime(
    int arr[], int N)
{
    // Initialize left and right pointers
    int left = 0, right = N - 1;

    // Traverse the array
    while (left < right) {

        // Increment left while array
        // element at left is prime
        while (isPrime(arr[left]))
            left++;

        // Decrement right while array
        // element at right is non-prime
        while (!isPrime(arr[right]))
            right--;

        // If left < right, then swap
        // arr[left] and arr[right]
        if (left < right) {

            // Swapp arr[left] and arr[right]
            swap(&arr[left], &arr[right]);
            left++;
            right--;
        }
    }

    // Print segregated array
    for (int i = 0; i < N; i++)
        cout << arr[i] << " ";
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 4, 6, 7, 8, 9, 10 };
    int N = sizeof(arr) / sizeof(arr[0]);

    segregatePrimeNonPrime(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to check if a number n
    // is a prime number of not
    static boolean isPrime(int n)
    {
        // Edges Cases
        if (n <= 1)
            return false;

        if (n <= 3)
            return true;

        // To skip middle five numbers
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        // Checks for prime or non prime
        for (int i = 5; i * i <= n; i = i + 6) {

            // If n is divisible by i
            // or i + 2, return false
            if (n % i == 0 || n % (i + 2) == 0)
                return false;
        }

        // Otherwise, the
        // number is prime
        return true;
    }

    // Function to segregate the primes
    // and non-primes present in an array
    static void segregatePrimeNonPrime(int arr[], int N)
    {
        // Initialize left and right pointers
        int left = 0, right = N - 1;

        // Traverse the array
        while (left < right) {

            // Increment left while array
            // element at left is prime
            while (isPrime(arr[left]))
                left++;

            // Decrement right while array
            // element at right is non-prime
            while (!isPrime(arr[right]))
                right--;

            // If left < right, then swap
            // arr[left] and arr[right]
            if (left < right) {

                // Swapp arr[left] and arr[right]
                int temp = arr[right];
                arr[right] = arr[left];
                arr[left] = temp;

                left++;
                right--;
            }
        }

        // Print segregated array
        for (int i = 0; i < N; i++)
            System.out.print(arr[i] + " ");
    }

    // Driver Code
    public static void main(String[] args)
    {

        int arr[] = { 2, 3, 4, 6, 7, 8, 9, 10 };
        int N = arr.length;

        segregatePrimeNonPrime(arr, N);
    }
}

// This code is contributed by Kingash.
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to check if a number n
# is a prime number of not
def isPrime(n):

    # Edges Cases
    if (n <= 1):
        return False

    if (n <= 3):
        return True

    # To skip middle five numbers
    if (n % 2 == 0 or n % 3 == 0):
        return False

    # Checks for prime or non prime
    i = 5

    while (i * i <= n):

        # If n is divisible by i or i + 2,
        # return False
        if (n % i == 0 or n % (i + 2) == 0):
            return False

        i += 6

    # Otherwise, the number is prime
    return True

# Function to segregate the primes and
# non-primes present in an array
def segregatePrimeNonPrime(arr, N):

    # Initialize left and right pointers
    left, right = 0, N - 1

    # Traverse the array
    while (left < right):

        # Increment left while array element
        # at left is prime
        while (isPrime(arr[left])):
            left += 1

        # Decrement right while array element
        # at right is non-prime
        while (not isPrime(arr[right])):
            right -= 1

        # If left < right, then swap
        # arr[left] and arr[right]
        if (left < right):

            # Swapp arr[left] and arr[right]
            arr[left], arr[right] = arr[right], arr[left]
            left += 1
            right -= 1

    # Print segregated array
    for num in arr:
        print(num, end = " ")

# Driver code
arr = [ 2, 3, 4, 6, 7, 8, 9, 10 ]
N = len(arr)

segregatePrimeNonPrime(arr, N)

# This code is contributed by girishthatte
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to check if a number n
// is a prime number of not
static bool isPrime(int n)
{

    // Edges Cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return true;

    // To skip middle five numbers
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Checks for prime or non prime
    for(int i = 5; i * i <= n; i = i + 6)
    {

        // If n is divisible by i
        // or i + 2, return false
        if (n % i == 0 || n % (i + 2) == 0)
            return false;
    }

    // Otherwise, the
    // number is prime
    return true;
}

// Function to segregate the primes
// and non-primes present in an array
static void segregatePrimeNonPrime(int[] arr, int N)
{

    // Initialize left and right pointers
    int left = 0, right = N - 1;

    // Traverse the array
    while (left < right)
    {

        // Increment left while array
        // element at left is prime
        while (isPrime(arr[left]))
            left++;

        // Decrement right while array
        // element at right is non-prime
        while (!isPrime(arr[right]))
            right--;

        // If left < right, then swap
        // arr[left] and arr[right]
        if (left < right)
        {

            // Swapp arr[left] and arr[right]
            int temp = arr[right];
            arr[right] = arr[left];
            arr[left] = temp;

            left++;
            right--;
        }
    }

    // Print segregated array
    for(int i = 0; i < N; i++)
        Console.Write(arr[i] + " ");
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 2, 3, 4, 6, 7, 8, 9, 10 };
    int N = arr.Length;

    segregatePrimeNonPrime(arr, N);
}
}

// This code is contributed by ukasp
```

## **java 描述语言**

```
<script>

// Javascript program implementation
// of the approach

// Function to generate prime numbers
// using Sieve of Eratosthenes
function SieveOfEratosthenes(prime, n)
{
    for(let p = 2; p * p <= n; p++)
    {

        // If prime[p] is unchanged,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for(let i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to segregate the primes and non-primes
function segregatePrimeNonPrime(prime, arr, N)
{

    // Generate all primes till 10^
    SieveOfEratosthenes(prime, 10000000);

    // Initialize left and right
    let left = 0, right = N - 1;

    // Traverse the array
    while (left < right)
    {

        // Increment left while array element
        // at left is prime
        while (prime[arr[left]])
            left++;

        // Decrement right while array element
        // at right is non-prime
        while (!prime[arr[right]])
            right--;

        // If left < right, then swap arr[left]
        // and arr[right]
        if (left < right)
        {

            // Swap arr[left] and arr[right]
            let temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }
    }

    // Print segregated array
    for(let i = 0; i < N; i++)
         document.write(arr[i] + " ");
}

// Driver Code

    let prime = Array.from({length: 10000001}, (_, i) => true);

    let arr = [ 2, 3, 4, 6, 7, 8, 9, 10 ];
    let N = arr.length;

    // Function Call
    segregatePrimeNonPrime(prime, arr, N);

</script>
```

****Output:** 

```
2 3 7 6 4 8 9 10
```** 

*****时间复杂度:** O(N*sqrt(N))*
***辅助空间:** O(1)***

****高效法:**以上方法可以**利用厄拉多塞的[筛进行](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)**优化，在恒定时间内找出数字是质数还是非质数。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
#include <iostream>
using namespace std;
bool prime[10000001];

// Function to swap two numbers a and b
void swap(int* a, int* b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Function to generate prime numbers
// using Sieve of Eratosthenes
void SieveOfEratosthenes(int n)
{
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is unchanged,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * p;
                 i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to segregate the primes
// and non-primes
void segregatePrimeNonPrime(
    int arr[], int N)
{
    // Generate all primes till 10^7
    SieveOfEratosthenes(10000000);

    // Initialize left and right
    int left = 0, right = N - 1;

    // Traverse the array
    while (left < right) {

        // Increment left while array
        // element at left is prime
        while (prime[arr[left]])
            left++;

        // Decrement right while array
        // element at right is non-prime
        while (!prime[arr[right]])
            right--;

        // If left < right, then swap
        // arr[left] and arr[right]
        if (left < right) {

            // Swap arr[left] and arr[right]
            swap(&arr[left], &arr[right]);
            left++;
            right--;
        }
    }

    // Print segregated array
    for (int i = 0; i < N; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 4, 6, 7, 8, 9, 10 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    segregatePrimeNonPrime(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to generate prime numbers
// using Sieve of Eratosthenes
public static void SieveOfEratosthenes(boolean[] prime,
                                       int n)
{
    for(int p = 2; p * p <= n; p++)
    {

        // If prime[p] is unchanged,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for(int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to segregate the primes and non-primes
public static void segregatePrimeNonPrime(boolean[] prime,
                                          int arr[], int N)
{

    // Generate all primes till 10^
    SieveOfEratosthenes(prime, 10000000);

    // Initialize left and right
    int left = 0, right = N - 1;

    // Traverse the array
    while (left < right)
    {

        // Increment left while array element
        // at left is prime
        while (prime[arr[left]])
            left++;

        // Decrement right while array element
        // at right is non-prime
        while (!prime[arr[right]])
            right--;

        // If left < right, then swap arr[left]
        // and arr[right]
        if (left < right)
        {

            // Swap arr[left] and arr[right]
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }
    }

    // Print segregated array
    for(int i = 0; i < N; i++)
        System.out.printf(arr[i] + " ");
}

// Driver code
public static void main(String[] args)
{
    boolean[] prime = new boolean[10000001];
    Arrays.fill(prime, true);
    int arr[] = { 2, 3, 4, 6, 7, 8, 9, 10 };
    int N = arr.length;

    // Function Call
    segregatePrimeNonPrime(prime, arr, N);
}
}

// This code is contributed by girishthatte
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to generate prime numbers
# using Sieve of Eratosthenes
def SieveOfEratosthenes(prime, n):

    p = 2

    while (p * p <= n):

        # If prime[p] is unchanged,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            i = p * p

            while (i <= n):
                prime[i] = False
                i += p

        p += 1

# Function to segregate the primes and non-primes
def segregatePrimeNonPrime(prime, arr, N):

    # Generate all primes till 10^7
    SieveOfEratosthenes(prime, 10000000)

    # Initialize left and right
    left, right = 0, N - 1

    # Traverse the array
    while (left < right):

        # Increment left while array element
        # at left is prime
        while (prime[arr[left]]):
            left += 1

        # Decrement right while array element
        # at right is non-prime
        while (not prime[arr[right]]):
            right -= 1

        # If left < right, then swap arr[left]
        # and arr[right]
        if (left < right):

            # Swap arr[left] and arr[right]
            arr[left], arr[right] = arr[right], arr[left]
            left += 1
            right -= 1

    # Print segregated array
    for num in arr:
        print(num, end = " ")

# Driver code
arr = [ 2, 3, 4, 6, 7, 8, 9, 10 ]
N = len(arr)
prime = [True] * 10000001

# Function Call
segregatePrimeNonPrime(prime, arr, N)

# This code is contributed by girishthatte
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to generate prime numbers
// using Sieve of Eratosthenes
public static void SieveOfEratosthenes(bool[] prime,
                                       int n)
{
    for(int p = 2; p * p <= n; p++)
    {

        // If prime[p] is unchanged,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for(int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to segregate the primes and non-primes
public static void segregatePrimeNonPrime(bool[] prime,
                                          int []arr, int N)
{

    // Generate all primes till 10^
    SieveOfEratosthenes(prime, 10000000);

    // Initialize left and right
    int left = 0, right = N - 1;

    // Traverse the array
    while (left < right)
    {

        // Increment left while array element
        // at left is prime
        while (prime[arr[left]])
            left++;

        // Decrement right while array element
        // at right is non-prime
        while (!prime[arr[right]])
            right--;

        // If left < right, then swap arr[left]
        // and arr[right]
        if (left < right)
        {

            // Swap arr[left] and arr[right]
            int temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }
    }

    // Print segregated array
    for(int i = 0; i < N; i++)
        Console.Write(arr[i] + " ");
}

// Driver code
public static void Main(String[] args)
{
    bool[] prime = new bool[10000001];
    for(int i = 0; i < prime.Length; i++)
        prime[i] = true;

    int []arr = { 2, 3, 4, 6, 7, 8, 9, 10 };
    int N = arr.Length;

    // Function Call
    segregatePrimeNonPrime(prime, arr, N);
}
}

// This code is contributed by Princi Singh
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to generate prime numbers
// using Sieve of Eratosthenes
function SieveOfEratosthenes(prime, n)
{
    for(let p = 2; p * p <= n; p++)
    {

        // If prime[p] is unchanged,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for(let i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to segregate the primes and non-primes
function segregatePrimeNonPrime(prime, arr, N)
{

    // Generate all primes till 10^
    SieveOfEratosthenes(prime, 10000000);

    // Initialize left and right
    let left = 0, right = N - 1;

    // Traverse the array
    while (left < right)
    {

        // Increment left while array element
        // at left is prime
        while (prime[arr[left]])
            left++;

        // Decrement right while array element
        // at right is non-prime
        while (!prime[arr[right]])
            right--;

        // If left < right, then swap arr[left]
        // and arr[right]
        if (left < right)
        {

            // Swap arr[left] and arr[right]
            let temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }
    }

    // Print segregated array
    for(let i = 0; i < N; i++)
        document.write(arr[i] + " ");
}

  // Driver Code

    let prime = Array.from({length: 10000001},
                (_, i) => true);
    let arr = [ 2, 3, 4, 6, 7, 8, 9, 10 ];
    let N = arr.length;

    // Function Call
    segregatePrimeNonPrime(prime, arr, N);

</script>
```

****Output:** 

```
2 3 7 6 4 8 9 10
```** 

*****时间复杂度:**O(N * log(log(N))*
***辅助空间:** O(N)***