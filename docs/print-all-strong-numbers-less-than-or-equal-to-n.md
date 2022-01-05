# 打印所有小于或等于 N 的强数字

> 原文:[https://www . geesforgeks . org/print-all-strong-numbers-小于或等于 n/](https://www.geeksforgeeks.org/print-all-strong-numbers-less-than-or-equal-to-n/)

给定一个数字 **N** ，打印所有小于或等于 **N** 的[强数字](https://www.geeksforgeeks.org/program-to-check-strong-number/)。

> **强数**是一个特殊数，其位数的阶乘之和等于原数。
> 比如:145 是强号。从，1！+ 4!+ 5!= 145.

**示例:**

> **输入:** N = 100
> **输出:** 1 2
> **说明:**
> 只有 1 和 2 是 1 到 100 的强号，因为
> 1！= 1，
> 2！= 2
> 
> **输入:** N = 1000
> **输出:** 1 2 145
> **说明:**
> 只有 1、2、145 是 1 到 1000 的强号，因为
> 1！= 1，
> 2！= 2，
> (1！+ 4!+ 5!) = 145

**方法:**思路是从**【1，N】**迭代，检查[范围内是否有强数](https://www.geeksforgeeks.org/program-to-check-strong-number/)。如果是，则打印相应的号码，否则检查下一个号码。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Store the factorial of all the
// digits from [0, 9]
int factorial[] = { 1, 1, 2, 6, 24, 120,
                    720, 5040, 40320, 362880 };

// Function to return true
// if number is strong or not
bool isStrong(int N)
{

    // Converting N to String so that
    // can easily access all it's digit
    string num = to_string(N);

    // sum will store summation of
    // factorial of all digits
    // of a number N
    int sum = 0;

    for(int i = 0; i < num.length(); i++)
    {
        sum += factorial[num[i] - '0'];
    }

    // Returns true of N is strong number
    return sum == N;
}

// Function to print all
// strong number till N
void printStrongNumbers(int N)
{

    // Iterating from 1 to N
    for(int i = 1; i <= N; i++)
    {

        // Checking if a number is
        // strong then print it
        if (isStrong(i))
        {
            cout << i << " ";
        }
    }
}

// Driver Code
int main()
{

    // Given number
    int N = 1000;

    // Function call
    printStrongNumbers(N);

    return 0;
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Store the factorial of all the
    // digits from [0, 9]
    static int[] factorial = { 1, 1, 2, 6, 24, 120,
                               720, 5040, 40320, 362880 };

    // Function to return true
    // if number is strong or not
    public static boolean isStrong(int N)
    {

        // Converting N to String so that
        // can easily access all it's digit
        String num = Integer.toString(N);

        // sum will store summation of
        // factorial of all digits
        // of a number N
        int sum = 0;

        for (int i = 0;
             i < num.length(); i++) {
            sum += factorial[Integer
                                 .parseInt(num
                                               .charAt(i)
                                           + "")];
        }

        // Returns true of N is strong number
        return sum == N;
    }

    // Function to print all
    // strong number till N
    public static void
    printStrongNumbers(int N)
    {

        // Iterating from 1 to N
        for (int i = 1; i <= N; i++) {

            // Checking if a number is
            // strong then print it
            if (isStrong(i)) {
                System.out.print(i + " ");
            }
        }
    }

    // Driver Code
    public static void
        main(String[] args)
            throws java.lang.Exception
    {
        // Given Number
        int N = 1000;

        // Function Call
        printStrongNumbers(N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Store the factorial of
# all the digits from [0, 9]
factorial = [1, 1, 2, 6, 24, 120,
             720, 5040, 40320, 362880]

# Function to return true
# if number is strong or not
def isStrong(N):

    # Converting N to String
    # so that can easily access
    # all it's digit
    num = str(N)

    # sum will store summation
    # of factorial of all
    # digits of a number N
    sum = 0

    for i in range (len(num)):
        sum += factorial[ord(num[i]) -
                         ord('0')]

    # Returns true of N
    # is strong number
    if sum == N:
       return True
    else:
       return False

# Function to print all
# strong number till N
def printStrongNumbers(N):

    # Iterating from 1 to N
    for i in range (1, N + 1):

        # Checking if a number is
        # strong then print it
        if (isStrong(i)):
            print (i, end = " ")

# Driver Code
if __name__ == "__main__":

    # Given number
    N = 1000

    # Function call
    printStrongNumbers(N)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Store the factorial of all the
// digits from [0, 9]
static int[] factorial = { 1, 1, 2, 6, 24, 120,
                         720, 5040, 40320, 362880 };

// Function to return true
// if number is strong or not
public static bool isStrong(int N)
{

    // Converting N to String so that
    // can easily access all it's digit
    String num = N.ToString();

    // sum will store summation of
    // factorial of all digits
    // of a number N
    int sum = 0;

    for (int i = 0; i < num.Length; i++)
    {
        sum += factorial[int.Parse(num[i] + "")];
    }

    // Returns true of N is strong number
    return sum == N;
}

// Function to print all
// strong number till N
public static void printStrongNumbers(int N)
{

    // Iterating from 1 to N
    for (int i = 1; i <= N; i++)
    {

        // Checking if a number is
        // strong then print it
        if (isStrong(i))
        {
            Console.Write(i + " ");
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    // Given Number
    int N = 1000;

    // Function Call
    printStrongNumbers(N);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Store the factorial of all the
// digits from [0, 9]
let factorial = [ 1, 1, 2, 6, 24, 120,
                    720, 5040, 40320, 362880 ];

// Function to return true
// if number is strong or not
function isStrong(N)
{

    // Converting N to String so that
    // can easily access all it's digit
    let num = N.toString();

    // sum will store summation of
    // factorial of all digits
    // of a number N
    let sum = 0;

    for(let i = 0; i < num.length; i++)
    {
        sum += factorial[num[i] - '0'];
    }

    // Returns true of N is strong number
    return sum == N;
}

// Function to print all
// strong number till N
function printStrongNumbers(N)
{

    // Iterating from 1 to N
    for(let i = 1; i <= N; i++)
    {

        // Checking if a number is
        // strong then print it
        if (isStrong(i))
        {
            document.write(i + " ");
        }
    }
}

// Driver Code

    // Given number
    let N = 1000;

    // Function call
    printStrongNumbers(N);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
1 2 145
```

**时间复杂度:** *O(N)*