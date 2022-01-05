# 矩阵中主对角线元素的和，它们是素数

> 原文:[https://www . geeksforgeeks . org/矩阵中主对角线元素之和是质数/](https://www.geeksforgeeks.org/sum-of-main-diagonal-elements-in-a-matrix-which-are-prime/)

给定一个由 **R** 行和 **C** 列组成的矩阵**[]**。任务是从主对角线找到所有元素的和，这些元素是[质数](https://www.geeksforgeeks.org/prime-numbers/)。
**注:**主对角线是从矩阵左上角向下到右下角的对角线。

**示例:**

> **输入:** R = 3，C = 3，mat[][] = {{1，2，3}，{0，1，2}，{0，4，2}}
> **输出:** 2
> **解释:**
> 主对角线的元素是{1，1，2}，其中只有‘2’是质数。
> 因此，素数为 2 的对角元素之和。
> 
> **输入:** R = 4，C = 4，mat[][] = { {1，2，3，4}，{ 0，7，21，12}，{1，2，3，6}，{ 3，5，2，31}}
> **输出:** 41
> **说明:**
> 主对角线的元素为{ 1，7，3，31}，其中{7，3，31}为质数。
> 因此，素数为 7 + 3 + 31 的对角元素之和= 41。

**天真方法:**

1.  遍历给定的矩阵，检查当前元素是否属于主对角线。
2.  如果元素属于主对角线，并且它是素数，那么将元素的值加到 totalSum。
3.  之后，遍历矩阵打印 totalSum 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function checks whether a number
// is prime or not
bool isPrime(int n)
{
    if (n < 2) {
        return false;
    }

    // Iterate to check primarility of n
    for (int i = 2; i < n; i++) {
        if (n % i == 0)
            return false;
    }

    return true;
}

// Function calculates the sum of
// prime elements of main diagonal
void primeDiagonalElementSum(
    int* mat,
    int r, int c)
{

    // Initialise total sum as 0
    int totalSum = 0;

    // Iterate the given matrix mat[][]
    for (int i = 0; i < r; i++) {

        for (int j = 0; j < c; j++) {

            int temp = *((mat + i * c) + j);

            // If element belongs to main
            // diagonal and is prime
            if ((i == j) && isPrime(temp))
                totalSum += (temp);
        }
    }

    // Print the total sum
    cout << totalSum << endl;
}

// Driver Code
int main()
{
    int R = 4, C = 5;

    // Given Matrix
    int mat[4][5] = { { 1, 2, 3, 4, 2 },
                      { 0, 3, 2, 3, 9 },
                      { 0, 4, 1, 2, 8 },
                      { 1, 2, 3, 6, 6 } };

    // Function Call
    primeDiagonalElementSum((int*)mat, R, C);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function checks whether a number
// is prime or not
static boolean isPrime(int n)
{
    if (n < 2)
    {
        return false;
    }

    // Iterate to check primarility of n
    for(int i = 2; i < n; i++)
    {
       if (n % i == 0)
           return false;
    }

    return true;
}

// Function calculates the sum of
// prime elements of main diagonal
static void primeDiagonalElementSum(int [][]mat,
                                    int r, int c)
{

    // Initialise total sum as 0
    int totalSum = 0;

    // Iterate the given matrix mat[][]
    for(int i = 0; i < r; i++)
    {
       for(int j = 0; j < c; j++)
       {
          int temp = mat[i][j];

          // If element belongs to main
          // diagonal and is prime
          if ((i == j) && isPrime(temp))
              totalSum += (temp);
       }
    }

    // Print the total sum
    System.out.print(totalSum + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int R = 4, C = 5;

    // Given Matrix
    int mat[][] = { { 1, 2, 3, 4, 2 },
                    { 0, 3, 2, 3, 9 },
                    { 0, 4, 1, 2, 8 },
                    { 1, 2, 3, 6, 6 } };

    // Function Call
    primeDiagonalElementSum(mat, R, C);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function checks whether a number
# is prime or not
def isPrime(n):

    if (n < 2):
        return False

    # Iterate to check primarility of n
    for i in range(2, n):
        if (n % i == 0):
            return False

    return True

# Function calculates the sum of
# prime elements of main diagonal
def primeDiagonalElementSum(mat, r, c):

    # Initialise total sum as 0
    totalSum = 0;

    # Iterate the given matrix mat[][]
    for i in range(r):
        for j in range(c):
            temp = mat[i][j]

            # If element belongs to main
            # diagonal and is prime
            if ((i == j) and isPrime(temp)):
                totalSum += (temp)

    # Print the total sum
    print(totalSum)

# Driver code
if __name__=="__main__":

    R = 4
    C = 5

    # Given Matrix
    mat = [ [ 1, 2, 3, 4, 2 ],
            [ 0, 3, 2, 3, 9 ],
            [ 0, 4, 1, 2, 8 ],
            [ 1, 2, 3, 6, 6 ] ]

    # Function call
    primeDiagonalElementSum(mat, R, C)

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function checks whether a number
// is prime or not
public static bool isPrime(int n)
{
    if (n < 2)
    {
        return false;
    }

    // Iterate to check primarility of n
    for(int i = 2; i < n; i++)
    {
       if (n % i == 0)
           return false;
    }
    return true;
}

// Function calculates the sum of
// prime elements of main diagonal
public static void primeDiagonalElementSum(int [,]mat,
                                           int r, int c)
{

    // Initialise total sum as 0
    int totalSum = 0;

    // Iterate the given matrix mat[][]
    for(int i = 0; i < r; i++)
    {
       for(int j = 0; j < c; j++)
       {
          int temp = mat[i, j];

          // If element belongs to main
          // diagonal and is prime
          if ((i == j) && isPrime(temp))
              totalSum += (temp);
       }
    }

    // Print the total sum
    Console.WriteLine(totalSum);
}

// Driver Code
public static void Main(String[] args)
{
    int R = 4, C = 5;

    // Given Matrix
    int [,]mat = { { 1, 2, 3, 4, 2 },
                   { 0, 3, 2, 3, 9 },
                   { 0, 4, 1, 2, 8 },
                   { 1, 2, 3, 6, 6 } };

    // Function Call
    primeDiagonalElementSum(mat, R, C);
}
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>

// Javascript program for
// the above approach

// Function checks whether a number
// is prime or not
function isPrime( n)
{
    if (n < 2)
    {
        return false;
    }

    // Iterate to check primarility of n
    for(let i = 2; i < n; i++)
    {
    if (n % i == 0)
        return false;
    }

    return true;
}

// Function calculates the sum of
// prime elements of main diagonal
function primeDiagonalElementSum(mat,r,c)
{

    // Initialise total sum as 0
    let totalSum = 0;

    // Iterate the given matrix mat[][]
    for(let i = 0; i < r; i++)
    {
    for(let j = 0; j < c; j++)
    {
        let temp = mat[i][j];

        // If element belongs to main
        // diagonal and is prime
        if ((i == j) && isPrime(temp))
            totalSum += (temp);
    }
    }

    // Print the total sum
    document.write(totalSum + "<br>");
}

// Driver Code

    let R = 4, C = 5;

    // Given Matrix
    let mat = [[ 1, 2, 3, 4, 2 ],
               [ 0, 3, 2, 3, 9 ],
                  [ 0, 4, 1, 2, 8 ],
               [ 1, 2, 3, 6, 6 ]];

    // Function Call
    primeDiagonalElementSum(mat, R, C);

// This code is contributed by sravan kumar

</script>
```

**Output:** 

```
3
```

**时间复杂度:** *O(R*C*K)* ，其中 K 是矩阵中最大的元素。
**辅助空间:** *O(1)*

**高效方法:**我们可以通过优化数字的[初级度测试来优化朴素方法。以下是优化初级测试的步骤:](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)

1.  不检查到 **N** ，我们可以检查到 **sqrt(N)** ，因为 **N** 的较大因子必须是已经检查过的较小因子的倍数。
2.  通过观察除了 2 和 3 之外，所有素数都是 **6k 1** 的形式，可以进一步改进算法。这是因为对于某些整数 k 和对于 i = -1、0、1、2、3 或 4，所有整数都可以表示为 **(6k + i)** 。
3.  As 2 除(6k + 0)，(6k + 2)，(6k+4)；和 3 除(6k + 3)。所以更有效的方法是测试 **N** 是否能被 **2** 或 **3** 整除，然后检查表格 **6k 1** 的所有数字。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function checks whether a number
// is prime or not
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function calculates the sum of
// prime elements of main diagonal
void primeDiagonalElementSum(
    int* mat,
    int r, int c)
{

    // Initialise total sum as 0
    int totalSum = 0;

    // Iterate the given matrix mat[][]
    for (int i = 0; i < r; i++) {

        for (int j = 0; j < c; j++) {

            int temp = *((mat + i * c) + j);

            // If element belongs to main
            // diagonal and is prime
            if ((i == j) && isPrime(temp))
                totalSum += (temp);
        }
    }

    // Print the total sum
    cout << totalSum << endl;
}

// Driver Code
int main()
{
    int R = 4, C = 5;

    // Given Matrix
    int mat[4][5] = { { 1, 2, 3, 4, 2 },
                      { 0, 3, 2, 3, 9 },
                      { 0, 4, 1, 2, 8 },
                      { 1, 2, 3, 6, 6 } };

    // Function Call
    primeDiagonalElementSum((int*)mat, R, C);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function checks whether a number
// is prime or not
static boolean isPrime(int n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function calculates the sum of
// prime elements of main diagonal
static void primeDiagonalElementSum(int[][] mat,
                                    int r, int c)
{

    // Initialise total sum as 0
    int totalSum = 0;

    // Iterate the given matrix mat[][]
    for(int i = 0; i < r; i++)
    {
        for(int j = 0; j < c; j++)
        {
            int temp = mat[i][j];

            // If element belongs to main
            // diagonal and is prime
            if ((i == j) && isPrime(temp))
                totalSum += (temp);
        }
    }

    // Print the total sum
    System.out.print(totalSum + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int R = 4, C = 5;

    // Given Matrix
    int mat[][] = { { 1, 2, 3, 4, 2 },
                    { 0, 3, 2, 3, 9 },
                    { 0, 4, 1, 2, 8 },
                    { 1, 2, 3, 6, 6 } };

    // Function call
    primeDiagonalElementSum(mat, R, C);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function checks whether a number
# is prime or not
def isPrime(n):

    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False

    i = 5
    while i * i <= n:
        if (n % i == 0 or n % (i + 2) == 0):
            return False

        i += 6

    return True

# Function calculates the sum of
# prime elements of main diagonal
def primeDiagonalElementSum(mat, r, c):

    # Initialise total sum as 0
    totalSum = 0

    # Iterate the given matrix mat[][]
    for i in range(r):
        for j in range(c):
            temp = mat[i][j]

            # If element belongs to main
            # diagonal and is prime
            if ((i == j) and isPrime(temp)):
                totalSum += (temp)

    # Print the total sum
    print(totalSum)

# Driver Code
R, C = 4, 5

# Given Matrix
mat = [ [ 1, 2, 3, 4, 2 ],
        [ 0, 3, 2, 3, 9 ],
        [ 0, 4, 1, 2, 8 ],
        [ 1, 2, 3, 6, 6 ] ]

# Function Call
primeDiagonalElementSum(mat, R, C)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function checks whether a number
// is prime or not
static bool isPrime(int n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function calculates the sum of
// prime elements of main diagonal
static void primeDiagonalElementSum(int[,] mat,
                                    int r, int c)
{

    // Initialise total sum as 0
    int totalSum = 0;

    // Iterate the given matrix [,]mat
    for(int i = 0; i < r; i++)
    {
        for(int j = 0; j < c; j++)
        {
            int temp = mat[i,j];

            // If element belongs to main
            // diagonal and is prime
            if ((i == j) && isPrime(temp))
                totalSum += (temp);
        }
    }

    // Print the total sum
    Console.Write(totalSum + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int R = 4, C = 5;

    // Given Matrix
    int [,]mat = { { 1, 2, 3, 4, 2 },
                    { 0, 3, 2, 3, 9 },
                    { 0, 4, 1, 2, 8 },
                    { 1, 2, 3, 6, 6 } };

    // Function call
    primeDiagonalElementSum(mat, R, C);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function checks whether a number
// is prime or not
function isPrime(n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (var i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function calculates the sum of
// prime elements of main diagonal
function primeDiagonalElementSum(  mat, r, c)
{

    // Initialise total sum as 0
    var totalSum = 0;

    // Iterate the given matrix mat[][]
    for (var i = 0; i < r; i++) {

        for (var j = 0; j < c; j++) {

            var temp = mat[i][j];

            // If element belongs to main
            // diagonal and is prime
            if ((i == j) && isPrime(temp))
                totalSum += (temp);
        }
    }

    // Print the total sum
    document.write( totalSum );
}

// Driver Code
var R = 4, C = 5;
// Given Matrix
var mat = [ [ 1, 2, 3, 4, 2 ],
                  [ 0, 3, 2, 3, 9 ],
                  [ 0, 4, 1, 2, 8 ],
                  [ 1, 2, 3, 6, 6 ] ];
// Function Call
primeDiagonalElementSum(mat, R, C);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** *O(R*C*sqrt(K))* ，其中 K 是矩阵中最大的元素。
T5【辅助空间: *O(1)*