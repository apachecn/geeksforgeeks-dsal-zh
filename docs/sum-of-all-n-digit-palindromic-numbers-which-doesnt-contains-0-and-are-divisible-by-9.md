# 不含 0 且可被 9 整除的所有 N 位回文数之和

> 原文:[https://www . geeksforgeeks . org/所有 n 位回文数字之和不包含 0 且可被 9 整除/](https://www.geeksforgeeks.org/sum-of-all-n-digit-palindromic-numbers-which-doesnt-contains-0-and-are-divisible-by-9/)

给定一个数字 **N** ，任务是找到所有 N 位回文数字的[和，这些数字可以被 **9** 整除，并且其中不包含 0。
**注:**之和可以很大，取 10 <sup>9</sup> +7 的模。
**例:**](https://www.geeksforgeeks.org/sum-of-all-n-digit-palindrome-numbers/) 

> **输入:** N = 2
> **输出:** 99
> **解释:**
> 只有一个能被 9 整除的 2 位数回文号是 99。
> **输入:** N = 3
> **输出:** 4995

**天真方法:**想法是迭代所有的 **N 位数**并检查这些数字是否是回文并且能被 9 整除并且其中不包含零。如果是，那么给定所需结果的所有数字的总和。
**高效方法:**以下是对此问题陈述的一些观察:

1.  如果 N 是奇数，那么这个数可以是**ab 的形式..x..ba"** 如果 N 是偶数，那么这个数可以是 **"ab..xx..ba"** ，其中' a '，' b '和' x '可以用 1 到 9 的数字代替。
2.  如果数字“ab..x..ba”被 9 整除， **(2*(a+b) + x)** 必须被 **9** 整除。
3.  对于每一对可能的 **(a，b)** 来说，总是存在一个这样的**‘x’**，所以这个数可以被 9 整除。
4.  那么可被 **9** 整除的 N 位回文号的[个数可以由以下公式计算:](https://www.geeksforgeeks.org/count-of-n-digit-palindrome-numbers/)

```
Since we have 9 digits to fill at the position a and b.
Therefore, total possible combinations will be:
if N is Odd then, count = pow(9, N/2)
if N is Even then, count = pow(9, N/2 - 1)
as N/2 digits are repeated at the end to get the 
number palindromic.
```

**x 唯一性的证明:**

*   a 和 b 的最小值是 1，因此最小和= 2。
*   a 和 b 的最大值是 9，因此最小和= 18。
*   由于这些数字是回文，因此总和由下式给出:

```
sum = 2*(a+b) + x;
```

*   2*(a+b)的形式为 2，4，6，8，…，36。为了使总和能被 9 整除，x 的值可以是:

```
sum    one of the possible value of x    sum + x
 2                   7                      9
 4                   5                      9
 6                   3                      9
 8                   1                      9
 .                   .                      . 
 .                   .                      . 
 .                   .                      . 
 36                  9                      45
```

以下是步骤:

*   经过以上观察，在任意 **kth** 位置上所有 [N 位回文数字](https://www.geeksforgeeks.org/sum-of-all-n-digit-palindrome-numbers/)的数字之和可被 9 整除，由下式给出:

```
sum at kth position = 45*(number of combinations)/9
```

*   在**【1，N】**上循环，找出可能组合的数量，在当前索引处放置一个数字。
*   用上面提到的公式求出当前数字的所有数字之和。
*   给定所需结果，每次迭代计算的所有总和的总和。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

long long int MOD = 1000000007;

// Function to find a^b efficiently
long long int power(long long int a,
                    long long int b)
{

    // Base Case
    if (b == 0)
        return 1;

    // To store the value of a^b
    long long int temp = power(a, b / 2);

    temp = (temp * temp) % MOD;

    // Multiply temp by a until b is not 0
    if (b % 2 != 0) {
        temp = (temp * a) % MOD;
    }

    // Return the final ans a^b
    return temp;
}

// Function to find sum of all N-digit
// palindromic number divisible by 9
void palindromicSum(int N)
{

    long long int sum = 0, res, ways;

    // Base Case
    if (N == 1) {
        cout << "9" << endl;
        return;
    }

    if (N == 2) {
        cout << "99" << endl;
        return;
    }

    ways = N / 2;

    // If N is even, decrease ways by 1
    if (N % 2 == 0)
        ways--;

    // Find the total number of ways

    res = power(9, ways - 1);

    // Iterate over [1, N] and find the
    // sum at each index
    for (int i = 0; i < N; i++) {
        sum = sum * 10 + 45 * res;
        sum %= MOD;
    }

    // Print the final Sum
    cout << sum << endl;
}

// Driver Code
int main()
{
    int N = 3;
    palindromicSum(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

static int MOD = 1000000007;

// Function to find a^b efficiently
static int power(int a, int b)
{

    // Base Case
    if (b == 0)
        return 1;

    // To store the value of a^b
    int temp = power(a, b / 2);
    temp = (temp * temp) % MOD;

    // Multiply temp by a until b is not 0
    if (b % 2 != 0)
    {
        temp = (temp * a) % MOD;
    }

    // Return the final ans a^b
    return temp;
}

// Function to find sum of all N-digit
// palindromic number divisible by 9
static void palindromicSum(int N)
{
    int sum = 0, res, ways;

    // Base Case
    if (N == 1)
    {
        System.out.print("9" + "\n");
        return;
    }

    if (N == 2)
    {
        System.out.print("99" + "\n");
        return;
    }
    ways = N / 2;

    // If N is even, decrease ways by 1
    if (N % 2 == 0)
        ways--;

    // Find the total number of ways
    res = power(9, ways - 1);

    // Iterate over [1, N] and find the
    // sum at each index
    for (int i = 0; i < N; i++)
    {
        sum = sum * 10 + 45 * res;
        sum %= MOD;
    }

    // Print the final Sum
    System.out.print(sum + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;
    palindromicSum(N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python 3 program for the above approach
MOD = 1000000007

# Function to find a^b efficiently
def power(a, b):

    # Base Case
    if (b == 0):
        return 1

    # To store the value of a^b
    temp = power(a, b // 2)

    temp = (temp * temp) % MOD

    # Multiply temp by a until b is not 0
    if (b % 2 != 0):
        temp = (temp * a) % MOD

    # Return the final ans a^b
    return temp

# Function to find sum of all N-digit
# palindromic number divisible by 9
def palindromicSum(N):

    sum = 0

    # Base Case
    if (N == 1):
        print("9")
        return

    if (N == 2):
        print("99")
        return

    ways = N // 2

    # If N is even, decrease ways by 1
    if (N % 2 == 0):
        ways -= 1

    # Find the total number of ways
    res = power(9, ways - 1)

    # Iterate over [1, N] and find the
    # sum at each index
    for i in range(N):
        sum = sum * 10 + 45 * res
        sum %= MOD

    # Print the final Sum
    print(sum)

# Driver Code
if __name__ == "__main__":

    N = 3
    palindromicSum(N)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int MOD = 1000000007;

// Function to find a^b efficiently
static int power(int a, int b)
{

    // Base Case
    if (b == 0)
        return 1;

    // To store the value of a^b
    int temp = power(a, b / 2);
    temp = (temp * temp) % MOD;

    // Multiply temp by a until b is not 0
    if (b % 2 != 0)
    {
        temp = (temp * a) % MOD;
    }

    // Return the readonly ans a^b
    return temp;
}

// Function to find sum of all N-digit
// palindromic number divisible by 9
static void palindromicSum(int N)
{
    int sum = 0, res, ways;

    // Base Case
    if (N == 1)
    {
        Console.Write("9" + "\n");
        return;
    }

    if (N == 2)
    {
        Console.Write("99" + "\n");
        return;
    }
    ways = N / 2;

    // If N is even, decrease ways by 1
    if (N % 2 == 0)
        ways--;

    // Find the total number of ways
    res = power(9, ways - 1);

    // Iterate over [1, N] and find the
    // sum at each index
    for(int i = 0; i < N; i++)
    {
       sum = sum * 10 + 45 * res;
       sum %= MOD;
    }

    // Print the readonly sum
    Console.Write(sum + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int N = 3;

    palindromicSum(N);
}
}

// This code is contributed by AbhiThakur
```

## java 描述语言

```
<script>

// Javascript program for the above approach

let MOD = 1000000007;

// Function to find a^b efficiently
function power(a, b)
{

    // Base Case
    if (b == 0)
        return 1;

    // To store the value of a^b
    let temp = power(a, b / 2);
    temp = (temp * temp) % MOD;

    // Multiply temp by a until b is not 0
    if (b % 2 != 0)
    {
        temp = (temp * a) % MOD;
    }

    // Return the final ans a^b
    return temp;
}

// Function to find sum of all N-digit
// palindromic number divisible by 9
function palindromicSum(N)
{
    let sum = 0, res, ways;

    // Base Case
    if (N == 1)
    {
        document.write("9" + "\n");
        return;
    }

    if (N == 2)
    {
        document.write("99" + "\n");
        return;
    }
    ways = Math.floor(N / 2);

    // If N is even, decrease ways by 1
    if (N % 2 == 0)
        ways--;

    // Find the total number of ways
    res = power(9, ways - 1);

    // Iterate over [1, N] and find the
    // sum at each index
    for (let i = 0; i < N; i++)
    {
        sum = sum * 10 + 45 * res;
        sum %= MOD;
    }

    // Print the final Sum
    document.write(sum + "<br/>");
}

// Driver Code

    let N = 3;
    palindromicSum(N);

</script>
```

**Output:** 

```
4995
```

***时间复杂度:** O(N)，其中 N 是给定的数。*