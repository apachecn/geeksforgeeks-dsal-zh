# 拆分二进制字符串，使左右子字符串中 0 和 1 的数量最大

> 原文:[https://www . geesforgeks . org/split-a-binary-string-so-count-of-0s-in-left-and-right-substrings-is-maximum/](https://www.geeksforgeeks.org/split-a-binary-string-such-that-count-of-0s-and-1s-in-left-and-right-substrings-is-maximum/)

给定长度为 **N** 的二进制[字符串](https://www.geeksforgeeks.org/string-data-structure/)、**字符串**，任务是通过将[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)拆分为两个非空子字符串，找到左侧[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)的 0 计数和右侧子字符串的 1 计数的最大和。

**示例:**

> **输入:** str = "000111"
> **输出:** 6
> **解释:**
> 将二进制字符串拆分为“000”和“111”。
> 字符串左子串的 0s 计数= 3
> 字符串右子串的 1s 计数= 3
> 因此，字符串左子串的 0s 计数和字符串右子串的 1s 计数之和= 3 + 3 = 6。
> 
> **输入:** S = "1111"
> **输出:** 3
> **解释:**
> 将二进制字符串拆分为“1”和“111”。
> 字符串左子串的 0s 计数= 0
> 字符串右子串的 1s 计数= 3
> 因此，字符串左子串的 0s 计数和字符串右子串的 1s 计数之和= 0 + 3 = 3。

**方法:**按照以下步骤解决问题:

1.  初始化一个变量，比如说 **res** ，来存储左子串中 **0** 的计数和右子串中 **1** 的计数的最大和。
2.  初始化一个变量，比如说 **cntOne** ，在给定的二进制字符串中存储 **1** 的计数。
3.  [遍历二进制字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，对于每个字符，检查是否是**‘1’**。如果发现为真，则将 **cntOne** 的值增加 **1** 。
4.  初始化两个变量，说**零**和**一**，存储 **0** s 的计数和 **1** s 的计数，直到 **i <sup>th</sup>** 索引。
5.  [遍历二进制字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并更新 **res = max(res，cntOne–1+0)**的值。
6.  最后，打印 **res** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of count  of
// 0s in the left substring and count of 1s in
// the right substring by splitting the string
int maxSumbySplittingstring(string str, int N)
{

    // Stores count of 1s
    // the in binary string
    int cntOne = 0;

    // Traverse the binary string
    for (int i = 0; i < N; i++) {

        // If current character is '1'
        if (str[i] == '1') {

            // Update cntOne
            cntOne++;
        }
    }

    // Stores count of 0s
    int zero = 0;

    // Stores count of 1s
    int one = 0;

    // Stores maximum sum of count of
    // 0s and 1s by splitting the string
    int res = 0;

    // Traverse the binary string
    for (int i = 0; i < N - 1; i++) {

        // If current character
        // is '0'
        if (str[i] == '0') {

            // Update zero
            zero++;
        }

        // If current character is '1'
        else {

            // Update one
            one++;
        }

        // Update res
        res = max(res, zero + cntOne - one);
    }

    return res;
}

// Driver Code
int main()
{
    string str = "00111";
    int N = str.length();

    cout << maxSumbySplittingstring(str, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

  // Function to find the maximum sum of count  of
  // 0s in the left subString and count of 1s in
  // the right subString by splitting the String
  static int maxSumbySplittingString(String str, int N)
  {

    // Stores count of 1s
    // the in binary String
    int cntOne = 0;

    // Traverse the binary String
    for (int i = 0; i < N; i++)
    {

      // If current character is '1'
      if (str.charAt(i) == '1')
      {

        // Update cntOne
        cntOne++;
      }
    }

    // Stores count of 0s
    int zero = 0;

    // Stores count of 1s
    int one = 0;

    // Stores maximum sum of count of
    // 0s and 1s by splitting the String
    int res = 0;

    // Traverse the binary String
    for (int i = 0; i < N - 1; i++) {

      // If current character
      // is '0'
      if (str.charAt(i) == '0') {

        // Update zero
        zero++;
      }

      // If current character is '1'
      else {

        // Update one
        one++;
      }

      // Update res
      res = Math.max(res, zero + cntOne - one);
    }
    return res;
  }

  // Driver Code
  public static void main(String[] args)
  {
    String str = "00111";
    int N = str.length();

    System.out.print(maxSumbySplittingString(str, N));
  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum sum of count  of
# 0s in the left suband count of 1s in
# the right subby splitting the string
def maxSumbySplittingstring(str, N):

    # Stores count of 1s
    # the in binary string
    cntOne = 0

    # Traverse the binary string
    for i in range(N):

        # If current character is '1'
        if (str[i] == '1'):

            # Update cntOne
            cntOne += 1

    # Stores count of 0s
    zero = 0

    # Stores count of 1s
    one = 0

    # Stores maximum sum of count of
    # 0s and 1s by splitting the string
    res = 0

    # Traverse the binary string
    for i in range(N - 1):

        # If current character
        # is '0'
        if (str[i] == '0'):

            # Update zero
            zero += 1

        # If current character is '1'
        else:

            # Update one
            one += 1

        # Update res
        res = max(res, zero + cntOne - one)
    return res

# Driver Code
if __name__ == '__main__':
    str = "00111"
    N = len(str)

    print (maxSumbySplittingstring(str, N))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program to implement
// the above approach
using System;
public class GFG
{

  // Function to find the maximum sum of count  of
  // 0s in the left subString and count of 1s in
  // the right subString by splitting the String
  static int maxSumbySplittingString(String str, int N)
  {

    // Stores count of 1s
    // the in binary String
    int cntOne = 0;

    // Traverse the binary String
    for (int i = 0; i < N; i++)
    {

      // If current character is '1'
      if (str[i] == '1')
      {

        // Update cntOne
        cntOne++;
      }
    }

    // Stores count of 0s
    int zero = 0;

    // Stores count of 1s
    int one = 0;

    // Stores maximum sum of count of
    // 0s and 1s by splitting the String
    int res = 0;

    // Traverse the binary String
    for (int i = 0; i < N - 1; i++) {

      // If current character
      // is '0'
      if (str[i] == '0') {

        // Update zero
        zero++;
      }

      // If current character is '1'
      else {

        // Update one
        one++;
      }

      // Update res
      res = Math.Max(res, zero + cntOne - one);
    }
    return res;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    String str = "00111";
    int N = str.Length;

    Console.Write(maxSumbySplittingString(str, N));
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the maximum sum of count  of
// 0s in the left substring and count of 1s in
// the right substring by splitting the string
function maxSumbySplittingstring(str, N)
{

    // Stores count of 1s
    // the in binary string
    var cntOne = 0;

    // Traverse the binary string
    for(var i = 0; i < N; i++) {

        // If current character is '1'
        if (str[i] == '1') {

            // Update cntOne
            cntOne++;
        }
    }

    // Stores count of 0s
    var zero = 0;

    // Stores count of 1s
    var one = 0;

    // Stores maximum sum of count of
    // 0s and 1s by splitting the string
    var res = 0;

    // Traverse the binary string
    for (var i = 0; i < N - 1; i++) {

        // If current character
        // is '0'
        if (str[i] == '0') {

            // Update zero
            zero++;
        }

        // If current character is '1'
        else {

            // Update one
            one++;
        }

        // Update res
        res = Math.max(res, zero + cntOne - one);
    }

    return res;
}

// Driver Code
var str = "00111";
var N = str.length;
document.write( maxSumbySplittingstring(str, N));

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)