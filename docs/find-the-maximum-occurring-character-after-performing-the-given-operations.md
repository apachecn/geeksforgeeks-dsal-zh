# 执行给定操作后找到最大出现字符

> 原文:[https://www . geesforgeks . org/find-执行给定操作后出现的最大字符数/](https://www.geeksforgeeks.org/find-the-maximum-occurring-character-after-performing-the-given-operations/)

给定一个由 **0、1** 和 ***** 组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是在执行给定操作后，从 **0** 和 **1** 中找出最大出现字符:

> *   Replace ***** with **0** , where ***** appears on the left side of the existing **0** s in the string.
> *   Replace ***** with **1** , where ***** appears on the right side of the existing **1** s in the string.
> *   If ***** can be replaced by **0** and **1** at the same time, it will remain unchanged.

**注意:**如果执行给定操作后 0 和 1 的频率相同，则打印 **-1** 。

**示例:**

> **输入:**str =“* * 0 * * 1 * * * 0”
> T3】输出: 0
> **说明:**
> 由于 **0** 可以代替其左侧的 ***** ，而 **1** 可以代替其右侧的 ***** ，因此字符串变为 000**1***0
> 
> **输入:** str = "0*1"
> **输出:** -1
> **说明:**
> 0 和 1 的频率相同，因此输出为-1。

**方法:**生成最终结果字符串，然后比较 0 和 1 的频率的想法。以下是步骤:

*   计算字符串中 0 和 1 的初始频率，并将其存储在变量中，如 **count_0** 和 **count_1** 。
*   初始化一个变量，比如 **prev** ，为-1。遍历字符串，检查当前字符是否为 ***** 。如果是，那就继续。
*   如果是遇到的第一个字符并且是 **0** ，那么将所有 ***** 添加到 **count_0** 并将 **prev** 更改为当前索引。
*   否则，如果第一个字符是 **1** ，则将 **prev** 更改为当前索引。
*   如果前一个字符是 **1** ，当前字符是 **0** ，那么在字符之间加上一半的 ***** 到 **0** ，一半到 **1** 。
*   如果前一个字符是 0，当前字符是 **1** ，那么它们之间没有 ***** 字符可以替换。
*   如果前一个和当前两个字符的类型相同，则将 ***** 的计数加到频率上。
*   比较 **0** 和 **1** 的频率，打印最大出现字符。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// maximum occurring character
void solve(string S)
{
    // Initialize count of
    // zero and one
    int count_0 = 0, count_1 = 0;

    int prev = -1;

    // Iterate over the given string
    for (int i = 0; i < S.length(); i++) {

        // Count the zeros
        if (S[i] == '0')
            count_0++;

        // Count the ones
        else if (S[i] == '1')
            count_1++;
    }

    // Iterate over the given string
    for (int i = 0; i < S.length(); i++) {

        // Check if character
        // is * then continue
        if (S[i] == '*')
            continue;

        // Check if first character
        // after * is X
        else if (S[i] == '0' && prev == -1) {

            // Add all * to
            // the frequency of X
            count_0 = count_0 + i;

            // Set prev to the
            // i-th character
            prev = i;
        }

        // Check if first character
        // after * is Y
        else if (S[i] == '1' && prev == -1) {

            // Set prev to the
            // i-th character
            prev = i;
        }

        // Check if prev character is 1
        // and current character is 0
        else if (S[prev] == '1' && S[i] == '0') {

            // Half of the * will be
            // converted to 0
            count_0 = count_0 + (i - prev - 1) / 2;

            // Half of the * will be
            // converted to 1
            count_1 = count_1 + (i - prev - 1) / 2;
            prev = i;
        }

        // Check if prev and current are 1
        else if (S[prev] == '1' && S[i] == '1') {

            // All * will get converted to 1
            count_1 = count_1 + (i - prev - 1);
            prev = i;
        }

        // No * can be replaced
        // by either 0 or 1
        else if (S[prev] == '0' && S[i] == '1')

            // Prev becomes the ith character
            prev = i;

        // Check if prev and current are 0
        else if (S[prev] == '0' && S[i] == '0') {

            // All * will get converted to 0
            count_0 = count_0 + (i - prev - 1);
            prev = i;
        }
    }

    // If frequency of 0
    // is more
    if (count_0 > count_1)
        cout << "0";

    // If frequency of 1
    // is more
    else if (count_1 > count_0)
        cout << "1";

    else {
        cout << -1;
    }
}

// Driver code
int main()
{
    // Given string
    string str = "**0**1***0";

    // Function Call
    solve(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the
// maximum occurring character
static void solve(String S)
{

    // Initialize count of
    // zero and one
    int count_0 = 0, count_1 = 0;

    int prev = -1;

    // Iterate over the given string
    for(int i = 0; i < S.length(); i++)
    {

        // Count the zeros
        if (S.charAt(i) == '0')
            count_0++;

        // Count the ones
        else if (S.charAt(i) == '1')
            count_1++;
    }

    // Iterate over the given string
    for(int i = 0; i < S.length(); i++)
    {

        // Check if character
        // is * then continue
        if (S.charAt(i) == '*')
            continue;

        // Check if first character
        // after * is X
        else if (S.charAt(i) == '0' && prev == -1)
        {

            // Add all * to
            // the frequency of X
            count_0 = count_0 + i;

            // Set prev to the
            // i-th character
            prev = i;
        }

        // Check if first character
        // after * is Y
        else if (S.charAt(i) == '1' && prev == -1)
        {

            // Set prev to the
            // i-th character
            prev = i;
        }

        // Check if prev character is 1
        // and current character is 0
        else if (S.charAt(prev) == '1' &&
                 S.charAt(i) == '0')
        {

            // Half of the * will be
            // converted to 0
            count_0 = count_0 + (i - prev - 1) / 2;

            // Half of the * will be
            // converted to 1
            count_1 = count_1 + (i - prev - 1) / 2;
            prev = i;
        }

        // Check if prev and current are 1
        else if (S.charAt(prev) == '1' &&
                 S.charAt(i) == '1')
        {

            // All * will get converted to 1
            count_1 = count_1 + (i - prev - 1);
            prev = i;
        }

        // No * can be replaced
        // by either 0 or 1
        else if (S.charAt(prev) == '0' &&
                 S.charAt(i) == '1')

            // Prev becomes the ith character
            prev = i;

        // Check if prev and current are 0
        else if (S.charAt(prev) == '0' &&
                 S.charAt(i) == '0')
        {

            // All * will get converted to 0
            count_0 = count_0 + (i - prev - 1);
            prev = i;
        }
    }

    // If frequency of 0
    // is more
    if (count_0 > count_1)
        System.out.print("0");

    // If frequency of 1
    // is more
    else if (count_1 > count_0)
        System.out.print("1");

    else
    {
        System.out.print("-1");
    }
}

// Driver code
public static void main (String[] args)
{

    // Given string
    String str = "**0**1***0";

    // Function call
    solve(str);
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the
# maximum occurring character
def solve(S):

    # Initialize count of
    # zero and one
    count_0 = 0
    count_1 = 0

    prev = -1

    # Iterate over the given string
    for i in range(len(S)) :

        # Count the zeros
        if (S[i] == '0'):
            count_0 += 1

        # Count the ones
        elif (S[i] == '1'):
            count_1 += 1

    # Iterate over the given string
    for i in range(len(S)):

        # Check if character
        # is * then continue
        if (S[i] == '*'):
            continue

        # Check if first character
        # after * is X
        elif (S[i] == '0' and prev == -1):

            # Add all * to
            # the frequency of X
            count_0 = count_0 + i

            # Set prev to the
            # i-th character
            prev = i

        # Check if first character
        # after * is Y
        elif (S[i] == '1' and prev == -1):

            # Set prev to the
            # i-th character
            prev = i

        # Check if prev character is 1
        # and current character is 0
        elif (S[prev] == '1' and S[i] == '0'):

            # Half of the * will be
            # converted to 0
            count_0 = count_0 + (i - prev - 1) / 2

            # Half of the * will be
            # converted to 1
            count_1 = count_1 + (i - prev - 1) // 2
            prev = i

        # Check if prev and current are 1
        elif (S[prev] == '1' and S[i] == '1'):

            # All * will get converted to 1
            count_1 = count_1 + (i - prev - 1)
            prev = i

        # No * can be replaced
        # by either 0 or 1
        elif (S[prev] == '0' and S[i] == '1'):

            # Prev becomes the ith character
            prev = i

        # Check if prev and current are 0
        elif (S[prev] == '0' and S[i] == '0'):

            # All * will get converted to 0
            count_0 = count_0 + (i - prev - 1)
            prev = i

    # If frequency of 0
    # is more
    if (count_0 > count_1):
        print("0")

    # If frequency of 1
    # is more
    elif (count_1 > count_0):
        print("1")
    else:
        print("-1")

# Driver code

# Given string
str = "**0**1***0"

# Function call
solve(str)

# This code is contributed by code_hunt
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the
// maximum occurring character
static void solve(string S)
{

    // Initialize count of
    // zero and one
    int count_0 = 0, count_1 = 0;

    int prev = -1;

    // Iterate over the given string
    for(int i = 0; i < S.Length; i++)
    {

        // Count the zeros
        if (S[i] == '0')
            count_0++;

        // Count the ones
        else if (S[i] == '1')
            count_1++;
    }

    // Iterate over the given string
    for(int i = 0; i < S.Length; i++)
    {

        // Check if character
        // is * then continue
        if (S[i] == '*')
            continue;

        // Check if first character
        // after * is X
        else if (S[i] == '0' && prev == -1)
        {

            // Add all * to
            // the frequency of X
            count_0 = count_0 + i;

            // Set prev to the
            // i-th character
            prev = i;
        }

        // Check if first character
        // after * is Y
        else if (S[i] == '1' && prev == -1)
        {

            // Set prev to the
            // i-th character
            prev = i;
        }

        // Check if prev character is 1
        // and current character is 0
        else if (S[prev] == '1' && S[i] == '0')
        {

            // Half of the * will be
            // converted to 0
            count_0 = count_0 + (i - prev - 1) / 2;

            // Half of the * will be
            // converted to 1
            count_1 = count_1 + (i - prev - 1) / 2;
            prev = i;
        }

        // Check if prev and current are 1
        else if (S[prev] == '1' && S[i] == '1')
        {

            // All * will get converted to 1
            count_1 = count_1 + (i - prev - 1);
            prev = i;
        }

        // No * can be replaced
        // by either 0 or 1
        else if (S[prev] == '0' && S[i] == '1')

            // Prev becomes the ith character
            prev = i;

        // Check if prev and current are 0
        else if (S[prev] == '0' && S[i] == '0')
        {

            // All * will get converted to 0
            count_0 = count_0 + (i - prev - 1);
            prev = i;
        }
    }

    // If frequency of 0
    // is more
    if (count_0 > count_1)
        Console.Write("0");

    // If frequency of 1
    // is more
    else if (count_1 > count_0)
        Console.Write("1");

    else
    {
        Console.Write("-1");
    }
}

// Driver code
public static void Main ()
{

    // Given string
    string str = "**0**1***0";

    // Function call
    solve(str);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to find the
    // maximum occurring character
    function solve( S) {

        // Initialize count of
        // zero and one
        var count_0 = 0, count_1 = 0;

        var prev = -1;

        // Iterate over the given string
        for (i = 0; i < S.length; i++) {

            // Count the zeros
            if (S.charAt(i) == '0')
                count_0++;

            // Count the ones
            else if (S.charAt(i) == '1')
                count_1++;
        }

        // Iterate over the given string
        for (i = 0; i < S.length; i++) {

            // Check if character
            // is * then continue
            if (S.charAt(i) == '*')
                continue;

            // Check if first character
            // after * is X
            else if (S.charAt(i) == '0' && prev == -1) {

                // Add all * to
                // the frequency of X
                count_0 = count_0 + i;

                // Set prev to the
                // i-th character
                prev = i;
            }

            // Check if first character
            // after * is Y
            else if (S.charAt(i) == '1' && prev == -1) {

                // Set prev to the
                // i-th character
                prev = i;
            }

            // Check if prev character is 1
            // and current character is 0
            else if (S.charAt(prev) == '1' && S.charAt(i) == '0') {

                // Half of the * will be
                // converted to 0
                count_0 = count_0 + (i - prev - 1) / 2;

                // Half of the * will be
                // converted to 1
                count_1 = count_1 + (i - prev - 1) / 2;
                prev = i;
            }

            // Check if prev and current are 1
            else if (S.charAt(prev) == '1' && S.charAt(i) == '1') {

                // All * will get converted to 1
                count_1 = count_1 + (i - prev - 1);
                prev = i;
            }

            // No * can be replaced
            // by either 0 or 1
            else if (S.charAt(prev) == '0' && S.charAt(i) == '1')

                // Prev becomes the ith character
                prev = i;

            // Check if prev and current are 0
            else if (S.charAt(prev) == '0' && S.charAt(i) == '0') {

                // All * will get converted to 0
                count_0 = count_0 + (i - prev - 1);
                prev = i;
            }
        }

        // If frequency of 0
        // is more
        if (count_0 > count_1)
            document.write("0");

        // If frequency of 1
        // is more
        else if (count_1 > count_0)
            document.write("1");

        else {
            document.write("-1");
        }
    }

    // Driver code
        // Given string
        var str = "**0**1***0";

        // Function call
        solve(str);

// This code IS contributed by umadevi9616
</script>
```

**Output:** 

```
0
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*