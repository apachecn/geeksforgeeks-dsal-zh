# 复数的模幂运算

> 原文:[https://www . geeksforgeeks . org/复数的模幂运算/](https://www.geeksforgeeks.org/modular-exponentiation-of-complex-numbers/)

给定四个整数 **A** 、 **B** 、 **K** 、 **M** 。任务是找到 **(A + iB) <sup>K</sup> % M** ，这也是一个复数。 **A + iB** 代表复数。

**示例:**

> **输入:** A = 2，B = 3，K = 4，M = 5
> T3】输出: 1 + i*0
> 
> **输入:** A = 7，B = 3，K = 10，M = 97
> T3】输出: 25 + i*29

**前提:** [模幂](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)

**方法:**
一种有效的方法类似于单个数的模幂运算。这里，我们有两个数字 A，b，而不是一个，所以，将一对整数作为参数传递给函数，而不是一个数字。

以下是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to multiply two complex numbers modulo M
pair<int, int> Multiply (pair<int, int> p, pair<int, int> q,
                                                    int M)
{
    // Multiplication of two complex numbers is 
    // (a + ib)(c + id) = (ac - bd) + i(ad + bc)

    int x = ((p.first * q.first) % M - (p.second * 
                                    q.second) % M + M) % M;

    int y = ((p.first * q.second) % M + (p.second * 
                                          q.first) % M) %M;

    // Return the multiplied value
    return {x, y};
}

// Function to calculate the complex modular exponentiation
pair<int, int> compPow(pair<int, int> complex, int k, int M)
{
    // Here, res is initialised to (1 + i0)
    pair<int, int> res = { 1, 0 }; 

    while (k > 0) 
    {
        // If k is odd
        if (k & 1)
        {
            // Multiply 'complex' with 'res'
            res = Multiply(res, complex, M); 
        }

        // Make complex as complex*complex
        complex = Multiply(complex, complex, M);

        // Make k as k/2
        k = k >> 1; 
    }

    //Return the required answer
    return res;
}

// Driver code
int main()
{

    int A = 7, B = 3, k = 10, M = 97;

    // Function call
    pair<int, int> ans = compPow({A, B}, k, M);

    cout << ans.first << " + i" << ans.second;    

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG 
{
static class pair 
{ 
    int first, second; 
    public pair(int first, int second) 
    { 
        this.first = first; 
        this.second = second; 
    } 
} 

// Function to multiply two complex numbers modulo M
static pair Multiply (pair p, pair q, int M)
{
    // Multiplication of two complex numbers is 
    // (a + ib)(c + id) = (ac - bd) + i(ad + bc)

    int x = ((p.first * q.first) % M -
             (p.second * q.second) % M + M) % M;

    int y = ((p.first * q.second) % M + 
             (p.second * q.first) % M) % M;

    // Return the multiplied value
    return new pair(x, y);
}

// Function to calculate the 
// complex modular exponentiation
static pair compPow(pair complex, int k, int M)
{
    // Here, res is initialised to (1 + i0)
    pair res = new pair(1, 0 ); 

    while (k > 0) 
    {
        // If k is odd
        if (k % 2 == 1)
        {
            // Multiply 'complex' with 'res'
            res = Multiply(res, complex, M); 
        }

        // Make complex as complex*complex
        complex = Multiply(complex, complex, M);

        // Make k as k/2
        k = k >> 1; 
    }

    // Return the required answer
    return res;
}

// Driver code
public static void main(String[] args)
{
    int A = 7, B = 3, k = 10, M = 97;

    // Function call
    pair ans = compPow(new pair(A, B), k, M);

    System.out.println(ans.first + " + i" + 
                       ans.second); 
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to multiply two complex numbers modulo M
def Multiply (p, q, M):

    # Multiplication of two complex numbers is 
    # (a + ib)(c + id) = (ac - bd) + i(ad + bc)
    x = ((p[0] * q[0]) % M - \
         (p[1] * q[1]) % M + M) % M

    y = ((p[0] * q[1]) % M + \
         (p[1] * q[0]) % M) %M

    # Return the multiplied value
    return [x, y]

# Function to calculate the
# complex modular exponentiation
def compPow(complex, k, M):

    # Here, res is initialised to (1 + i0)
    res = [1, 0] 

    while (k > 0):

        # If k is odd
        if (k & 1):

            # Multiply 'complex' with 'res'
            res = Multiply(res, complex, M)

        # Make complex as complex*complex
        complex = Multiply(complex, complex, M)

        # Make k as k/2
        k = k >> 1

    # Return the required answer
    return res

# Driver code
if __name__ == '__main__':
    A = 7
    B = 3
    k = 10
    M = 97

    # Function call
    ans = compPow([A, B], k, M)

    print(ans[0], "+ i", end = "")
    print(ans[1])

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG 
{
public class pair 
{ 
    public int first, second; 
    public pair(int first, int second) 
    { 
        this.first = first; 
        this.second = second; 
    } 
} 

// Function to multiply two complex numbers modulo M
static pair Multiply (pair p, pair q, int M)
{
    // Multiplication of two complex numbers is 
    // (a + ib)(c + id) = (ac - bd) + i(ad + bc)

    int x = ((p.first * q.first) % M -
             (p.second * q.second) % M + M) % M;

    int y = ((p.first * q.second) % M + 
             (p.second * q.first) % M) % M;

    // Return the multiplied value
    return new pair(x, y);
}

// Function to calculate the 
// complex modular exponentiation
static pair compPow(pair complex, int k, int M)
{
    // Here, res is initialised to (1 + i0)
    pair res = new pair(1, 0 ); 

    while (k > 0) 
    {
        // If k is odd
        if (k % 2 == 1)
        {
            // Multiply 'complex' with 'res'
            res = Multiply(res, complex, M); 
        }

        // Make complex as complex*complex
        complex = Multiply(complex, complex, M);

        // Make k as k/2
        k = k >> 1; 
    }

    // Return the required answer
    return res;
}

// Driver code
public static void Main(String[] args)
{
    int A = 7, B = 3, k = 10, M = 97;

    // Function call
    pair ans = compPow(new pair(A, B), k, M);

    Console.WriteLine(ans.first + " + i" + 
                      ans.second); 
}
}

// This code is contributed by 29AjayKumar
```

**Output:**

```
25 + i29

```

**时间复杂度:** O(log k)。