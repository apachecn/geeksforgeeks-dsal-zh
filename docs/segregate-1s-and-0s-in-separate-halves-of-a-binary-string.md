# 将 1 和 0 分隔成二进制字符串的两半

> 原文:[https://www . geeksforgeeks . org/将二进制字符串的半部分分隔为-1 和-0/](https://www.geeksforgeeks.org/segregate-1s-and-0s-in-separate-halves-of-a-binary-string/)

给定一个偶数长度的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串**，由相等数量的 **0** s 和 **1** s 组成，任务是[通过重复](https://www.geeksforgeeks.org/segregate-0s-and-1s-in-an-array-by-traversing-array-once/)[反转子字符串](https://www.geeksforgeeks.org/reverse-the-substrings-of-the-given-string-according-to-the-given-array-of-indices/)将所有的 1 和 0分成两半。打印所需的最小反转次数。

**示例:**

> **输入:** str = "01011100"
> **输出:** 2
> **说明:**执行的操作如下:
> 
> 1.  ”<u>010111</u>00”—>“11101000”
> 2.  “111<u>01</u>000”—>11110000”
> 
> **输入:** str = "101010"
> **输出:** 2
> **说明:**执行的操作如下:
> 
> 1.  “1<u>0101</u>0”—>“110100”
> 2.  “11<u>01</u>00”—>“111000”

**方法:**思路是统计字符串任意两个连续字符不相等的实例数。按照以下步骤解决问题:

*   初始化一个变量，比如**和**，计算相邻不相等字符对的数量。
*   现在，反转任何子串后，计数减少 **2** 。
*   [如果 **ans** 的值为奇数](https://www.geeksforgeeks.org/program-check-number-positive-negative-odd-even-zero/)，则所需答案为**(ans–1)/2，因为最终的字符串将在字符串的中心包含一对这样的字符串。**
*   否则，所需答案为 **ans/2** 。

下面是上述方法的实现:

## C++14

```
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum number
// of operations required to segregate
// all 1s and 0s in a binary string
void minOps(string s, int N)
{

    // Stores the count of unequal
    // pair of adjacent characters
    int ans = 0;
    for (int i = 1; i < N; i++)
    {

        // If an unequal pair of
        // adjacent characters occurs
        if (s[i] != s[i - 1])
        {
            ans++;
        }
    }

    // For odd count
    if (ans % 2 == 1)
    {
        cout << (ans - 1) / 2 << endl;
        return;
    }

    // For even count
    cout<<(ans / 2);
}

// Driver Code
int main()
{

  // Given string
  string str = "01011100";

  // Length of the string
  int N = str.size();

  // Prints the minimum count
  // of operations required
  minOps(str, N);

  return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to count the minimum number
    // of operations required to segregate
    // all 1s and 0s in a binary string
    static void minOps(String s, int N)
    {
        // Stores the count of unequal
        // pair of adjacent characters
        int ans = 0;

        for (int i = 1; i < N; i++) {

            // If an unequal pair of
            // adjacent characters occurs
            if (s.charAt(i) != s.charAt(i - 1)) {
                ans++;
            }
        }

        // For odd count
        if (ans % 2 == 1) {
            System.out.print((ans - 1) / 2);
            return;
        }

        // For even count
        System.out.print(ans / 2);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given string
        String str = "01011100";

        // Length of the string
        int N = str.length();

        // Prints the minimum count
        // of operations required
        minOps(str, N);
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to count the minimum number
# of operations required to segregate
# all 1s and 0s in a binary string
def minOps(s, N) :

    # Stores the count of unequal
    # pair of adjacent characters
    ans = 0
    for i in range(1, N):

        # If an unequal pair of
        # adjacent characters occurs
        if (s[i] != s[i - 1]) :
            ans += 1

    # For odd count
    if (ans % 2 == 1) :     
        print((ans - 1) // 2)
        return

    # For even count
    print(ans // 2)

# Driver Code

# Given string
str = "01011100"

# Length of the string
N = len(str)

# Prints the minimum count
# of operations required
minOps(str, N)

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

    // Function to count the minimum number
    // of operations required to segregate
    // all 1s and 0s in a binary string
    static void minOps(String s, int N)
    {

        // Stores the count of unequal
        // pair of adjacent characters
        int ans = 0;

        for (int i = 1; i < N; i++)
        {

            // If an unequal pair of
            // adjacent characters occurs
            if (s[i] != s[i - 1])
            {
                ans++;
            }
        }

        // For odd count
        if (ans % 2 == 1)
        {
            Console.Write((ans - 1) / 2);
            return;
        }

        // For even count
        Console.Write(ans / 2);
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // Given string
        String str = "01011100";

        // Length of the string
        int N = str.Length;

        // Prints the minimum count
        // of operations required
        minOps(str, N);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to count the minimum number
    // of operations required to segregate
    // all 1s and 0s in a binary string
    function minOps( s , N)
    {
        // Stores the count of unequal
        // pair of adjacent characters
        var ans = 0;

        for (i = 1; i < N; i++) {

            // If an unequal pair of
            // adjacent characters occurs
            if (s.charAt(i) != s.charAt(i - 1)) {
                ans++;
            }
        }

        // For odd count
        if (ans % 2 == 1) {
            document.write((ans - 1) / 2);
            return;
        }

        // For even count
        document.write(ans / 2);
    }

    // Driver Code

        // Given string
        var str = "01011100";

        // Length of the string
        var N = str.length;

        // Prints the minimum count
        // of operations required
        minOps(str, N);

// This code contributed by aashish1995

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)