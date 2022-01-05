# 所有 N 位回文数字的异或和或

> 原文:[https://www . geesforgeks . org/xor-and-or-of-all-n 位回文数字/](https://www.geeksforgeeks.org/xor-and-or-of-all-n-digit-palindrome-number/)

给定一个整数 **N** 。任务是找出所有 N 位回文数字的异或和或。
**示例**

> **输入:**3
> T3】输出: XOR = 714 且 OR = 1023
> **输入:** 4
> **输出:** XOR = 4606 且 OR = 16383

**进场:**

*   通过

    ```
    starting number = pow(10, n - 1)
    ending number = pow(10, n) - 1
    ```

    求出 N 位回文号的起止号

*   迭代起始数直到结束数，检查该数是否回文。
*   如果该数是回文数，则分别取该数的异或和或。
*   否则继续进行下一次迭代，并在所有迭代后打印异或和或的值。

以下是上述方法的实现:

## C++

```
// C++ program to find the XOR
// and OR of all palindrome numbers
// of N digits
#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// is palindrome or not
bool ispalin(int num)
{
    // Convert the num n to string
    string s = to_string(num);

    int st = 0, ed = s.size() - 1;

    // Iterate over string to
    // check whether it is
    // palindromic or not
    while (st <= ed) {
        if (s[st] != s[ed])
            return false;
        st++;
        ed--;
    }
    return true;
}

// Function to find XOR of all
// N-digits palindrome number
void CalculateXORandOR(int n)
{
    // To store the XOR and OR of all
    // palindromic number
    int CalculateXOR = 0;
    int CalculateOR = 0;

    // Starting N-digit
    // palindromic number
    int start = pow(10, n - 1);

    // Ending N-digit
    // palindromic number
    int end = pow(10, n) - 1;

    // Iterate over starting and
    /// ending number
    for (int i = start; i <= end; i++) {

        // To check if i is
        // palindromic or not
        if (ispalin(i)) {
            CalculateXOR = CalculateXOR ^ i;
            CalculateOR = CalculateOR | i;
        }
    }

    // Print the XOR and OR of all
    // palindromic number
    cout << "XOR = " << CalculateXOR;
    cout << " OR = " << CalculateOR;
}

// Driver Code
int main()
{
    int n = 4;
    CalculateXORandOR(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the XOR
// and OR of all palindrome numbers
// of N digits
class GFG
{

// Function to check if a number
// is palindrome or not
static boolean ispalin(int num)
{
    // Convert the num n to string
    String s = Integer.toString(num);

    int st = 0, ed = s.length() - 1;

    // Iterate over string to
    // check whether it is
    // palindromic or not
    while (st <= ed) {
        if (s.charAt(st) != s.charAt(ed))
            return false;
        st++;
        ed--;
    }
    return true;
}

// Function to find XOR of all
// N-digits palindrome number
static void CalculateXORandOR(int n)
{
    // To store the XOR and OR of all
    // palindromic number
    int CalculateXOR = 0;
    int CalculateOR = 0;

    // Starting N-digit
    // palindromic number
    int start = (int)Math.pow(10, n - 1);

    // Ending N-digit
    // palindromic number
    int end = (int)Math.pow(10, n) - 1;

    // Iterate over starting and
    /// ending number
    for (int i = start; i <= end; i++) {

        // To check if i is
        // palindromic or not
        if (ispalin(i)) {
            CalculateXOR = CalculateXOR ^ i;
            CalculateOR = CalculateOR | i;
        }
    }

    // Print the XOR and OR of all
    // palindromic number
    System.out.print("XOR = " + CalculateXOR);
    System.out.println(" OR = " + CalculateOR);
}

// Driver Code
public static void main (String[] args) 
{
    int n = 4;
    CalculateXORandOR(n);
}

}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find the XOR 
# and OR of all palindrome numbers 
# of N digits 

# Function to check if a number 
# is palindrome or not 
def ispalin(num) : 

    # Convert the num n to string 
    s = str(num); 

    st = 0;
    ed = len(s) - 1; 

    # Iterate over string to 
    # check whether it is 
    # palindromic or not 
    while (st <= ed) :
        if (s[st] != s[ed]) :
            return False; 
        st += 1; 
        ed -= 1; 

    return True; 

# Function to find XOR of all 
# N-digits palindrome number 
def CalculateXORandOR(n) : 

    # To store the XOR and OR of all 
    # palindromic number 
    CalculateXOR = 0; 
    CalculateOR = 0; 

    # Starting N-digit 
    # palindromic number 
    start = 10 ** (n - 1); 

    # Ending N-digit 
    # palindromic number 
    end = (10**n) - 1; 

    # Iterate over starting and 
    # ending number 
    for i in range( start, end + 1) :

        # To check if i is 
        # palindromic or not 
        if (ispalin(i)) :
            CalculateXOR = CalculateXOR ^ i; 
            CalculateOR = CalculateOR | i; 

    # Print the XOR and OR of all 
    # palindromic number 
    print("XOR =", CalculateXOR,end = " "); 
    print("OR = ", CalculateOR); 

# Driver Code 
if __name__ == "__main__" : 

    n = 4;
    CalculateXORandOR(n); 

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find the XOR
// and OR of all palindrome numbers
// of N digits

using System;

class GFG
{

// Function to check if a number
// is palindrome or not
static bool ispalin(int num)
{
    // Convert the num n to string
    string s = num.ToString();

    int st = 0;
    int ed = s.Length - 1;

    // Iterate over string to
    // check whether it is
    // palindromic or not
    while (st <= ed) {
        if (s[st] != s[ed])
            return false;
        st++;
        ed--;
    }
    return true;
}

// Function to find XOR of all
// N-digits palindrome number
static void CalculateXORandOR(int n)
{
    // To store the XOR and OR of all
    // palindromic number
    int CalculateXOR = 0;
    int CalculateOR = 0;

    // Starting N-digit
    // palindromic number
    int start = (int)Math.Pow(10, n - 1);

    // Ending N-digit
    // palindromic number
    int end = (int)Math.Pow(10, n) - 1;

    // Iterate over starting and
    /// ending number
    for (int i = start; i <= end; i++) {

        // To check if i is
        // palindromic or not
        if (ispalin(i)) {
            CalculateXOR = CalculateXOR ^ i;
            CalculateOR = CalculateOR | i;
        }
    }

    // Print the XOR and OR of all
    // palindromic number
    Console.Write("XOR = " + CalculateXOR);
    Console.WriteLine(" OR = " + CalculateOR);
}

// Driver Code
public static void Main (string[] args) 
{
    int n = 4;
    CalculateXORandOR(n);
}

}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program to find the XOR
// and OR of all palindrome numbers
// of N digits

// Function to check if a number
// is palindrome or not
function ispalin(num)
{
    // Convert the num n to string
    let s = num.toString();

    let st = 0, ed = s.length - 1;

    // Iterate over string to
    // check whether it is
    // palindromic or not
    while (st <= ed) {
        if (s[st] != s[ed])
            return false;
        st++;
        ed--;
    }
    return true;
}

// Function to find XOR of all
// N-digits palindrome number
function CalculateXORandOR(n)
{
    // To store the XOR and OR of all
    // palindromic number
    let CalculateXOR = 0;
    let CalculateOR = 0;

    // Starting N-digit
    // palindromic number
    let start = Math.pow(10, n - 1);

    // Ending N-digit
    // palindromic number
    let end = Math.pow(10, n) - 1;

    // Iterate over starting and
    /// ending number
    for (let i = start; i <= end; i++) {

        // To check if i is
        // palindromic or not
        if (ispalin(i)) {
            CalculateXOR = CalculateXOR ^ i;
            CalculateOR = CalculateOR | i;
        }
    }

    // Print the XOR and OR of all
    // palindromic number
    document.write("XOR = " + CalculateXOR);
    document.write(" OR = " + CalculateOR);
}

// Driver Code
    let n = 4;
    CalculateXORandOR(n);

</script>
```

**Output:** 

```
XOR = 4606 OR = 16383
```

**时间复杂度:** O(10 <sup>n</sup> )