# 求 N 个不同整数的和

> 原文:[https://www . geesforgeks . org/find-n-distinct-integers-with-sum-n/](https://www.geeksforgeeks.org/find-n-distinct-integers-with-sum-n/)

给定一个整数 **N** ，任务是找到 **N** 个不同的整数，其和为 **N** 。如果有多个整数组合，请打印其中任何一个。

**示例:**

> **输入:** N = 3
> **输出:** 1，-1，3
> **说明:**
> 将 1 + (-1) + 3 的数相加，和为 3。
> 
> **输入:** N = 4
> **输出:** 1，-1，0，4
> **说明:**
> 将 1 + (-1) + 0 + (4)的数字相加，和为 4。

**方法:**思路是像 **(+x，-x)** 一样打印 **N/2** [对称对](https://www.geeksforgeeks.org/given-an-array-of-pairs-find-all-symmetric-pairs-in-it/)，这样合成的和永远是 **0** 。
现在如果整数 **N 为奇数**，则打印 **N** 连同这些整数组，使所有整数之和等于**N**T17】如果 N 为偶数，则打印 **0 和 N** 连同这些整数组，使所有整数之和等于 **N** 。

下面是上述方法的实现:

## C++

```
// C++ for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print distinct N
// numbers whose sum is N
void findNumbers(int N)
{
    // To store how many symmetric
    // pairs needs to be calculated
    int half = N / 2;

    // For even N we have to print
    // one less symmetric pair
    if (N % 2 == 0) {
        half--;
    }

    // Iterate till [1 n/2] and Print
    // all symmetric pairs(i, -i)
    for (int i = 1; i <= half; i++) {

        // Print 2 symmetric numbers
        cout << (-1) * i
             << ", " << i << ", ";
    }

    // if N is Odd, then print N
    if (N & 1) {
        cout << N << endl;
    }

    // Else print(0, N)
  else {
    cout << 0 << ", "
         << N << endl;
   }
}

// Driver Code
int main()
{
    // Given Sum
    int N = 5;

    // Function Call
    findNumbers(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java for the above approach
class GFG{

// Function to print distinct N
// numbers whose sum is N
public static void findNumbers(int N)
{

    // To store how many symmetric
    // pairs needs to be calculated
    int half = N / 2;

    // For even N we have to print
    // one less symmetric pair
    if (N % 2 == 0)
    {
        half--;
    }

    // Iterate till [1 n/2] and Print
    // all symmetric pairs(i, -i)
    for(int i = 1; i <= half; i++)
    {

       // Print 2 symmetric numbers
       System.out.print((-1) * i + ", " +
                               i + ", ");
    }

    // if N is Odd, then print N
    int check = N & 1;
    if (check != 0)
    {
        System.out.println(N);
    }

    // Else print(0, N)
    else
    {
    System.out.println(0 + ", " + N);
    }
}

// Driver code
public static void main(String[] args)
{

    // Given sum
    int N = 5;

    // Function sall
    findNumbers(N);
}
}

// This code is contributed by divyeshrabadiya07       
```

## 蟒蛇 3

```
# Python3 code for the above approach

# Function to print distinct N
# numbers whose sum is N
def findNumbers(N):

    # To store how many symmetric
    # pairs needs to be calculated
    half = int(N / 2)

    # For even N we have to print
    # one less symmetric pair
    if (N % 2 == 0):
        half = half - 1

    # Iterate till [1 n/2] and Print
    # all symmetric pairs(i, -i)
    for i in range(1, half + 1):

        # Print 2 symmetric numbers
        print((-1) * i, end = ', ')
        print(i, end = ', ')

    # If N is Odd, then print N
    if (N & 1):
        print(N, end = '\n')

    # Else print(0, N)
    else:
        print(0, end = ', ')
        print(N, end = '\n')

# Driver Code
N = 5

# Function Call
findNumbers(N)

# This code is contributed by PratikBasu   
```

## C#

```
// C# for the above approach
using System;
class GFG{

// Function to print distinct N
// numbers whose sum is N
public static void findNumbers(int N)
{

    // To store how many symmetric
    // pairs needs to be calculated
    int half = N / 2;

    // For even N we have to print
    // one less symmetric pair
    if (N % 2 == 0)
    {
        half--;
    }

    // Iterate till [1 n/2] and Print
    // all symmetric pairs(i, -i)
    for(int i = 1; i <= half; i++)
    {

        // Print 2 symmetric numbers
        Console.Write((-1) * i + ", " +
                             i + ", ");
    }

    // if N is Odd, then print N
    int check = N & 1;
    if (check != 0)
    {
        Console.Write(N + "\n");
    }

    // Else print(0, N)
    else
    {
    Console.Write(0 + ", " + N + "\n");
    }
}

// Driver code
public static void Main(string[] args)
{

    // Given sum
    int N = 5;

    // Function sall
    findNumbers(N);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to print distinct N
// numbers whose sum is N
function findNumbers( N)
{
    // To store how many symmetric
    // pairs needs to be calculated
    let half = parseInt(N / 2);

    // For even N we have to print
    // one less symmetric pair
    if (N % 2 == 0) {
        half--;
    }

    // Iterate till [1 n/2] and Print
    // all symmetric pairs(i, -i)
    for (let i = 1; i <= half; i++) {

        // Print 2 symmetric numbers
         document.write( (-1) * i
             + ", " + i + ", ");
    }

    // if N is Odd, then print N
    if (N & 1) {
         document.write( N);
    }

    // Else print(0, N)
  else {
     document.write(  0 + ", "
         + N +"<br/>");
   }
}

// Driver Code

    // Given Sum
    let N = 5;

    // Function Call
    findNumbers(N);

    // This code contributed by aashish1995

</script>
```

**输出:**

```
-1,1,-2,2,5
```