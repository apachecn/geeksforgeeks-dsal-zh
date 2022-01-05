# 将 0 的子串和 1 的子串串联起来的最小删除次数

> 原文:[https://www . geesforgeks . org/minimum-removes-make-string-concation-of-substring-of-0s-后跟-substring-of-1s/](https://www.geeksforgeeks.org/minimum-removals-to-make-a-string-concatenation-of-a-substring-of-0s-followed-by-a-substring-of-1s/)

给定长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串**，任务是从给定的二进制字符串中找到需要删除的最小字符数，以构成 **0** s 的子字符串，后跟 **1** s 的子字符串。

**示例:**

> **输入:** str = "00101101"
> **输出:** 2
> **解释:**移除 str[2]和 str[6]或移除 str[3]和 str[6]将给定的二进制字符串分别修改为“000111”或“001111”。这两种情况下所需的移除次数都是 2，这是可能的最小值。
> 
> **输入:**str = " 1110000001111 "
> T3】输出: 3

**天真法:**解决这个问题最简单的方法就是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，对于遇到的每一个**‘1’**，通过删除 **0** s 或者删除 **1** s，计算出所需的最小删除次数，最后打印出所需的最小删除次数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过在 **1s** 之后有一个辅助空间来保持 **0s** 的计数来优化。使用这种预计算，时间复杂度可以提高 **N** 倍。以下是步骤:

*   初始化一个变量，比如**和**，来存储需要删除的最小字符数。
*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，比如 **zeroCount[]** ，计算给定索引后出现的 **0s** 的个数。
*   [在范围**【N–2，0】**内从末端遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **字符串**，如果当前字符为 **0** ，则将**零计数【I】**更新为**(零计数【I+1】+1)**。否则，将**零计数[i]** 更新为**零计数[i + 1]** 。
*   初始化一个变量，比如说**一计数**，来计算 **1s** 的数量。
*   [再次遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)。对于每个发现为**‘1’**的角色，更新 **ans** 为 **ans** 和**的最小值(oneCount + zeroCount[i])** 。
*   经过上述步骤后，如果**和**的值保持不变，则需要删除 **0** 字符。否则， **ans** 是需要删除的字符数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#include <iostream>

using namespace std;

// Function to count minimum removals
// required to make a given string
// concatenation of substring of 0s
// followed by substring of 1s
int minimumDeletions(string s)
{

    // Stores the length of the string
    int n = s.size();

    // Precompute the count of 0s
    int zeroCount[n];

    // Check for the last character
    zeroCount[n - 1] = (s[n - 1] == '0') ? 1 : 0;

    // Traverse and update zeroCount array
    for(int i = n - 2; i >= 0; i--)

        // If current character is 0,
        zeroCount[i] = (s[i] == '0') ?

                       // Update aCount[i] as
                       // aCount[i + 1] + 1
                       zeroCount[i + 1] + 1 :

                       // Update as aCount[i + 1]
                       zeroCount[i + 1];

    // Keeps track of deleted 1s
    int oneCount = 0;

    // Stores the count of removals
    int ans = INT_MAX;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // If current character is 1
        if (s[i] == '1')
        {

            // Update ans
            ans = min(ans,
                      oneCount + 
                      zeroCount[i]);
            oneCount++;
        }
    }

    // If all 1s are deleted
    ans = min(ans, oneCount);

    // Return the minimum
    // number of deletions
    return (ans == INT_MAX) ? 0 : ans;
}

// Driver Code
int main()
{
    string stri = "00101101";

    cout << minimumDeletions(stri) << endl;

    return 0;
}

// This code is contributed by AnkThon
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to count minimum removals
    // required to make a given string
    // concatenation of substring of 0s
    // followed by substring of 1s
    public static int minimumDeletions(String s)
    {
        // Stores the length of the string
        int n = s.length();

        // Precompute the count of 0s
        int zeroCount[] = new int[n];

        // Check for the last character
        zeroCount[n - 1] = (s.charAt(n - 1)
                            == '0')
                               ? 1
                               : 0;

        // Traverse and update zeroCount array
        for (int i = n - 2; i >= 0; i--)

            // If current character is 0,
            zeroCount[i] = (s.charAt(i) == '0')

                               // Update aCount[i] as
                               // aCount[i + 1] + 1
                               ? zeroCount[i + 1] + 1

                               // Update as aCount[i + 1]
                               : zeroCount[i + 1];

        // Keeps track of deleted 1s
        int oneCount = 0;

        // Stores the count of removals
        int ans = Integer.MAX_VALUE;

        // Traverse the array
        for (int i = 0; i < n; i++) {

            // If current character is 1
            if (s.charAt(i) == '1') {

                // Update ans
                ans = Math.min(ans,
                               oneCount
                                   + zeroCount[i]);
                oneCount++;
            }
        }

        // If all 1s are deleted
        ans = Math.min(ans, oneCount);

        // Return the minimum
        // number of deletions
        return (ans == Integer.MAX_VALUE)
            ? 0
            : ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "00101101";
        System.out.println(
            minimumDeletions(str));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count minimum removals
# required to make a given string
# concatenation of substring of 0s
# followed by substring of 1s
def minimumDeletions(s):

    # Stores the length of the string
    n = len(s)

    # Precompute the count of 0s
    zeroCount = [ 0 for i in range(n)]

    # Check for the last character
    zeroCount[n - 1] = 1 if s[n - 1] == '0' else 0

    # Traverse and update zeroCount array
    for i in range(n - 2, -1, -1):

        # If current character is 0,
        zeroCount[i] = zeroCount[i + 1] + 1 if (s[i] == '0') else zeroCount[i + 1]

    # Keeps track of deleted 1s
    oneCount = 0

    # Stores the count of removals
    ans = 10**9

    # Traverse the array
    for i in range(n):

        # If current character is 1
        if (s[i] == '1'):

            # Update ans
            ans = min(ans,oneCount + zeroCount[i])
            oneCount += 1

    # If all 1s are deleted
    ans = min(ans, oneCount)

    # Return the minimum
    # number of deletions
    return 0 if ans == 10**18 else ans

# Driver Code
if __name__ == '__main__':
    str = "00101101"
    print(minimumDeletions(str))

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to count minimum removals
    // required to make a given string
    // concatenation of substring of 0s
    // followed by substring of 1s
    public static int minimumDeletions(String s)
    {
        // Stores the length of the string
        int n = s.Length;

        // Precompute the count of 0s
        int []zeroCount = new int[n];

        // Check for the last character
        zeroCount[n - 1] = (s[n - 1]
                            == '0')
                               ? 1
                               : 0;

        // Traverse and update zeroCount array
        for (int i = n - 2; i >= 0; i--)

            // If current character is 0,
            zeroCount[i] = (s[i] == '0')

                               // Update aCount[i] as
                               // aCount[i + 1] + 1
                               ? zeroCount[i + 1] + 1

                               // Update as aCount[i + 1]
                               : zeroCount[i + 1];

        // Keeps track of deleted 1s
        int oneCount = 0;

        // Stores the count of removals
        int ans = int.MaxValue;

        // Traverse the array
        for (int i = 0; i < n; i++) {

            // If current character is 1
            if (s[i] == '1') {

                // Update ans
                ans = Math.Min(ans,
                               oneCount
                                   + zeroCount[i]);
                oneCount++;
            }
        }

        // If all 1s are deleted
        ans = Math.Min(ans, oneCount);

        // Return the minimum
        // number of deletions
        return (ans == int.MaxValue)
            ? 0
            : ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String str = "00101101";
        Console.WriteLine(
            minimumDeletions(str));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Function to count minimum removals
    // required to make a given string
    // concatenation of substring of 0s
    // followed by substring of 1s
    function minimumDeletions(s)
    {
        // Stores the length of the string
        let n = s.length;

        // Precompute the count of 0s
        let zeroCount = [];

        // Check for the last character
        zeroCount[n - 1] = (s[n - 1]
                            == '0')
                               ? 1
                               : 0;

        // Traverse and update zeroCount array
        for (let i = n - 2; i >= 0; i--)

            // If current character is 0,
            zeroCount[i] = (s[i] == '0')

                           // Update aCount[i] as
                          // aCount[i + 1] + 1
                          ? zeroCount[i + 1] + 1

                         // Update as aCount[i + 1]
                           : zeroCount[i + 1];

        // Keeps track of deleted 1s
        let oneCount = 0;

        // Stores the count of removals
        let ans = Number.MAX_VALUE;

        // Traverse the array
        for (let i = 0; i < n; i++) {

            // If current character is 1
            if (s[i] == '1') {

                // Update ans
                ans = Math.min(ans,
                           oneCount
                           + zeroCount[i]);
                oneCount++;
            }
        }

        // If all 1s are deleted
        ans = Math.min(ans, oneCount);

        // Return the minimum
        // number of deletions
        return (ans == Number.MAX_VALUE)
            ? 0
            : ans;
    }

// Driver Code

    let str = "00101101";
        document.write(
            minimumDeletions(str));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)