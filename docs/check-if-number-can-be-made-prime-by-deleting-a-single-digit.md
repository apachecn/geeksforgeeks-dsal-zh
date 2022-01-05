# 通过删除单个数字

检查数字是否可以变成质数

> 原文:[https://www . geeksforgeeks . org/check-if-number-be-prime-by-delete-个位数/](https://www.geeksforgeeks.org/check-if-number-can-be-made-prime-by-deleting-a-single-digit/)

给定一个整数 **N** ，任务是检查是否可以通过从 **N** 中删除任意一个数字来使 **N** 成为素数。

**示例:**

> **输入:** N = 610
> **输出:**是
> **说明:**
> 从 610 中删除 0，得到 61，是素数。
> 
> **输入:**N = 68
> T3】输出:否

**进场:**思路是把 **N** 转换成一根弦。现在对字符串的每个数字进行迭代并[从字符串](https://www.geeksforgeeks.org/stdstringerase-in-cpp/)中删除索引 I 处的字符，然后在删除索引 I 处的字符后将字符串转换为整数，现在检查该整数是否为质数，然后返回 true。否则，最后还假。

下面是上述方法的实现:

## C++

```
// C++ implementation to check if a number
// becomes prime by deleting any digit

#include <bits/stdc++.h>
using namespace std;

// Function to check if N is prime
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

// Function to delete character at index i
// from given string str
string deleteIth(string str, int i)
{
    // Deletes character at position 4
    str.erase(str.begin() + i);

    return str;
}

// Function to check if a number
// becomes prime by deleting any digit
bool isPrimePossible(int N)
{
    // Converting the number to string
    string s = to_string(N);

    // length of string
    int l = s.length();

    // number should not be
    // of single digit
    if (l < 2)
        return false;

    // Loop to find all numbers
    // after deleting a single digit
    for (int i = 0; i < l ; i++) {

        // Deleting ith character
        // from the string
        string str = deleteIth(s, i);

        // converting string to int
        int num = stoi(str);

        if (isPrime(num))
            return true;
    }
    return false;
}

// Driver Code
int main()
{
    int N = 610;
    isPrimePossible(N) ? cout << "Yes"
                     : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if a number
// becomes prime by deleting any digit
import java.util.*;
class GFG{

  // Function to check if N is prime
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

    for (int i = 5; i * i <= n; i = i + 6)
      if (n % i == 0 || n % (i + 2) == 0)
        return false;

    return true;
  }

  // Function to delete character at index i
  // from given String str
  static String deleteIth(String str, int i)
  {
    // Deletes character at position 4
    str = str.substring(0, i) +
            str.substring(i + 1);

    return str;
  }

  // Function to check if a number
  // becomes prime by deleting any digit
  static boolean isPrimePossible(int N)
  {
    // Converting the number to String
    String s = String.valueOf(N);

    // length of String
    int l = s.length();

    // number should not be
    // of single digit
    if (l < 2)
      return false;

    // Loop to find all numbers
    // after deleting a single digit
    for (int i = 0; i < l; i++)
    {

      // Deleting ith character
      // from the String
      String str = deleteIth(s, i);

      // converting String to int
      int num = Integer.valueOf(str);

      if (isPrime(num))
        return true;
    }
    return false;
  }

  // Driver Code
  public static void main(String[] args)
  {
    int N = 610;
    if (isPrimePossible(N))
      System.out.print("Yes");
    else
      System.out.print("No");
  }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to check if a number
# becomes prime by deleting any digit

# Function to check if N is prime
#from builtins import range
def isPrime(n):

    # Corner cases
    if (n <= 1):
        return False;
    if (n <= 3):
        return True;

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False;

    for i in range(5, int(n**1/2), 6):
        if (n % i == 0 or n % (i + 2) == 0):
            return False;

    return True;

# Function to delete character at index i
# from given String str
def deleteIth(str, i):

    # Deletes character at position 4
    str = str[0:i] + str[i + 1:];

    return str;

# Function to check if a number
# becomes prime by deleting any digit
def isPrimePossible(N):

    # Converting the number to String
    s = str(N);

    # length of String
    l = len(s);

    # number should not be
    # of single digit
    if (l < 2):
        return False;

    # Loop to find all numbers
    # after deleting a single digit
    for i in range(l):

        # Deleting ith character
        # from the String
        str1 = deleteIth(s, i);

        # converting String to int
        num = int(str1);

        if (isPrime(num)):
            return True;

    return False;

# Driver Code
if __name__ == '__main__':
    N = 610;
    if (isPrimePossible(N)):
        print("Yes");
    else:
        print("No");

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation to check if a number
// becomes prime by deleting any digit
using System;

class GFG{

// Function to check if N is prime
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

// Function to delete character at index i
// from given String str
static String deleteIth(String str, int i)
{

    // Deletes character at position 4
    str = str.Substring(0, i) +
          str.Substring(i + 1);

    return str;
}

// Function to check if a number
// becomes prime by deleting any digit
static bool isPrimePossible(int N)
{

    // Converting the number to String
    String s = String.Join("", N);

    // length of String
    int l = s.Length;

    // number should not be
    // of single digit
    if (l < 2)
        return false;

    // Loop to find all numbers
    // after deleting a single digit
    for(int i = 0; i < l; i++)
    {

        // Deleting ith character
        // from the String
        String str = deleteIth(s, i);

        // converting String to int
        int num = Int32.Parse(str);

        if (isPrime(num))
            return true;
    }
    return false;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 610;

    if (isPrimePossible(N))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// JavaScript implementation to check if a number
// becomes prime by deleting any digit

// Function to check if N is prime
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

    for (let i = 5; i * i <= n; i = i + 6)
      if (n % i == 0 || n % (i + 2) == 0)
        return false;

    return true;
  }

  // Function to delete character at index i
  // from given String str
  function deleteIth(str, i)
  {
    // Deletes character at position 4
    str = str.substr(0, i) +
            str.substr(i + 1);

    return str;
  }

  // Function to check if a number
  // becomes prime by deleting any digit
 function isPrimePossible(N)
  {
    // Converting the number to String
    let s = N.toString();

    // length of String
    let l = s.length;

    // number should not be
    // of single digit
    if (l < 2)
      return false;

    // Loop to find all numbers
    // after deleting a single digit
    for (let i = 0; i < l; i++)
    {

      // Deleting ith character
      // from the String
      let str = deleteIth(s, i);

      // converting String to let
      let num = parseInt(str);

      if (isPrime(num))
        return true;
    }
    return false;
  }

// Driver Code

    let N = 610;
    if (isPrimePossible(N))
      document.write("Yes");
    else
      document.write("No");

</script>
```

**Output**

```
Yes
```

**时间复杂度:***O(D)*
T5】辅助空间: *O(1)*