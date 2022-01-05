# 计算 K 小于 Y 的所有可能值，使得 GCD(X，Y) = GCD(X+K，Y)

> 原文:[https://www . geeksforgeeks . org/count-所有可能的值-k-小于-y-so-gcdx-y-gcdxk-y/](https://www.geeksforgeeks.org/count-all-possible-values-of-k-less-than-y-such-that-gcdx-y-gcdxk-y/)

给定两个整数 **X** 和 **Y** ，任务是求整数个数， **K** ，使得 [**gcd(X，Y)**](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/) 等于[**gcd(X+K，Y)**](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/) ，其中**0<u><T20】K<Y</u>**。

***例:***

> **输入:** X = 3，Y = 15
> **输出:** 4
> **说明:**K 的所有可能值为{0，3，6，9}，其中 [GCD](https://www.geeksforgeeks.org/stdgcd-c-inbuilt-function-finding-gcd/) (X，Y) = GCD(X + K，Y)。
> 
> **输入:** X = 2，Y = 12
> **输出:** 2
> **说明:**K 的所有可能值都是{0，8}。

**天真法:**解决问题最简单的方法就是迭代**【0，Y–1】**的范围，对于 **i** 的每个值，检查 [**GCD(X + i，Y)**](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/) 是否等于 [**GCD(X，Y)**](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/) 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to calculate
// GCD of two integers
int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to count possible
// values of K
int calculateK(int x, int y)
{
    int count = 0;
    int gcd_xy = gcd(x, y);
    for (int i = 0; i < y; i++) {

        // If required condition
        // is satisfied
        if (gcd(x + i, y) == gcd_xy)

            // Increase count
            count++;
    }

    return count;
}

// Driver Code
int main()
{

    // Given X and y
    int x = 3, y = 15;

    cout << calculateK(x, y) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to calculate
// GCD of two integers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;  
    return gcd(b, a % b);
}

// Function to count possible
// values of K
static int calculateK(int x, int y)
{
    int count = 0;
    int gcd_xy = gcd(x, y);
    for (int i = 0; i < y; i++)
    {

        // If required condition
        // is satisfied
        if (gcd(x + i, y) == gcd_xy)

            // Increase count
            count++;
    }  
    return count;
}

// Driver code
public static void main(String[] args)
{
    // Given X and y
    int x = 3, y = 15; 
    System.out.print(calculateK(x, y));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate
# GCD of two integers
def gcd(a, b):

    if (b == 0):
        return a

    return gcd(b, a % b)

# Function to count possible
# values of K
def calculateK(x, y):

    count = 0
    gcd_xy = gcd(x, y)

    for i in range(y):

        # If required condition
        # is satisfied
        if (gcd(x + i, y) == gcd_xy):

            # Increase count
            count += 1

    return count

# Driver Code
if __name__ == '__main__':

    # Given X and y
    x = 3
    y = 15

    print (calculateK(x, y))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate
// GCD of two integers
static int gcd(int a, int b)
{
    if (b == 0)
        return a; 

    return gcd(b, a % b);
}

// Function to count possible
// values of K
static int calculateK(int x, int y)
{
    int count = 0;
    int gcd_xy = gcd(x, y);

    for(int i = 0; i < y; i++)
    {

        // If required condition
        // is satisfied
        if (gcd(x + i, y) == gcd_xy)

            // Increase count
            count++;
    }  
    return count;
}

// Driver code
public static void Main(String[] args)
{

    // Given X and y
    int x = 3, y = 15; 

    Console.Write(calculateK(x, y));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to calculate
    // GCD of two integers
    function gcd(a , b) {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Function to count possible
    // values of K
    function calculateK(x , y) {
        var count = 0;
        var gcd_xy = gcd(x, y);
        for (i = 0; i < y; i++) {

            // If required condition
            // is satisfied
            if (gcd(x + i, y) == gcd_xy)

                // Increase count
                count++;
        }
        return count;
    }

    // Driver code

        // Given X and y
        var x = 3, y = 15;
        document.write(calculateK(x, y));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(YlogY)*
***辅助空间:** O(1)*

**有效途径:**思路是利用[欧拉全能性函数](https://www.geeksforgeeks.org/eulers-totient-function/)的概念。按照以下步骤解决问题:

*   计算 **X** 和 **Y** 的 [gcd](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/) 并将其存储在变量 **g** 中。
*   用 **Y/g** 初始化变量 **n** 。
*   现在，找到 **n** 的[全能功能](https://www.geeksforgeeks.org/eulers-totient-function/)，这将是所需的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to find the gcd of a and b
int gcd(int a, int b)
{

    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to find the number of Ks
int calculateK(int x, int y)
{

    // Find gcd
    int g = gcd(x, y);
    int n = y / g;
    int res = n;

    // Calculating value of totient
    // function for n
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            res -= (res / i);
            while (n % i == 0)
                n /= i;
        }
    }
    if (n != 1)
        res -= (res / n);
    return res;
}

// Driver Code
int main()
{

    // Given X and Y
    int x = 3, y = 15;

    cout << calculateK(x, y) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find the gcd of a and b
static int gcd(int a, int b)
{

    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to find the number of Ks
static int calculateK(int x, int y)
{

    // Find gcd
    int g = gcd(x, y);
    int n = y / g;
    int res = n;

    // Calculating value of totient
    // function for n
    for (int i = 2; i * i <= n; i++)
    {
        if (n % i == 0)
        {
            res -= (res / i);
            while (n % i == 0)
                n /= i;
        }
    }
    if (n != 1)
        res -= (res / n);
    return res;
}

// Driver Code
public static void main(String[] args)
{

    // Given X and Y
    int x = 3, y = 15;
    System.out.print(calculateK(x, y) +"\n");
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the gcd of a and b
def gcd(a, b):
    if (b == 0):
        return a
    return gcd(b, a % b)

# Function to find the number of Ks
def calculateK(x, y):

    # Find gcd
    g = gcd(x, y)
    n = y // g
    res = n

    # Calculating value of totient
    # function for n
    i = 2
    while i * i <= n:
        if (n % i == 0):
            res -= (res // i)
            while (n % i == 0):
                n //= i
        i += 1
    if (n != 1):
        res -= (res // n)
    return res

# Driver Code
if __name__ == "__main__":

    # Given X and Y
    x = 3
    y = 15

    print(calculateK(x, y))

    # This code is contributed by chitranayal.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the gcd of a and b
static int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to find the number of Ks
static int calculateK(int x, int y)
{

    // Find gcd
    int g = gcd(x, y);
    int n = y / g;
    int res = n;

    // Calculating value of totient
    // function for n
    for(int i = 2; i * i <= n; i++)
    {
        if (n % i == 0)
        {
            res -= (res / i);

            while (n % i == 0)
                n /= i;
        }
    }
    if (n != 1)
        res -= (res / n);

    return res;
}

// Driver Code
public static void Main(String[] args)
{

    // Given X and Y
    int x = 3, y = 15;

    Console.Write(calculateK(x, y) + "\n");
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to find the gcd of a and b
    function gcd(a , b) {

        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Function to find the number of Ks
    function calculateK(x , y) {

        // Find gcd
        var g = gcd(x, y);
        var n = y / g;
        var res = n;

        // Calculating value of totient
        // function for n
        for (i = 2; i * i <= n; i++) {
            if (n % i == 0) {
                res -= (res / i);
                while (n % i == 0)
                    n /= i;
            }
        }
        if (n != 1)
            res -= (res / n);
        return res;
    }

    // Driver Code

        // Given X and Y
        var x = 3, y = 15;
        document.write(calculateK(x, y) + "\n");

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(log(min(X，Y)) + √N)，其中 N 为 Y/gcd(X，Y)。*
***辅助空间:** O(1)*