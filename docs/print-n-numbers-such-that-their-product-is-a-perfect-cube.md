# 打印 N 个数字，这样他们的产品就是一个完美的立方体

> 原文:[https://www . geeksforgeeks . org/print-n-numbers-so-他们的产品是一个完美的立方体/](https://www.geeksforgeeks.org/print-n-numbers-such-that-their-product-is-a-perfect-cube/)

给定一个数字 **N** ，任务是找到不同的 **N** 数字，这样他们的产品就是一个[完美立方体](https://www.geeksforgeeks.org/perfect-cube/)。
**举例:**

> **输入:** N = 3
> **输出:** 1，8，27
> **解释:**
> 输出数的乘积= 1 * 8 * 27 = 216，是 6 的完美立方(6 <sup>3</sup> = 216)
> **输入:** N = 2
> **输出:** 1 8
> **解释:**T20

**方法:**解决方案基于
的事实

> **第一个‘N’个完美立方数的乘积永远是一个完美立方。**

因此，前 N 个自然数的[完美立方体](https://www.geeksforgeeks.org/perfect-cubes-range/)将被打印为输出。
**例如:**

```
For N = 1 => [1]
    Product is 1
    and cube root of 1 is also 1

For N = 2 => [1, 8]
    Product is 8
    and cube root of 8 is 2

For N = 3 => [1, 8, 27]
    Product is 216
    and cube root of 216 is 6

and so on
```

以下是上述方法的实现:

## C++

```
// C++ program to find N numbers such that
// their product is a perfect cube

#include <bits/stdc++.h>
using namespace std;

// Function to find the N numbers such
//that their product is a perfect cube
void findNumbers(int N)
{
    int i = 1;

    // Loop to traverse each
//number from 1 to N
    while (i <= N) {

// Print the cube of i
//as the ith term of the output
        cout << (i * i * i)
             << " ";

        i++;
    }
}

// Driver Code
int main()
{
    int N = 4;

    // Function Call
    findNumbers(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N numbers such that
// their product is a perfect cube
import java.util.*;

class GFG
{

// Function to find the N numbers such
//that their product is a perfect cube
static void findNumbers(int N)
{
    int i = 1;

    // Loop to traverse each
    //number from 1 to N
    while (i <= N) {

        // Print the cube of i
        //as the ith term of the output
        System.out.print( (i * i * i)
            + " ");

        i++;
    }
}

// Driver Code
public static void main (String []args)
{
    int N = 4;

    // Function Call
    findNumbers(N);
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program to find N numbers such that
# their product is a perfect cube

# Function to find the N numbers such
# that their product is a perfect cube
def findNumbers(N):
    i = 1

    # Loop to traverse each
    # number from 1 to N
    while (i <= N):

        # Print the cube of i
        # as the ith term of the output
        print((i * i * i), end=" ")

        i += 1

# Driver Code
if __name__ == '__main__':
    N = 4

    # Function Call
    findNumbers(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find N numbers such that
// their product is a perfect cube
using System;

class GFG
{

// Function to find the N numbers such
//that their product is a perfect cube
static void findNumbers(int N)
{
    int i = 1;

    // Loop to traverse each
    //number from 1 to N
    while (i <= N) {

        // Print the cube of i
        //as the ith term of the output
        Console.Write( (i * i * i)
            + " ");

        i++;
    }
}

// Driver Code
public static void Main (string []args)
{
    int N = 4;

    // Function Call
    findNumbers(N);
}
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>
// JavaScript program to find N numbers such that
// their product is a perfect cube

// Function to find the N numbers such
//that their product is a perfect cube
function findNumbers(N)
{
    let i = 1;

    // Loop to traverse each
    //number from 1 to N
    while (i <= N) {

    // Print the cube of i
    //as the ith term of the output
        document.write((i * i * i)
            + " ");

        i++;
    }
}

// Driver Code

    let N = 4;

    // Function Call
    findNumbers(N);

// This code is contributed by Manoj.
</script>
```

**Output:** 

```
1 8 27 64
```

**业绩分析:**

*   **时间复杂度:**和上面的方法一样，我们正在寻找 N 个数的完美立方，因此需要 **O(N)** 时间。
*   **辅助空间复杂度:**和上面的方法一样，没有使用额外的空间；因此辅助空间的复杂性将是 **O(1)** 。