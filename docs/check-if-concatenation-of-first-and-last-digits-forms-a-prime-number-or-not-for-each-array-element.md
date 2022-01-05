# 检查第一个和最后一个数字的连接是否构成每个数组元素的质数

> 原文:[https://www . geeksforgeeks . org/check-if-concation-first-and-last-digits-forms-a-prime-number-or-not-for-每个数组元素/](https://www.geeksforgeeks.org/check-if-concatenation-of-first-and-last-digits-forms-a-prime-number-or-not-for-each-array-element/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **Q[]** ，数组 **Q[]** 每个元素的任务是检查通过连接 **Q[i]** 的第一个和最后一个数字形成的任何数字是否是[质数](https://www.geeksforgeeks.org/tag/prime-number/)。

**示例:**

> **输入:** Q[] = {30，66 }
> T3】输出:T5】真
> 假
> T8】说明:
> Q[0]:可能的组合是 3 和 30。因为 3 是素数，所以输出为真。
> Q[1]:唯一可能的组合是 66，不是素数。因此，输出为假。
> 
> **输入:** Q[] = {2127，13}
> **输出:**
> 假
> 真
> **说明:**
> Q[0]:可能的组合是 27 和 72。因为它们都不是质数，所以输出为假。
> Q[1]:可能的组合是 13 和 31。因为它们都是质数，所以输出为真。

**方法:**使用厄拉多塞的[筛子可以高效解决问题。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 按照以下步骤解决给定问题:

1.  由于通过组合一对数字可能得到的最高数字是 99，因此使用厄拉多塞的[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)预先计算并存储所有质数到的 99，并将其存储在布尔数组中，比如**质数【】**，其中**质数【I】= 0**(非质数)和 **1** (质数)。
2.  [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **Q[]，**并执行以下步骤:
    *   通过执行 **Q[i] % 10** 提取 **Q[i]** 的最后一位数字并存储在变量中，比如说**最后一位**。
    *   通过将 **Q[i]** 连续除以 **10** 提取 **Q[i]** 的第一个数字，直到 **Q[i]** 减少到小于 **10** 并将其存储在一个变量中，先说**。**
    *   **现在，生成两种可能的组合:

        *   **第一* 10 +最后**。
        *   **最后* 10 +第一**。** 
    *   **对于以上两种组合中的每一种，[检查它们中是否有质数](https://www.geeksforgeeks.org/prime-numbers/)。**
    *   **如果任何形成的数字被发现是质数，那么打印真，否则打印假。**

**下面是上述方法的实现。**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores if i is prime (1)
// or non-prime(0)
int sieve[105];

// Function to build sieve array
void buildSieve()
{
    // Initialize all the values
    // in sieve equals to 1
    for (int i = 2; i < 100; i++)
        sieve[i] = 1;

    // Sieve of Eratosthenes
    for (int i = 2; i < 100; i++) {

        // If current number is prime
        if (sieve[i] == 1) {

            // Set all multiples as non-prime
            for (int j = i * i; j < 100; j += i)
                sieve[j] = 0;
        }
    }
}

// Function to check if the numbers formed
// by combining first and last digits
// generates a prime number or not
bool isAnyPrime(int first, int last)
{
    int num1 = first * 10 + last;
    int num2 = last * 10 + first;

    // Check if any of the numbers
    // formed is a prime number or not
    if (sieve[num1] == 1 || sieve[num2] == 1)
        return true;
    else
        return false;
}

void performQueries(vector<int> q)
{

    // Traverse the array of queries
    for (int i = 0; i < q.size(); i++) {
        int A = q[i];

        // Extract the last digit
        int last = A % 10;

        // Extract the first digit
        int first;
        while (A >= 10)
            A = A / 10;
        first = A;

        // If any of the two
        // numbers is prime
        if (isAnyPrime(first, last))
            cout << "True\n";

        // Otherwise
        else
            cout << "False\n";
    }
}

// Driver Code
int main()
{
    vector<int> q = { 30, 66 };

    // Computes and stores
    // primes using Sieve
    buildSieve();

    // Function call to perform queries
    performQueries(q);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

// Stores if i is prime (1)
// or non-prime(0)
static int[] sieve = new int[105];

// Function to build sieve array
static void buildSieve()
{

    // Initialize all the values
    // in sieve equals to 1
    for (int i = 2; i < 100; i++)
        sieve[i] = 1;

    // Sieve of Eratosthenes
    for (int i = 2; i < 100; i++) {

        // If current number is prime
        if (sieve[i] == 1) {

            // Set all multiples as non-prime
            for (int j = i * i; j < 100; j += i)
                sieve[j] = 0;
        }
    }
}

// Function to check if the numbers formed
// by combining first and last digits
// generates a prime number or not
static boolean isAnyPrime(int first, int last)
{
    int num1 = first * 10 + last;
    int num2 = last * 10 + first;

    // Check if any of the numbers
    // formed is a prime number or not
    if (sieve[num1] == 1 || sieve[num2] == 1)
        return true;
    else
        return false;
}

static void performQueries(int[] q)
{

    // Traverse the array of queries
    for (int i = 0; i < q.length; i++) {
        int A = q[i];

        // Extract the last digit
        int last = A % 10;

        // Extract the first digit
        int first;
        while (A >= 10)
            A = A / 10;
        first = A;

        // If any of the two
        // numbers is prime
        if (isAnyPrime(first, last))
            System.out.println("True\n");

        // Otherwise
        else
            System.out.print("False\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int[] q = { 30, 66 };

    // Computes and stores
    // primes using Sieve
    buildSieve();

    // Function call to perform queries
    performQueries(q);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## **蟒蛇 3**

```
# Python 3 program for the above approach

# Stores if i is prime (1)
# or non-prime(0)
sieve = [0 for i in range(105)]

# Function to build sieve array
def buildSieve():
    global sieve

    # Initialize all the values
    # in sieve equals to 1
    for i in range(2, 100):
        sieve[i] = 1

    # Sieve of Eratosthenes
    for i in range(2, 100):

        # If current number is prime
        if (sieve[i] == 1):

            # Set all multiples as non-prime
            for j in range( i* i, 100, i):
                sieve[j] = 0

# Function to check if the numbers formed
# by combining first and last digits
# generates a prime number or not
def isAnyPrime(first, last):
    global sieve
    num1 = first * 10 + last
    num2 = last * 10 + first

    # Check if any of the numbers
    # formed is a prime number or not
    if (sieve[num1] == 1 or sieve[num2] == 1):
        return True
    else:
        return False

def performQueries(q):

    # Traverse the array of queries
    for i in range(len(q)):
        A = q[i]

        # Extract the last digit
        last = A % 10

        # Extract the first digit
        first = 0
        while (A >= 10):
            A = A // 10
        first = A

        # If any of the two
        # numbers is prime
        if (isAnyPrime(first, last)):
            print("True")

        # Otherwise
        else:
            print("False")

# Driver Code
if __name__ == '__main__':
    q =  [30, 66]

    # Computes and stores
    # primes using Sieve
    buildSieve()

    # Function call to perform queries
    performQueries(q)

    # This code is contributed by bgangwar59.
```

## **C#**

```
// C# program for above approach
/*package whatever //do not write package name here */
using System;
public class GFG
{

// Stores if i is prime (1)
// or non-prime(0)
static int[] sieve = new int[105];

// Function to build sieve array
static void buildSieve()
{

    // Initialize all the values
    // in sieve equals to 1
    for (int i = 2; i < 100; i++)
        sieve[i] = 1;

    // Sieve of Eratosthenes
    for (int i = 2; i < 100; i++)
    {

        // If current number is prime
        if (sieve[i] == 1)
        {

            // Set all multiples as non-prime
            for (int j = i * i; j < 100; j += i)
                sieve[j] = 0;
        }
    }
}

// Function to check if the numbers formed
// by combining first and last digits
// generates a prime number or not
static bool isAnyPrime(int first, int last)
{
    int num1 = first * 10 + last;
    int num2 = last * 10 + first;

    // Check if any of the numbers
    // formed is a prime number or not
    if (sieve[num1] == 1 || sieve[num2] == 1)
        return true;
    else
        return false;
}

static void performQueries(int[] q)
{

    // Traverse the array of queries
    for (int i = 0; i < q.Length; i++) {
        int A = q[i];

        // Extract the last digit
        int last = A % 10;

        // Extract the first digit
        int first;
        while (A >= 10)
            A = A / 10;
        first = A;

        // If any of the two
        // numbers is prime
        if (isAnyPrime(first, last))
            Console.Write("True\n");

        // Otherwise
        else
            Console.Write("False\n");
    }
}

// Driver code
public static void Main(String[] args)
{
    int[] q = { 30, 66 };

    // Computes and stores
    // primes using Sieve
    buildSieve();

    // Function call to perform queries
    performQueries(q);
}
}

// This code is contributed by code_hunt.
```

## **java 描述语言**

```
<script>
// javascript program for the above approach

// Stores if i is prime (1)
// or non-prime(0)
var sieve = Array.from({length: 105}, (_, i) => 0);

// Function to build sieve array
function buildSieve()
{

    // Initialize all the values
    // in sieve equals to 1
    for (i = 2; i < 100; i++)
        sieve[i] = 1;

    // Sieve of Eratosthenes
    for (i = 2; i < 100; i++) {

        // If current number is prime
        if (sieve[i] == 1) {

            // Set all multiples as non-prime
            for (j = i * i; j < 100; j += i)
                sieve[j] = 0;
        }
    }
}

// Function to check if the numbers formed
// by combining first and last digits
// generates a prime number or not
function isAnyPrime(first , last)
{
    var num1 = first * 10 + last;
    var num2 = last * 10 + first;

    // Check if any of the numbers
    // formed is a prime number or not
    if (sieve[num1] == 1 || sieve[num2] == 1)
        return true;
    else
        return false;
}

function performQueries(q)
{

    // Traverse the array of queries
    for (i = 0; i < q.length; i++) {
        var A = q[i];

        // Extract the last digit
        var last = A % 10;

        // Extract the first digit
        var first;
        while (A >= 10)
            A = A / 10;
        first = A;

        // If any of the two
        // numbers is prime
        if (isAnyPrime(first, last))
            document.write("True<br>");

        // Otherwise
        else
            document.write("False");
    }
}

// Driver Code
var q = [ 30, 66 ];

// Computes and stores
// primes using Sieve
buildSieve();

// Function call to perform queries
performQueries(q);

// This code is contributed by Princi Singh

</script>
```

****Output:** 

```
True
False
```** 

*****时间复杂度:**O(N)*
T5】辅助*T8】空间: O(1)***