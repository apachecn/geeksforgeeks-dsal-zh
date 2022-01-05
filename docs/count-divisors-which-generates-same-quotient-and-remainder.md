# 计算产生相同商和余数的除数

> 原文:[https://www . geeksforgeeks . org/count-divisions-产生相同商和余数/](https://www.geeksforgeeks.org/count-divisors-which-generates-same-quotient-and-remainder/)

给定一个正整数 **N** ，任务是找出所有数字 **M** 的计数，使得当数字 **N** 除以 **M** 时，商等于其余数，即 **(⌊N/M⌋ = N mod M)** ，其中 **⌊ ⌋** 表示给定数字的楼层值。

**示例:**

> **输入:** N = 8
> **输出:** 2
> **说明:**当 8 除以 3 和 7 时，返回相同的商和余数。
> 8 / 3 = 8 % 3，8 / 7 = 8 % 7。所以，要求的答案是 2。
> 
> **输入:**N = 100000000000
> T3】输出: 84

**天真法:**最简单的方法是基于这样一个事实: **M** 不能大于 **N** 至于大于 **N** 的任何数，商都为零。而其与 **N** 的模永远是 **N** 。因此，迭代从 **1 到 N** 的所有数字，并计算所有满足给定条件的数字。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**有效方法:**最佳想法基于以下观察:

> 如果 **(⌊N/M⌋ = N mod M)** ，那么 **M + 1** 必须是 **N** 的除数。

**观察证明:**

> 如果 **⌊N/M⌋ = N mod M** ，那么让 **N / M** 等于 **K** 。
> 因此， **N** 必须等于 **K * M + K** ，因为 **K** 是商，也是余数。
> **N = K * M+K**
> **N = K *(M+1)**
> 因此，要让 **M** 出现在我们的答案集中， **M + 1** 必须是 **N** 的除数。
> 注意 **M + 1** 必须是 **N** 的除数是 **⌊N/M⌋ = N mod M** 的必要条件但不是充分条件。

按照以下步骤解决问题:

*   找到 N 的所有[因子，并将其存储在数组中。这可以用 O(√ N)复杂度来计算。](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)
*   通过[迭代数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)检查所有除数，如果除数减 1 满足给定条件 **⌊N / M⌋ = N mod M** ，则增加计数。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the
// count of numbers such that it
// gives same quotient and remainder
void countDivisors(long long int n)
{

    int count = 0;

    // Stores divisor of number N.
    vector<long long int> divisor;

    // Iterate through numbers from 2
    // to sqrt(N) and store divisors of N
    for (int i = 2; i <= sqrt(n); i++) {

        if (n % i == 0) {

            if (n / i == i)
                divisor.push_back(i);

            else {

                divisor.push_back(i);
                divisor.push_back(n / i);
            }
        }
    }

    // As N is also divisor of itself
    divisor.push_back(n);

    // Iterate through divisors
    for (auto x : divisor) {
        x -= 1;

        // Checking whether x satisfies the
        // required condition
        if ((n / x) == (n % x))
            count++;
    }

    // Print the count
    cout << count;
}

// Driver Code
int main()
{
    // Given N
    long long int N = 1000000000000;

    // Function Call
    countDivisors(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
class GFG {

    // Function to calculate the
    // count of numbers such that it
    // gives same quotient and remainder
    static void countDivisors(int n)
    {   
        int count = 0;
        int j = 0;

        // Stores divisor of number N.
        int divisor[] =  new int[n];

        // Iterate through numbers from 2
        // to sqrt(N) and store divisors of N
        for (int i = 2; i <= Math.sqrt(n); i++) {   
            if (n % i == 0) {
                if (n / i == i){
                    divisor[j] = i;
                     j += 1;
                }
                else {
                    divisor[j] = i;
                    divisor[j + 1] = n / i;                   
                    j += 2;
                }
            }
        }

        // As N is also divisor of itself
        divisor[j] = n;

        // Iterate through divisors
        for (int i = 0; i <= j; i++)
        {
            int x = divisor[i];
            x -= 1;

            // Checking whether x satisfies the
            // required condition
            if ((n / x) == (n % x))
                count++;
        }

        // Print the count
        System.out.print(count);
    }

    // Driver Code
    public static void main (String[] args)
    {

        // Given N
        int N = 10000000;

        // Function Call
        countDivisors(N);
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program of the above approach
from math import floor, sqrt

# Function to calculate the
# count of numbers such that it
# gives same quotient and remainder
def countDivisors(n):

    count = 0

    # Stores divisor of number N.
    divisor = []

    # Iterate through numbers from 2
    # to sqrt(N) and store divisors of N
    for i in range(2, floor(sqrt(n))):
        if (n % i == 0):
            if (n // i == i):
                divisor.append(i)
            else:
                divisor.append(i)
                divisor.append(n // i)

    # As N is also divisor of itself
    divisor.append(n)

    # Iterate through divisors
    for x in divisor:
        x -= 1

        # Checking whether x satisfies the
        # required condition
        if ((n // x) == (n % x)):
            count += 1

    # Print the count
    print(count)

# Driver Code
if __name__ == '__main__':

    # Given N
    N = 1000000000000

    # Function Call
    countDivisors(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program of the above approach
using System;
class GFG {

    // Function to calculate the
    // count of numbers such that it
    // gives same quotient and remainder
    static void countDivisors(int n)
    {   
        int count = 0;
        int j = 0;

        // Stores divisor of number N.
        int []divisor =  new int[n];

        // Iterate through numbers from 2
        // to sqrt(N) and store divisors of N
        for (int i = 2; i <= Math.Sqrt(n); i++) {   
            if (n % i == 0) {
                if (n / i == i){
                    divisor[j] = i;
                     j += 1;
                }
                else {
                    divisor[j] = i;
                    divisor[j + 1] = n / i;                   
                    j += 2;
                }
            }
        }

        // As N is also divisor of itself
        divisor[j] = n;

        // Iterate through divisors
        for (int i = 0; i <= j; i++)
        {
            int x = divisor[i];
            x -= 1;

            // Checking whether x satisfies the
            // required condition
            if ((n / x) == (n % x))
                count++;
        }

        // Print the count
        Console.Write(count);
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // Given N
        int N = 10000000;

        // Function Call
        countDivisors(N);
    }
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program of the above approach   

// Function to calculate the
    // count of numbers such that it
    // gives same quotient and remainder
    function countDivisors(n)
    {
        var count = 0;
        var j = 0;

        // Stores divisor of number N.
        var divisor = Array(n).fill(0);

        // Iterate through numbers from 2
        // to sqrt(N) and store divisors of N
        for (var i = 2; i <= Math.sqrt(n); i++)
        {
            if (n % i == 0) {
                if (parseInt(n / i) == i)
                {
                    divisor[j] = i;
                    j += 1;
                } else {
                    divisor[j] = i;
                    divisor[j + 1] = parseInt(n / i);
                    j += 2;
                }
            }
        }

        // As N is also divisor of itself
        divisor[j] = n;

        // Iterate through divisors
        for (var i = 0; i <= j; i++) {
            var x = divisor[i];
            x -= 1;

            // Checking whether x satisfies the
            // required condition
            if (parseInt(n / x) == parseInt(n % x))
                count++;
        }

        // Print the count
        document.write(count);
    }

    // Driver Code

        // Given N
        var N = 10000000;

        // Function Call
        countDivisors(N);

// This code contributed by aashish1995

</script>
```

**Output:** 

```
84
```

***时间复杂度:** O(sqrt(N))*
***辅助空间:** O(sqrt(N))*