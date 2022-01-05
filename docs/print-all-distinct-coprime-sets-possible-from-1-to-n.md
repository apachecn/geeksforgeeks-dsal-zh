# 打印从 1 到 N 的所有可能的不同互质集

> 原文:[https://www . geesforgeks . org/print-all-distinct-互素-set-may-from-1-n/](https://www.geeksforgeeks.org/print-all-distinct-coprime-sets-possible-from-1-to-n/)

给定一个整数 **N** ，任务是找到所有不同的同素集合，直到给定的整数 **N** ，这样一个元素不会出现在多于一个集合中。

> 如果 [**GCD(a，b) = 1**](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/) **，则一个数字 **a** 据说是[与 **b** 共同质数](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)。**

**例:**

> **输入:** N = 5
> **输出:** (1，2) (3，4，5)
> **输入:** N = 6
> **输出:** (1，2) (3，4) (5，6)

**进场:**

*   为了解决上面提到的问题，我们可以观察到，如果 N 小于 4，那么所有的元素都已经是同素的，直到 N，因为它们的 GCD 总是为 1。因此，对于 N = [1，3]，可能的互质集分别是(1)、(1，2)和(1，2，3)。
*   对于 N > 3 的所有值，有两种可能的情况:
    *   如果 **N** 的值是**偶数**，那么每个集合将包含 2 个相邻元素，直到 **N** 本身，因为相邻的数字总是彼此同素的。
    *   如果整数 N 的值为**奇数**，那么除了最后一个集合将包含最后三个元素之外，每个集合将包含 2 个相邻元素。

以下是上述方法的实现:

## C++

```
// C++ implementation to print
// all distinct co-prime sets
// possible for numbers from 1 to N

#include <bits/stdc++.h>
using namespace std;

// Function to print all coprime sets
void coPrimeSet(int n)
{

    int firstadj, secadj;

    // Check if n is less than 4
    // then simply print all values till n
    if (n < 4) {
        cout << "( ";
        for (int i = 1; i <= n; i++)
            cout << i << ", ";

        cout << ")\n";
    }

    // For all the values of n > 3
    else {

        // Check if n is even
        // then every set will contain
        // 2 adjacent elements up-to n
        if (n % 2 == 0) {
            for (int i = 0; i < n / 2; i++) {
                firstadj = 2 * i + 1;
                secadj = 2 * i + 2;

                cout << "(" << firstadj
                     << ", " << secadj << ")\n";
            }
        }
        else {

            // if n is odd then every set will
            // contain 2 adjacent element
            // except the last set which
            // will have last three elements
            for (int i = 0; i < n / 2 - 1; i++)

            {
                firstadj = 2 * i + 1;
                secadj = 2 * i + 2;

                cout << "(" << firstadj
                     << ", " << secadj << ")\n";
            }

            // Last element for odd case
            cout << "(" << n - 2 << ", " << n - 1
                 << ", " << n << ")\n";
        }
    }
}

// Driver Code
int main()
{
    int n = 5;

    coPrimeSet(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print
// all distinct co-prime sets
// possible for numbers from 1 to N
import java.util.*;

class GFG{

// Function to print all co-prime sets
static void coPrimeSet(int n)
{
    int firstadj, secadj;

    // Check if n is less than 4 then
    // simply print all values till n
    if (n < 4)
    {
        System.out.print("( ");
        for(int i = 1; i <= n; i++)
           System.out.print(i + ", ");

        System.out.print(")\n");
    }

    // For all the values of n > 3
    else
    {

        // Check if n is even then
        // every set will contain
        // 2 adjacent elements up-to n
        if (n % 2 == 0)
        {
            for(int i = 0; i < n / 2; i++)
            {
               firstadj = 2 * i + 1;
                 secadj = 2 * i + 2;

               System.out.print("(" + firstadj +
                               ", " + secadj + ")\n");
            }
        }
        else
        {

            // If n is odd then every set will
            // contain 2 adjacent element
            // except the last set which
            // will have last three elements
            for(int i = 0; i < n / 2 - 1; i++)
            {
               firstadj = 2 * i + 1;
                 secadj = 2 * i + 2;

               System.out.print("(" + firstadj +
                               ", " + secadj + ")\n");
            }

            // Last element for odd case
            System.out.print("(" + (n - 2) +
                            ", " +  ( n - 1) +
                            ", " + n + ")\n");
        }
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 5;

    coPrimeSet(n);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to print
# all distinct co-prime sets
# possible for numbers from 1 to N

# Function to prall co-prime sets
def coPrimeSet(n):

    firstadj = 0;
    secadj = 0;

    # Check if n is less than 4 then
    # simply prall values till n
    if (n < 4):
        print("( ");

        for i in range(1, n + 1):
            print(i + ", ");
        print(")");

    # For all the values of n > 3
    else:

        # Check if n is even then
        # every set will contain
        # 2 adjacent elements up-to n
        if (n % 2 == 0):

            for i in range(0, n /2 ):
                firstadj = 2 * i + 1;
                secadj = 2 * i + 2;

                print("(", firstadj, ", ",
                           secadj, ")");
        else:

            # If n is odd then every set will
            # contain 2 adjacent element
            # except the last set which
            # will have last three elements
            for i in range(0, int(n / 2) - 1):
                firstadj = 2 * i + 1;
                secadj = 2 * i + 2;

                print("(", firstadj, ", ",
                           secadj, ")");

            # Last element for odd case
            print("(", (n - 2), ", ",
                       (n - 1), ", ", n, ")");

# Driver code
if __name__ == '__main__':

    n = 5;

    coPrimeSet(n);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation to print
// all distinct co-prime sets
// possible for numbers from 1 to N
using System;

class GFG{

// Function to print all co-prime sets
static void coPrimeSet(int n)
{
    int firstadj, secadj;

    // Check if n is less than 4 then
    // simply print all values till n
    if (n < 4)
    {
        Console.Write("( ");
        for(int i = 1; i <= n; i++)
           Console.Write(i + ", ");

        Console.Write(")\n");
    }

    // For all the values of n > 3
    else
    {

        // Check if n is even then
        // every set will contain
        // 2 adjacent elements up-to n
        if (n % 2 == 0)
        {
            for(int i = 0; i < n / 2; i++)
            {
               firstadj = 2 * i + 1;
                 secadj = 2 * i + 2;

               Console.Write("(" + firstadj +
                            ", " + secadj + ")\n");
            }
        }
        else
        {

            // If n is odd then every set will
            // contain 2 adjacent element
            // except the last set which
            // will have last three elements
            for(int i = 0; i < n / 2 - 1; i++)
            {
               firstadj = 2 * i + 1;
                 secadj = 2 * i + 2;

               Console.Write("(" + firstadj +
                            ", " + secadj + ")\n");
            }

            // Last element for odd case
            Console.Write("(" + (n - 2) +
                         ", " + (n - 1) +
                           ", " + n + ")\n");
        }
    }
}

// Driver code
public static void Main()
{
    int n = 5;

    coPrimeSet(n);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation to print
// all distinct co-prime sets
// possible for numbers from 1 to N

// Function to print all co-prime sets
function coPrimeSet(n)
{
    let firstadj, secadj;

    // Check if n is less than 4 then
    // simply print all values till n
    if (n < 4)
    {
         document.write("( ");
        for(let i = 1; i <= n; i++)
           document.write(i + ", ");

       document.write(")" + "<br/>");
    }

    // For all the values of n > 3
    else
    {

        // Check if n is even then
        // every set will contain
        // 2 adjacent elements up-to n
        if (n % 2 == 0)
        {
            for(let i = 0; i < Math.floor(n / 2); i++)
            {
               firstadj = 2 * i + 1;
                 secadj = 2 * i + 2;

               document.write("(" + firstadj +
                         ", " + secadj + ")"+ "<br/>");
            }
        }
        else
        {

            // If n is odd then every set will
            // contain 2 adjacent element
            // except the last set which
            // will have last three elements
            for(let i = 0; i < Math.floor(n / 2) - 1; i++)
            {
               firstadj = 2 * i + 1;
                 secadj = 2 * i + 2;

               document.write("(" + firstadj +
                               ", " + secadj + ")" + "<br/>");
            }

            // Last element for odd case
            document.write("(" + (n - 2) +
                            ", " +  ( n - 1) +
                            ", " + n + ")" + "<br/>");
        }
    }
}

  // Driver Code

    let n = 5;

    coPrimeSet(n);

</script>
```

**Output:** 

```
(1, 2)
(3, 4, 5)
```