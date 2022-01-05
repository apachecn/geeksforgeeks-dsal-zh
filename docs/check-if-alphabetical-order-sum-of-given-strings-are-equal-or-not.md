# 检查给定字符串的字母顺序和是否相等

> 原文:[https://www . geesforgeks . org/check-if-按字母顺序-给定字符串的总和-相等或不相等/](https://www.geeksforgeeks.org/check-if-alphabetical-order-sum-of-given-strings-are-equal-or-not/)

给定两个字符串 **s1** 和 **s2** ，任务是检查两个给定字符串的字符的**字母**顺序**和**是否相等或**不是**
**示例:**

> **输入** : s1=“极客”，S2 =“abcdefg”
> **输出**:真
> **说明**:两串字符的字母顺序和为:
> 
> *   s1= 7+5+5+11 = 28
> *   s2= 1+2+3+4+5+6+7 = 28
>     
> 
> **输入** : s1=“坏”，s2=“好”
> **输出**:假

**逼近**:通过简单的**在字符串上迭代**找到字符的**字母顺序和**就可以解决任务。对于每个字符，在结果答案中加上**当前字符+ 1** 的 ASCII 值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if both strings have the
// same alphabetical order sum of characters
bool findTheSum(string s1, string s2)
{
    int sum1 = 0;
    int sum2 = 0;
    int n = s1.length();
    int m = s2.length();

    // Add value of char in sum1
    for (int i = 0; i < n; i++) {
        sum1 += s1[i] - 'a' + 1;
    }

    // Add value of char in sum2
    for (int i = 0; i < m; i++) {
        sum2 += s2[i] - 'a' + 1;
    }

    // Check sum1 are equal to sum2 or not
    if (sum1 == sum2) {
        return true;
    }
    else {
        return false;
    }
}

// Driver Code
int main()
{
    string s1 = "geek";
    string s2 = "abcdefg";
    cout << (findTheSum(s1, s2) ? "True" : "False");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
import java.util.*;
public class GFG {

  // Function to check if both strings have the
  // same alphabetical order sum of characters
  static boolean findTheSum(String s1, String s2)
  {
    int sum1 = 0;
    int sum2 = 0;
    int n = s1.length();
    int m = s2.length();

    // Add value of char in sum1
    for (int i = 0; i < n; i++) {
      sum1 += s1.charAt(i) - 'a' + 1;
    }

    // Add value of char in sum2
    for (int i = 0; i < m; i++) {
      sum2 += s2.charAt(i) - 'a' + 1;
    }

    // Check sum1 are equal to sum2 or not
    if (sum1 == sum2) {
      return true;
    }
    else {
      return false;
    }
  }

  // Driver code
  public static void main(String args[])
  {
    String s1 = "geek";
    String s2 = "abcdefg";
    System.out.println((findTheSum(s1, s2) ? "True" : "False"));

  }
}

// This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# code to implement above approach
using System;
public class GFG {

  // Function to check if both strings have the
  // same alphabetical order sum of characters
  static bool findTheSum(String s1, String s2)
  {
    int sum1 = 0;
    int sum2 = 0;
    int n = s1.Length;
    int m = s2.Length;

    // Add value of char in sum1
    for (int i = 0; i < n; i++) {
      sum1 += s1[i] - 'a' + 1;
    }

    // Add value of char in sum2
    for (int i = 0; i < m; i++) {
      sum2 += s2[i] - 'a' + 1;
    }

    // Check sum1 are equal to sum2 or not
    if (sum1 == sum2) {
      return true;
    }
    else {
      return false;
    }
  }

  // Driver code
  public static void Main(String []args)
  {
    String s1 = "geek";
    String s2 = "abcdefg";
    Console.WriteLine((findTheSum(s1, s2) ? "True" : "False"));
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to check if both strings have the
    // same alphabetical order sum of characters
    const findTheSum = (s1, s2) => {
        let sum1 = 0;
        let sum2 = 0;
        let n = s1.length;
        let m = s2.length;

        // Add value of char in sum1
        for (let i = 0; i < n; i++) {
            sum1 += s1.charCodeAt(i) - 'a'.charCodeAt(0) + 1;
        }

        // Add value of char in sum2
        for (let i = 0; i < m; i++) {
            sum2 += s2.charCodeAt(i) - 'a'.charCodeAt(0) + 1;
        }

        // Check sum1 are equal to sum2 or not
        if (sum1 == sum2) {
            return true;
        }
        else {
            return false;
        }
    }

    // Driver Code

    let s1 = "geek";
    let s2 = "abcdefg";
    if (findTheSum(s1, s2)) document.write("True");
    else document.write("False");

    // This code is contributed by rakeshsahni

</script>
```

**Output:** 

```
True
```

***时间复杂度*****:**O(N)
***辅助空间*** **:** O(1)