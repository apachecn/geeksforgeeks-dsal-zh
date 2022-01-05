# 检查一个数字是否是回文，不使用任何额外的空格|设置 2

> 原文:[https://www . geeksforgeeks . org/check-如果一个数字是回文或不使用任何额外空间集-2/](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome-or-not-without-using-any-extra-space-set-2/)

给定一个数字“n ”,我们的目标是在不使用任何额外空间的情况下找出它是否是回文。我们不能复制一份新的号码。

**示例:**

> **输入:** n = 2332
> **输出:**没错是回文。
> **说明:**
> 原数= 2332
> 倒数= 2332
> 两者相同，故号为回文。
> 
> **输入:** n=1111
> **输出:**没错是回文。
> 
> **输入:**n = 1234
> T3】输出:否不回文。

**其他方法:**其他递归方法和比较位数的方法在本文的[集-1 中讨论。在这里，我们正在讨论其他方法。](https://www.geeksforgeeks.org/check-number-palindrome-not-without-using-extra-space/)

**方法:**这种方法依靠 3 个主要步骤，找出数字中的位数。把数字从中间分成两部分。注意长度为奇数的情况，在这种情况下，我们将不得不使用中间元素两次。检查两个数字中的数字是否相同。按照以下步骤解决问题:

*   将变量 **K** 初始化为数字**n**的长度
*   将变量**和**初始化为 **0。**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，K/2)** ，并执行以下任务:
    *   将 **n%10** 的值放入变量**和**中，并用 **10 除 **n** 。**
*   如果 **K%2** 等于 **1** ，则将 **n%10** 的值放入变量 **ans 中。**
*   执行上述步骤后，如果**和**等于 **n** ，则为苍白色，否则为非苍白色。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find if the number is a
// pallindrome or not
bool isPalindrome(int n)
{
    if (n < 0)
        return false;
    if (n < 10)
        return true;

    // Find the length of the number
    int K = ceil(log(n) / log(10));

    int ans = 0;

    // Partition the number into 2 halves
    for (int i = 0; i < K / 2; i++) {
        ans = ans * 10 + n % 10;
        n = n / 10;
    }
    if (K % 2 == 1)
        ans = ans * 10 + n % 10;

    // Equality Condition
    return (ans == n);
}

// Driver Code
int main()
{
    isPalindrome(1001) ? cout << "Yes, it is Palindrome"
                       : cout << "No, not Palindrome";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find if the number is a
// pallindrome or not
static boolean isPalindrome(int n)
{
    if (n < 0)
        return false;
    if (n < 10)
        return true;

    // Find the length of the number
    int K = (int) Math.ceil(Math.log(n) / Math.log(10));

    int ans = 0;

    // Partition the number into 2 halves
    for (int i = 0; i < K / 2; i++) {
        ans = ans * 10 + n % 10;
        n = n / 10;
    }
    if (K % 2 == 1)
        ans = ans * 10 + n % 10;

    // Equality Condition
    return (ans == n);
}

// Driver Code
public static void main(String[] args)
{
    System.out.print(isPalindrome(1001) ? "Yes, it is Palindrome"
                       : "No, not Palindrome");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python code for the above approach
import math as Math

# Function to find if the number is a
# pallindrome or not
def isPalindrome(n):
    if (n < 0):
        return False
    if (n < 10):
        return True

    # Find the length of the number
    K = Math.ceil(Math.log(n) / Math.log(10))

    ans = 0

    # Partition the number into 2 halves
    for i in range(0, K // 2):
        ans = ans * 10 + n % 10
        n = Math.floor(n / 10)
    if (K % 2 == 1):
        ans = ans * 10 + n % 10

    # Equality Condition
    return (ans == n)

# Driver Code
print("Yes, it is Palindrome") if isPalindrome(
    1001) else print("No, not Palindrome")

# This code is contributed by Saurabh jaiswal
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

  // Function to find if the number is a
  // pallindrome or not
  static bool isPalindrome(int n)
  {
    if (n < 0)
      return false;
    if (n < 10)
      return true;

    // Find the length of the number
    int K = (int)Math.Ceiling(Math.Log(n) / Math.Log(10));

    int ans = 0;

    // Partition the number into 2 halves
    for (int i = 0; i < K / 2; i++)
    {
      ans = ans * 10 + n % 10;
      n = n / 10;
    }
    if (K % 2 == 1)
      ans = ans * 10 + n % 10;

    // Equality Condition
    return (ans == n);
  }

  // Driver Code
  public static void Main()
  {
    Console.Write(isPalindrome(1001) ? "Yes, it is Palindrome" : "No, not Palindrome");
  }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function to find if the number is a
       // pallindrome or not
       function isPalindrome(n) {
           if (n < 0)
               return false;
           if (n < 10)
               return true;

           // Find the length of the number
           let K = Math.ceil(Math.log(n) / Math.log(10));

           let ans = 0;

           // Partition the number into 2 halves
           for (let i = 0; i < K / 2; i++) {
               ans = ans * 10 + n % 10;
               n = Math.floor(n / 10);
           }
           if (K % 2 == 1)
               ans = ans * 10 + n % 10;

           // Equality Condition
           return (ans == n);
       }

       // Driver Code
       isPalindrome(1001) ? document.write("Yes, it is Palindrome")
           : document.write("No, not Palindrome");

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
Yes, it is Palindrome
```

***时间复杂度:**O(K)*其中 *K 为位数*
***辅助方式:** O(1)*