# 异或斐波那契数列前 N 项之和

> 原文:[https://www . geesforgeks . org/xor-斐波那契数列的前 n 项之和/](https://www.geeksforgeeks.org/sum-of-the-first-n-terms-of-xor-fibonacci-series/)

给定三个正整数 **A** 、 **B** 和 **N** ，其中 **A** 和 **B** 是[异或斐波那契数列](https://www.geeksforgeeks.org/nth-xor-fibonacci-number/)的前两项，任务是求[异或斐波那契数列](https://www.geeksforgeeks.org/nth-xor-fibonacci-number/)的前 **N** 项之和，定义如下:

> **f(n)= f(n–1)^ f(n–2)**
> 
> 其中 **^** 是[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)， **F(0)** 是 **1** ， **F(1)** 是 **2** 。

**示例:**

> **输入:** A = 0，B = 1，N = 3
> **输出:** 2
> **说明:**异或斐波那契数列的前 3 项是 0，1，1。前 3 项的级数之和= 0 + 1 + 1 = 2。
> 
> **输入:** a = 2，b = 5，N = 8
> T3】输出: 35

**天真方法:**最简单的方法是生成异或斐波那契数列直到第一个 **N 项**并计算总和。最后，打印得出的总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum of the
// first N terms of XOR Fibonacci Series
void findSum(int a, int b, int n)
{
    // Base Case
    if (n == 1) {
        cout << a;
        return;
    }

    // Stores the sum of
    // the first N terms
    int s = a + b;

    // Iterate from [0, n-3]
    for (int i = 0; i < n - 2; i++) {

        // Store XOR of last 2 elements
        int x = a xor b;

        // Update sum
        s += x;

        // Update the first element
        a = b;

        // Update the second element
        b = x;
    }

    // Print the final sum
    cout << s;
}

// Driver Code
int main()
{
    int a = 2, b = 5, N = 8;

    // Function Call
    findSum(a, b, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to calculate the sum of the
// first N terms of XOR Fibonacci Series
static void findSum(int a, int b, int n)
{

    // Base Case
    if (n == 1)
    {
        System.out.println(a);
        return;
    }

    // Stores the sum of
    // the first N terms
    int s = a + b;

    // Iterate from [0, n-3]
    for(int i = 0; i < n - 2; i++)
    {

        // Store XOR of last 2 elements
        int x = a ^ b;

        // Update sum
        s += x;

        // Update the first element
        a = b;

        // Update the second element
        b = x;
    }

    // Print the final sum
    System.out.println(s);
}

// Driver Code
public static void main(String[] args)
{
    int a = 2, b = 5, N = 8;

    // Function Call
    findSum(a, b, N);
}
}

// This code is contributed by jana_sayantan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate the sum of the
# first N terms of XOR Fibonacci Series
def findSum(a, b, N):

    # Base case
    if N == 1:
        print(a)
        return

    # Stores the sum of
    # the first N terms
    s = a + b

    # Iterate from [0, n-3]
    for i in range(0, N - 2):

        # Store XOR of last 2 elements
        x = a ^ b

        # Update sum
        s += x

        # Update the first element
        a = b

        # Update the second element
        b = x

    # Print the final sum
    print(s)
    return

# Driver code
if __name__ == '__main__':

    a = 2
    b = 5
    N = 8

    # Function call
    findSum(a, b, N)

# This code is contributed by MuskanKalra1
```

## C#

```
// C# program for the above approach 
using System;
class GFG
{

// Function to calculate the sum of the
// first N terms of XOR Fibonacci Series
static void findSum(int a, int b, int n)
{

    // Base Case
    if (n == 1)
    {
        Console.WriteLine(a);
        return;
    }

    // Stores the sum of
    // the first N terms
    int s = a + b;

    // Iterate from [0, n-3]
    for(int i = 0; i < n - 2; i++)
    {

        // Store XOR of last 2 elements
        int x = a ^ b;

        // Update sum
        s += x;

        // Update the first element
        a = b;

        // Update the second element
        b = x;
    }

    // Print the final sum
    Console.WriteLine(s);
}

// Driver Code
public static void Main()
{
    int a = 2, b = 5, N = 8;

    // Function Call
    findSum(a, b, N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>
// Javascript program for the above approach

    // Function to calculate the sum of the
    // first N terms of XOR Fibonacci Series
    function findSum( a ,b, n)
    {

        // Base Case
        if (n == 1) {
            document.write(a);
            return;
        }

        // Stores the sum of
        // the first N terms
        let s = a + b;

        // Iterate from [0, n-3]
        for ( i = 0; i < n - 2; i++) {

            // Store XOR of last 2 elements
            let x = a ^ b;

            // Update sum
            s += x;

            // Update the first element
            a = b;

            // Update the second element
            b = x;
        }

        // Printt the const sum
        document.write(s);
    }

    // Driver Code

        let a = 2, b = 5, N = 8;

        // Function Call
        findSum(a, b, N);

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
35
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方法:**为了优化上述方法，该想法基于以下观察:

由于 **a ^ a = 0** ,并给出

> *F(0) = a 和 F(1) = b*
> *现在，F(2) = F(0) ^ F(1) = a ^ b*
> *和，f(3)= f(1)^ f(2)= b ^(a ^ b)= a*
> *f(4)= a ^ b ^ a = b*
> f(5)= a ^ b
> t15】f

可以观察到，在每 **3** 个数字后，该序列重复自身。于是，出现了以下三种情况:

1.  **如果 N 能被 3 整除:**级数之和为 **(N / 3) * (a + b + x)** ，其中 **x** 为 **a** 与 **b** 的异或。
2.  **如果 N % 3 剩下余数 1:** 数列的和是 **(N / 3)*(a + b + x) + a** ，其中 **x** 是 **a** 和 **b** 的按位异或。
3.  **如果 N % 3 剩下余数 2:** 数列的和是 **(N / 3)*(a + b + x) + a + b** ，其中 **x** 是 **a** 和 **b** 的按位异或。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of the
// first N terms of XOR Fibonacci Series
void findSum(int a, int b, int n)
{
    // Store the sum of first n terms
    int sum = 0;

    // Store XOR of a and b
    int x = a ^ b;

    // Case 1: If n is divisible by 3
    if (n % 3 == 0) {
        sum = (n / 3) * (a + b + x);
    }

    // Case 2: If n % 3 leaves remainder 1
    else if (n % 3 == 1) {
        sum = (n / 3) * (a + b + x) + a;
    }

    // Case 3: If n % 3 leaves remainder 2
    // on division by 3
    else {
        sum = (n / 3) * (a + b + x) + a + b;
    }

    // Print the final sum
    cout << sum;
}

// Driver Code
int main()
{
    int a = 2, b = 5, N = 8;

    // Function Call
    findSum(a, b, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to calculate sum of the
// first N terms of XOR Fibonacci Series
static void findSum(int a, int b, int n)
{

    // Store the sum of first n terms
    int sum = 0;

    // Store XOR of a and b
    int x = a ^ b;

    // Case 1: If n is divisible by 3
    if (n % 3 == 0)
    {
        sum = (n / 3) * (a + b + x);
    }

    // Case 2: If n % 3 leaves remainder 1
    else if (n % 3 == 1)
    {
        sum = (n / 3) * (a + b + x) + a;
    }

    // Case 3: If n % 3 leaves remainder 2
    // on division by 3
    else
    {
        sum = (n / 3) * (a + b + x) + a + b;
    }

    // Print the final sum
    System.out.print(sum);
}

// Driver Code
public static void main(String[] args)
{
    int a = 2, b = 5, N = 8;

    // Function Call
    findSum(a, b, N);
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate sum of the
# first N terms of XOR Fibonacci Series
def findSum(a, b, N):

    # Store the sum of first n terms
    sum = 0

    # Store xor of a and b
    x = a ^ b

    # Case 1: If n is divisible by 3
    if N % 3 == 0:
        sum = (N // 3) * (a + b + x)

    # Case 2: If n % 3 leaves remainder 1
    elif N % 3 == 1:
        sum = (N // 3) * (a + b + x) + a

    # Case 3: If n % 3 leaves remainder 2
    # on division by 3
    else:
        sum = (N // 3) * (a + b + x) + a + b

    # Print the final sum
    print(sum)
    return

# Driver code
if __name__ == '__main__':

    a = 2
    b = 5
    N = 8

    # Function call
    findSum(a, b, N)

# This code is contributed by MuskanKalra1
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate sum of the
// first N terms of XOR Fibonacci Series
static void findSum(int a, int b, int n)
{

    // Store the sum of first n terms
    int sum = 0;

    // Store XOR of a and b
    int x = a ^ b;

    // Case 1: If n is divisible by 3
    if (n % 3 == 0)
    {
        sum = (n / 3) * (a + b + x);
    }

    // Case 2: If n % 3 leaves remainder 1
    else if (n % 3 == 1)
    {
        sum = (n / 3) * (a + b + x) + a;
    }

    // Case 3: If n % 3 leaves remainder 2
    // on division by 3
    else
    {
        sum = (n / 3) * (a + b + x) + a + b;
    }

    // Print the final sum
    Console.Write(sum);
}

// Driver Code
public static void Main(String[] args)
{
    int a = 2, b = 5, N = 8;

    // Function Call
    findSum(a, b, N);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to calculate sum of the
    // first N terms of XOR Fibonacci Series
    function findSum(a , b , n) {

        // Store the sum of first n terms
        var sum = 0;

        // Store XOR of a and b
        var x = a ^ b;

        // Case 1: If n is divisible by 3
        if (n % 3 == 0) {
            sum = parseInt(n / 3) * (a + b + x);
        }

        // Case 2: If n % 3 leaves remainder 1
        else if (n % 3 == 1) {
            sum =parseInt(n / 3)* (a + b + x) + a;
        }

        // Case 3: If n % 3 leaves remainder 2
        // on division by 3
        else {
            sum = parseInt(n / 3)* (a + b + x) + a + b;
        }

        // Print the final sum
        document.write(sum);
    }

    // Driver Code

        var a = 2, b = 5, N = 8;

        // Function Call
        findSum(a, b, N);

// This code is contributed by aashish1995

</script>
```

**Output**

```
35
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)