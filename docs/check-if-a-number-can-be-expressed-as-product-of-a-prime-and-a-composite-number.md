# 检查一个数是否可以表示为一个质数和一个合成数的乘积

> 原文:[https://www . geesforgeks . org/check-if-a-number-can-express-as-product-of-a-prime-and-a-composite-number/](https://www.geeksforgeeks.org/check-if-a-number-can-be-expressed-as-product-of-a-prime-and-a-composite-number/)

给定一个数字 **N，**的任务是检查 **N** 是否可以表示为一个[素数](https://www.geeksforgeeks.org/prime-numbers/)和一个复合数的乘积。如果可以，那么打印**是**，否则**否**。

**示例:**

> **输入:** N = 52
> **输出:**是
> **说明:** 52 可以表示为 4 和 13 的乘积，其中 4 是复合数，13 是素数。
> 
> **输入:**N = 49
> T3】输出:否

**方法:**这个问题可以借助厄拉多塞算法的[筛来解决。现在，要解决这个问题，请遵循以下步骤:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

1.  创建一个布尔数组**是素**，其中带有元素的**是**真**如果是素，否则是**假**。**
2.  使用筛选算法找到所有质数直到 **N** 。
3.  现在为 **i=2 到 i < N** 运行一个[循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)，在每次迭代中:
    *   检查这两种情况:
        *   如果 **N** 被 **i** 整除。
        *   如果 **i** 是素数而 **N/i** 不是，或者如果我不是素数而 **N/i** 是。
    *   如果以上两个条件都满足，返回**真**。
    *   否则，返回**假**。
4.  打印答案，根据以上观察。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate all prime
// numbers less than N
void SieveOfEratosthenes(int N, bool isPrime[])
{
    // Initialize all entries of boolean array
    // as true. A value in isPrime[i] will finally
    // be false if i is Not a prime, else true
    // bool isPrime[N+1];
    isPrime[0] = isPrime[1] = false;
    for (int i = 2; i <= N; i++)
        isPrime[i] = true;

    for (int p = 2; p * p <= N; p++) {

        // If isPrime[p] is not changed,
        // then it is a prime
        if (isPrime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= N; i += p)
                isPrime[i] = false;
        }
    }
}

// Function to check if we can
// represent N as product of a prime
// and a composite number or not
bool isRepresentable(int N)
{

    // Generating primes using Sieve
    bool isPrime[N + 1];

    SieveOfEratosthenes(N, isPrime);

    // Traversing through the array
    for (int i = 2; i < N; i++) {

        if (N % i == 0) {
            if (N % i == 0
                    and (isPrime[i] and !isPrime[N / i])
                or (!isPrime[i] and isPrime[N / i])) {
                return true;
            }
        }
    }

    return false;
}

// Driver Code
int main()
{
    int N = 52;
    if (isRepresentable(N)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach
import java.util.*;
public class GFG
{

// Function to generate all prime
// numbers less than N
static void SieveOfEratosthenes(int N, boolean []isPrime)
{

    // Initialize all entries of boolean array
    // as true. A value in isPrime[i] will finally
    // be false if i is Not a prime, else true
    // bool isPrime[N+1];
    isPrime[0] = isPrime[1] = false;
    for (int i = 2; i <= N; i++)
        isPrime[i] = true;

    for (int p = 2; p * p <= N; p++) {

        // If isPrime[p] is not changed,
        // then it is a prime
        if (isPrime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= N; i += p)
                isPrime[i] = false;
        }
    }
}

// Function to check if we can
// represent N as product of a prime
// and a composite number or not
static boolean isRepresentable(int N)
{

    // Generating primes using Sieve
    boolean []isPrime = new boolean[N + 1];

    SieveOfEratosthenes(N, isPrime);

    // Traversing through the array
    for (int i = 2; i < N; i++) {

        if (N % i == 0) {
            if (N % i == 0
                    && (isPrime[i] && !isPrime[N / i])
                || (!isPrime[i] && isPrime[N / i])) {
                return true;
            }
        }
    }

    return false;
}

// Driver Code
public static void main(String arg[])
{
    int N = 52;
    if (isRepresentable(N)) {
        System.out.println("Yes");
    }
    else {
        System.out.println("No");
    }
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# python program for the above approach
import math

# Function to generate all prime
# numbers less than N
def SieveOfEratosthenes(N, isPrime):

    # Initialize all entries of boolean array
    # as true. A value in isPrime[i] will finally
    # be false if i is Not a prime, else true
    # bool isPrime[N+1];
    isPrime[0] = False
    isPrime[1] = False
    for i in range(2, N+1):
        isPrime[i] = True

    for p in range(2, int(math.sqrt(N)) + 1):

        # If isPrime[p] is not changed,
        # then it is a prime
        if (isPrime[p] == True):

            # Update all multiples of p
            for i in range(p+2, N+1, p):
                isPrime[i] = False

# Function to check if we can
# represent N as product of a prime
# and a composite number or not
def isRepresentable(N):

    # Generating primes using Sieve
    isPrime = [0 for _ in range(N + 1)]

    SieveOfEratosthenes(N, isPrime)

    # Traversing through the array
    for i in range(2, N):

        if (N % i == 0):
            if (N % i == 0 and (isPrime[i] and not isPrime[N // i]) or (not isPrime[i] and isPrime[N // i])):
                return True

    return False

# Driver Code
if __name__ == "__main__":

    N = 52
    if (isRepresentable(N)):
        print("Yes")

    else:
        print("No")

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program to implement the above approach
using System;
class GFG
{
// Function to generate all prime
// numbers less than N
static void SieveOfEratosthenes(int N, bool []isPrime)
{
    // Initialize all entries of boolean array
    // as true. A value in isPrime[i] will finally
    // be false if i is Not a prime, else true
    // bool isPrime[N+1];
    isPrime[0] = isPrime[1] = false;
    for (int i = 2; i <= N; i++)
        isPrime[i] = true;

    for (int p = 2; p * p <= N; p++) {

        // If isPrime[p] is not changed,
        // then it is a prime
        if (isPrime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= N; i += p)
                isPrime[i] = false;
        }
    }
}

// Function to check if we can
// represent N as product of a prime
// and a composite number or not
static bool isRepresentable(int N)
{

    // Generating primes using Sieve
    bool []isPrime = new bool[N + 1];

    SieveOfEratosthenes(N, isPrime);

    // Traversing through the array
    for (int i = 2; i < N; i++) {

        if (N % i == 0) {
            if (N % i == 0
                    && (isPrime[i] && !isPrime[N / i])
                || (!isPrime[i] && isPrime[N / i])) {
                return true;
            }
        }
    }

    return false;
}

// Driver Code
public static void Main()
{
    int N = 52;
    if (isRepresentable(N)) {
        Console.Write("Yes");
    }
    else {
        Console.Write("No");
    }
}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to generate all prime
// numbers less than N
function SieveOfEratosthenes(N, isPrime)
{
    // Initialize all entries of boolean array
    // as true. A value in isPrime[i] will finally
    // be false if i is Not a prime, else true
    // bool isPrime[N+1];
    isPrime[0] = isPrime[1] = false;
    for (let i = 2; i <= N; i++)
        isPrime[i] = true;

    for (let p = 2; p * p <= N; p++) {

        // If isPrime[p] is not changed,
        // then it is a prime
        if (isPrime[p] == true) {

            // Update all multiples of p
            for (let i = p * 2; i <= N; i += p)
                isPrime[i] = false;
        }
    }
}

// Function to check if we can
// represent N as product of a prime
// and a composite number or not
function isRepresentable(N)
{

    // Generating primes using Sieve
    let isPrime = [];

    SieveOfEratosthenes(N, isPrime);

    // Traversing through the array
    for (let i = 2; i < N; i++) {

        if (N % i == 0) {
            if (N % i == 0
                    && (isPrime[i] && !isPrime[N / i])
                || (!isPrime[i] && isPrime[N / i])) {
                return true;
            }
        }
    }

    return false;
}

// Driver Code
let N = 52;
if (isRepresentable(N)) {
  document.write("Yes");
}

else {
  document.write("No");
}

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
Yes
```

**时间复杂度:**O(N * log(logN))
T3】辅助空间: O(N)