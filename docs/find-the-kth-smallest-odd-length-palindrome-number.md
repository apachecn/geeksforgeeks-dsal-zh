# 求第 k 个最小奇数长度回文数

> 原文:[https://www . geesforgeks . org/find-the-kth-minist-odd-length-回文-number/](https://www.geeksforgeeks.org/find-the-kth-smallest-odd-length-palindrome-number/)

给定一个正整数 **K** ，任务是找到 K <sup>第</sup>个最小的[回文号](https://www.geeksforgeeks.org/python-program-check-string-palindrome-not/)个奇数长度。

**示例:**

> **输入:** K = 5
> **输出:** 5
> **解释:**
> 奇数长度的回文数为{1，2，3，4，5，6，7，…，}。第 5 个<sup>最小回文数是 5。</sup>
> 
> **输入:**K = 10
> T3】输出: 101

**方法:**给定的问题可以基于以下观察来解决:

*   长度为 1 的第一个[回文数字](https://www.geeksforgeeks.org/python-program-check-string-palindrome-not/)是 1、2、3、4、5、6、7、8 和 9。
*   长度为 3 的第一个回文数是 101，这是第十个最小的奇数长度回文数。同样，第 11 <sup>次</sup>、第 12 <sup>次</sup>、第 13 <sup>次</sup>、…、第 99 <sup>次</sup>最小回文号分别为 111、121、131 …、999。
*   因此，除最后一位数字外，第 K <sup>个</sup>个最小奇数长度回文数可以通过连接 **K** 和 **K** 的倒数构成。

从上面的观察来看， **Kth** 最小的奇数长度回文号是通过追加除了最后一个在 **K** 末尾的数字之外的 **K** 的所有数字的倒数给出的。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the Kth smallest
// odd length palindrome
int oddLengthPalindrome(int k)
{

    // Store the original number K
    int palin = k;

    // Removing the last digit of K
    k = k / 10;

    // Generate the palindrome by
    // appending the reverse of K
    // except last digit to itself
    while (k > 0)
    {

        // Find the remainder
        int rev = k % 10;

        // Add the digit to palin
        palin = (palin * 10) + rev;

        // Divide K by 10
        k = k / 10;
    }

    // Return the resultant palindromic
    // number formed
    return palin;
}

// Driver Code
int main()
{
    int k = 504;

    cout << oddLengthPalindrome(k);
}

// This code is contributed by rishavmahato348
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to find the Kth smallest
// odd length palindrome
static int oddLengthPalindrome(int k)
{

    // Store the original number K
    int palin = k;

    // Removing the last digit of K
    k = k / 10;

    // Generate the palindrome by
    // appending the reverse of K
    // except last digit to itself
    while (k > 0)
    { 

        // Find the remainder
        int rev = k % 10;

        // Add the digit to palin
        palin = (palin * 10) + rev;

        // Divide K by 10
        k = k / 10;
    }

    // Return the resultant palindromic
    // number formed
    return palin;
}

// Driver Code
public static void main(String[] args)
{
    int k = 504;

    System.out.println(oddLengthPalindrome(k));
}
}

// This code is contributed by Sudhanshu Bhagat & Govind Choudhary
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the Kth smallest
# odd length palindrome number
def oddLengthPalindrome(K):

    # Store the original number K
    palin = K

    # Removing the last digit of K
    K = K // 10

    # Generate the palindrome by
    # appending the reverse of K
    # except last digit to itself
    while (K > 0):

        # Find the remainder
        rev = K % 10

        # Add the digit to palin
        palin = palin * 10 + rev

        # Divide K by 10
        K = K // 10

    # Return the resultant palindromic
    # number formed
    return palin

# Driver Code
if __name__ == '__main__':

    K = 504
    print(oddLengthPalindrome(K))

#Contributed by Govind Choudhary & Pallav Pushparaj
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the Kth smallest
// palindrome of odd length
static int oddLengthPalindrome(int k)
{

    // Store the original number K
    int palin = k;

    // Removing the last digit of K
    k = k / 10;

    // Generate the palindrome by
    // appending the reverse of K
    // except last digit to itself
    while (k > 0)
    {

        // Find the remainder
        int rev = k % 10;

        // Add the digit to palin
        palin = (palin * 10) + rev;

        // Divide K by 10
        k = k / 10;
    }

    // Return the resultant palindromic
    // number formed
    return palin;
}

// Driver Code
static void Main(string[] args)
{
    int k = 504;

    Console.WriteLine(oddLengthPalindrome(k));
}
}

// This code is contributed by Sudhanshu Bhagat & Govind Choudhary
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the Kth smallest
// odd length palindrome
function oddLengthPalindrome(k)
{

    // Store the original number K
    let palin = k;

    // Removing the last digit of K
    k = Math.floor(k / 10);

    // Generate the palindrome by
    // appending the reverse of K
    // except last digit to itself
    while (k > 0)
    { 

        // Find the remainder
        let rev = k % 10;

        // Add the digit to palin
        palin = (palin * 10) + rev;

        // Divide K by 10
        k = Math.floor(k / 10);
    }

    // Return the resultant palindromic
    // number formed
    return palin;
}

// Driver Code

    let k = 504;

    document.write(oddLengthPalindrome(k));

// This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
50405
```

***时间复杂度:**O(log<sub>10</sub>K)*
***辅助空间:** O(1)*