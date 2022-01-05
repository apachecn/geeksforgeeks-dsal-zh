# 最接近 N 的较小回文数

> 原文:[https://www . geesforgeks . org/small-回文-number-最接近-n/](https://www.geeksforgeeks.org/smaller-palindromic-number-closest-to-n/)

给定一个整数 **N** ，任务是找到比 **N** 更小的最近的[回文号](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)。

**示例:**

> **输入:** N = 4000
> **输出:** 3993
> **说明:**
> 3993 是最接近 N(= 4000)的回文号，也小于 N(= 4000)。因此，3993 是必需的答案。
> 
> **输入:**N = 2889
> T3】输出: 2882

**方法:**按照以下步骤解决问题:

*   减少 **N** 的值，而 **N** 不是[回文号](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)
*   最后打印 **N** 的更新值，发现是一个[回文号](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if
// a number is palindrome or not
bool checkPalindrome(int N)
{
    // Stores reverse of N
    int rev = 0;

    // Stores the value of N
    int temp = N;

    // Calculate reverse of N
    while (N != 0) {

        // Update rev
        rev = rev * 10
              + N % 10;

        // Update N
        N = N / 10;
    }

    // Update N
    N = temp;

    // if N is equal to
    // rev of N
    if (N == rev) {
        return true;
    }

    return false;
}

// Function to find the closest
// smaller palindromic number to N
int closestSmallerPalindrome(int N)
{

    // Calculate closest smaller
    // palindromic number to N
    do {

        // Update N
        N--;
    } while (N >= 0
             && !checkPalindrome(N));

    return N;
}

// Driver Code
int main()
{
    int N = 4000;
    cout << closestSmallerPalindrome(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.util.*;
import java.lang.Math;

class GFG {

    // Function to check whether
    // a number is palindrome or not
    static boolean checkPalindrome(int N)
    {
        // Stores reverse of N
        int rev = 0;

        // Stores the value of N
        int temp = N;

        // Calculate reverse of N
        while (N != 0) {

            // Update rev
            rev = rev * 10
                  + N % 10;

            // Update N
            N = N / 10;
        }

        // Update N
        N = temp;

        // if N is equal to
        // rev of N
        if (N == rev) {
            return true;
        }

        return false;
    }

    // Function to find the closest
    // smaller palindromic number to N
    static int
    closestSmallerPalindrome(int N)
    {

        // Calculate closest smaller
        // palindromic number to N
        do {

            // Update N
            N--;
        } while (N >= 0
                 && !checkPalindrome(N));

        return N;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 4000;
        System.out.println(
            closestSmallerPalindrome(N));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if
# a number is palindrome or not
def checkPalindrome(N):

    # Stores reverse of N
    rev = 0

    # Stores the value of N
    temp = N

    # Calculate reverse of N
    while (N != 0):

        # Update rev
        rev = rev * 10 + N % 10

        # Update N
        N = N // 10

    # Update N
    N = temp

    # If N is equal to
    # rev of N
    if (N == rev):
        return True

    return False

# Function to find the closest
# smaller palindromic number to N
def closestSmallerPalindrome(N):

    # Calculate closest smaller
    # palindromic number to N
    while N >= 0 and not checkPalindrome(N):

        # Update N
        N -= 1

    return N

# Driver Code
if __name__ == '__main__':

    N = 4000

    print(closestSmallerPalindrome(N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to check whether
// a number is palindrome or not
static bool checkPalindrome(int N)
{

    // Stores reverse of N
    int rev = 0;

    // Stores the value of N
    int temp = N;

    // Calculate reverse of N
    while (N != 0)
    {

        // Update rev
        rev = rev * 10 + N % 10;

        // Update N
        N = N / 10;
    }

    // Update N
    N = temp;

    // If N is equal to
    // rev of N
    if (N == rev)
    {
        return true;
    }

    return false;
}

// Function to find the closest
// smaller palindromic number to N
static int closestSmallerPalindrome(int N)
{

    // Calculate closest smaller
    // palindromic number to N
    do
    {

        // Update N
        N--;
    } while (N >= 0 && !checkPalindrome(N));

    return N;
}

// Driver Code
public static void Main()
{
    int N = 4000;

    Console.WriteLine(closestSmallerPalindrome(N));
}
}

// This code is contributed by bgangwar59
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

    // Function to check whether
    // a number is palindrome or not
    function checkPalindrome(N)
    {
        // Stores reverse of N
        let rev = 0;

        // Stores the value of N
        let temp = N;

        // Calculate reverse of N
        while (N != 0) {

            // Update rev
            rev = Math.floor(rev * 10
                  + N % 10);

            // Update N
            N = Math.floor( N / 10);
        }

        // Update N
        N = temp;

        // if N is equal to
        // rev of N
        if (N == rev) {
            return true;
        }

        return false;
    }

    // Function to find the closest
    // smaller palindromic number to N
    function
    closestSmallerPalindrome(N)
    {

        // Calculate closest smaller
        // palindromic number to N
        do {

            // Update N
            N--;
        } while (N >= 0
                 && !checkPalindrome(N));

        return N;
    }

    // Driver Code
    let N = 4000;
    document.write(closestSmallerPalindrome(N));

</script>
```

**Output:** 

```
3993
```

***时间复杂度:**O(N * log<sub>10</sub>N)*
***辅助空间:**O(log<sub>10</sub>N)*