# 使用递归计算一个数的所有因子的程序

> 原文:[https://www . geesforgeks . org/program-to-find-all-factors-of-a-number-use-recursion/](https://www.geeksforgeeks.org/program-to-find-all-factors-of-a-number-using-recursion/)

给定一个数字 **N** ，任务是用递归打印 N 的所有因子。
**例:**

> **输入:** N = 16
> **输出:** 1 2 4 8 16
> **说明:**
> 1、2、4、8、16 是 16 的因子。因子是一个将数完全除的数。
> **输入:** N = 8
> **输出:** 1 2 4 8

**方法:**想法是创建一个接受 2 个参数的函数。该函数从 1 到 N 递归调用，在每次调用中，如果数字是 N 的因子，则打印出来。当数量超过 n 时，递归将停止
下面是上述方法的实现:

## C++

```
// C++ program to find all the factors
// of a number using recursion

#include <bits/stdc++.h>
using namespace std;

// Recursive function to
// print factors of a number
void factors(int n, int i)
{
    // Checking if the number is less than N
    if (i <= n) {
        if (n % i == 0) {
            cout << i << " ";
        }

        // Calling the function recursively
        // for the next number
        factors(n, i + 1);
    }
}

// Driver code
int main()
{
    int N = 16;
    factors(N, 1);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all the factors
// of a number using recursion

class GFG {

    // Recursive function to
    // print factors of a number
    static void factors(int n, int i)
    {

        // Checking if the number is less than N
        if (i <= n) {
            if (n % i == 0) {
                System.out.print(i + " ");
            }

            // Calling the function recursively
            // for the next number
            factors(n, i + 1);
        }
    }
    // Driver code
    public static void main(String args[])
    {
        int N = 16;
        factors(N, 1);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find all the factors
# of a number using recursion

# Recursive function to
# prfactors of a number
def factors(n, i):

    # Checking if the number is less than N
    if (i <= n):
        if (n % i == 0):
            print(i, end = " ");

        # Calling the function recursively
        # for the next number
        factors(n, i + 1);

# Driver code
if __name__ == '__main__':
    N = 16;
    factors(N, 1);

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to find all the factors
// of a number using recursion

using System;

class GFG {

    // Recursive function to
    // print factors of a number
    static void factors(int n, int i)
    {

        // Checking if the number is less than N
        if (i <= n) {
            if (n % i == 0) {
                Console.WriteLine(i + " ");
            }

            // Calling the function recursively
            // for the next number
            factors(n, i + 1);
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 16;
        factors(n, 1);
    }
}
```

## java 描述语言

```
<script>

// Javascript program to find all the factors
// of a number using recursion

// Recursive function to
// print factors of a number
function factors(n, i)
{
    // Checking if the number is less than N
    if (i <= n) {
        if (n % i == 0) {
            document.write(i + " ");
        }

        // Calling the function recursively
        // for the next number
        factors(n, i + 1);
    }
}

// Driver code
var N = 16;
factors(N, 1);

</script>
```

**Output:** 

```
1 2 4 8 16
```

**时间复杂度:** O(N)