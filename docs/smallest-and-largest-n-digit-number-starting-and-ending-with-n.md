# 以 N 开头和结尾的最小和最大 N 位数

> 原文:[https://www . geesforgeks . org/最小和最大 n 位数-以-n 开头和结尾/](https://www.geeksforgeeks.org/smallest-and-largest-n-digit-number-starting-and-ending-with-n/)

给定一个整数 **N** ，任务是找到以数字 **N** 开始和结束的最小和最大的 **N 位**数字。
**示例:**

> **输入:** N = 3
> **输出:**
> 最小数= 303
> 最大数= 393
> **说明:**
> 303 是以 3 开头和结尾的最小 3 位数。
> 393 是以 3 开头和结尾的最大 3 位数。
> **输入:** N = 1
> **输出:**
> 最小数= 1
> 最大数= 1
> **说明:**
> 1 是以 1 开头和结尾的最小和最大的 1 位数。

**进场:**
我们知道最大最小的 **N 位**号是 **9999…9** ，其中 **9** 重复 **N 次**和 **1000…0** ，其中 **0** 分别重复 **N-1** 次。
现在要得到最小和最大的 **N 位**数字以 **N** 开始和结束，我们需要将最小和最大的 **N 位**数字的第一个和最后一个数字替换为 **N** 。
我们要照顾角箱，即 **N = 1** 时，这里最大和最小的数字都是 **1** 。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find n digit
// largest number starting
// and ending with n
string findNumberL(int n)
{

    // Corner Case when n = 1
    if (n == 1)
        return "1";

    // Result will store the
    // n - 2*length(n) digit
    // largest number
    string result = "";

    // Find the number of
    // digits in number n
    int length = (int)floor(log10(n) + 1);

    // Append 9
    for(int i = 1; i <= n - (2 * length); i++)
    {
        result += '9';
    }

    // To make it largest n digit
    // number starting and ending
    // with n, we just need to
    // append n at start and end
    result = to_string(n) + result + to_string(n);

    // Return the largest number
    return result;
}

// Function to find n digit
// smallest number starting
// and ending with n
string findNumberS(int n)
{

    // Corner Case when n = 1
    if (n == 1)
        return "1";

    // Result will store the
    // n - 2*length(n) digit
    // smallest number
    string result = "";

    // Find the number of
    // digits in number n
    int length = (int)floor(log10(n) + 1);
    for (int i = 1; i <= n - (2 * length); i++)
    {
        result += '0';
    }

    // To make it smallest n digit
    // number starting and ending
    // with n, we just need to
    // append n at start and end
    result = to_string(n) + result + to_string(n);

    // Return the smallest number
    return result;
}

// Driver code
int main()
{

    // Given number
    int N = 3;

    // Function call
    cout << "Smallest Number = " << findNumberS(N) << endl;
    cout << "Largest Number = " << findNumberL(N);
    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to find n digit
    // largest number starting
    // and ending with n
    static String findNumberL(int n)
    {
        // Corner Case when n = 1
        if (n == 1)
            return "1";

        // Result will store the
        // n - 2*length(n) digit
        // largest number
        String result = "";

        // Find the number of
        // digits in number n
        int length
            = (int)Math.floor(
                Math.log10(n) + 1);

        // Append 9
        for (int i = 1;
             i <= n - (2 * length); i++) {
            result += '9';
        }

        // To make it largest n digit
        // number starting and ending
        // with n, we just need to
        // append n at start and end
        result = Integer.toString(n)
                 + result
                 + Integer.toString(n);

        // Return the largest number
        return result;
    }

    // Function to find n digit
    // smallest number starting
    // and ending with n
    static String findNumberS(int n)
    {

        // Corner Case when n = 1
        if (n == 1)
            return "1";

        // Result will store the
        // n - 2*length(n) digit
        // smallest number
        String result = "";

        // Find the number of
        // digits in number n
        int length
            = (int)Math.floor(
                Math.log10(n) + 1);
        for (int i = 1; i <= n - (2 * length); i++) {
            result += '0';
        }

        // To make it smallest n digit
        // number starting and ending
        // with n, we just need to
        // append n at start and end
        result = Integer.toString(n)
                 + result
                 + Integer.toString(n);

        // Return the smallest number
        return result;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Number
        int N = 3;

        // Function Call
        System.out.println(
            "Smallest Number = "
            + findNumberS(N));
        System.out.print(
            "Largest Number = "
            + findNumberL(N));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
import math

# Function to find n digit
# largest number starting
#and ending with n
def findNumberL(n):

    # Corner Case when n = 1
    if (n == 1):
        return "1"

    # Result will store the
    # n - 2*length(n) digit
    # largest number
    result = ""

    # Find the number of
    # digits in number n
    length  = math.floor(math.log10(n) + 1)

    # Append 9
    for i in range(1, n - (2 *
                   length) + 1):
        result += '9'

    # To make it largest n digit
    # number starting and ending
    # with n, we just need to
    # append n at start and end
    result = (str(n) + result +
              str(n))

    # Return the largest number
    return result

# Function to find n digit
# smallest number starting
# and ending with n
def findNumberS(n):

    # Corner Case when n = 1
    if (n == 1):
            return "1"

    # Result will store the
    # n - 2*length(n) digit
    # smallest number
    result = ""

    # Find the number of
    # digits in number n
    length = math.floor(math.log10(n) + 1)

    for i in range(1, n -
                   (2 * length) + 1):
        result += '0'

    # To make it smallest n digit
    # number starting and ending
    # with n, we just need to
    # append n at start and end
    result = (str(n) + result +
              str(n))

    # Return the smallest number
    return result

# Driver Code
if __name__ == "__main__":

    # Given Number
    N = 3

    # Function Call
    print("Smallest Number = " + findNumberS(N))
    print("Largest Number = "+ findNumberL(N))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find n digit
// largest number starting
// and ending with n
static String findNumberL(int n)
{

    // Corner Case when n = 1
    if (n == 1)
        return "1";

    // Result will store the
    // n - 2*length(n) digit
    // largest number
    String result = "";

    // Find the number of
    // digits in number n
    int length = (int)Math.Floor(
                      Math.Log10(n) + 1);

    // Append 9
    for(int i = 1;
            i <= n - (2 * length); i++)
    {
        result += '9';
    }

    // To make it largest n digit
    // number starting and ending
    // with n, we just need to
    // append n at start and end
    result = n.ToString() + result +
             n.ToString();

    // Return the largest number
    return result;
}

// Function to find n digit
// smallest number starting
// and ending with n
static String findNumberS(int n)
{

    // Corner Case when n = 1
    if (n == 1)
        return "1";

    // Result will store the
    // n - 2*length(n) digit
    // smallest number
    String result = "";

    // Find the number of
    // digits in number n
    int length = (int)Math.Floor(
                      Math.Log10(n) + 1);
    for (int i = 1;
             i <= n - (2 * length); i++)
    {
        result += '0';
    }

    // To make it smallest n digit
    // number starting and ending
    // with n, we just need to
    // append n at start and end
    result = n.ToString() + result +
             n.ToString();

    // Return the smallest number
    return result;
}

// Driver Code
public static void Main(String[] args)
{

    // Given number
    int N = 3;

    // Function call
    Console.WriteLine("Smallest Number = " +
                       findNumberS(N));
    Console.Write("Largest Number = " +
                   findNumberL(N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to find n digit
    // largest number starting
    // and ending with n
    function findNumberL(n)
    {
        // Corner Case when n = 1
        if (n == 1)
            return "1";

        // Result will store the
        // n - 2*length(n) digit
        // largest number
        let result = "";

        // Find the number of
        // digits in number n
        let length
            = Math.floor(
                Math.log10(n) + 1);

        // Append 9
        for (let i = 1;
             i <= n - (2 * length); i++) {
            result += '9';
        }

        // To make it largest n digit
        // number starting and ending
        // with n, we just need to
        // append n at start and end
        result = n.toString()
                 + result
                 + n.toString();

        // Return the largest number
        return result;
    }

    // Function to find n digit
    // smallest number starting
    // and ending with n
    function findNumberS(n)
    {

        // Corner Case when n = 1
        if (n == 1)
            return "1";

        // Result will store the
        // n - 2*length(n) digit
        // smallest number
        let result = "";

        // Find the number of
        // digits in number n
        let length
            = Math.floor(
                Math.log10(n) + 1);
        for (let i = 1; i <= n - (2 * length); i++) {
            result += '0';
        }

        // To make it smallest n digit
        // number starting and ending
        // with n, we just need to
        // append n at start and end
        result = n.toString()
                 + result
                 + n.toString();

        // Return the smallest number
        return result;
    }

// Driver Code

     // Given Number
        let N = 3;

        // Function Call
        document.write(
            "Smallest Number = "
            + findNumberS(N) + "<br/>");
        document.write(
            "Largest Number = "
            + findNumberL(N));

</script>
```

**Output:** 

```
Smallest Number = 303
Largest Number = 393
```

**时间复杂度:** *O(N)*