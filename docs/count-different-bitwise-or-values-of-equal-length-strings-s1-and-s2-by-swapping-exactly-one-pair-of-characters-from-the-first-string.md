# 通过从第一个字符串中交换正好一对字符来计算长度相等的字符串 S1 和 S2 的不同位或值

> 原文:[https://www . geeksforgeeks . org/count-等长字符串的不同位或值-S1-和-S2-通过从第一个字符串交换正好一对字符/](https://www.geeksforgeeks.org/count-different-bitwise-or-values-of-equal-length-strings-s1-and-s2-by-swapping-exactly-one-pair-of-characters-from-the-first-string/)

给定两个长度均为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)**【S1】**和 **S2** ，任务是通过[从字符串 **S1** 中交换](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/)正好一对字符，来计算除原始字符串 **S1** 和 **S2** 之外的[位或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的不同值的数量。

**示例:**

> **输入:**S1 =“1100”，S2 =“0011”
> **输出:** 4
> **说明:**S1 和 S2 的按位 OR，如果不进行交换则为“1111”。
> 以下是为获得不同的按位“或”值而进行的字符交换:
> 
> *   如果在 0 <sup>第</sup>和 2 <sup>第</sup>索引处的字符被交换，那么字符串 S1 修改为“0110”。现在，两个字符串的按位“或”是“0111”。
> *   如果在 0 <sup>第</sup>和 3 <sup>第</sup>索引处的字符被交换，那么字符串 S1 修改为“0101”。现在，两个字符串的按位“或”是“0111”。
> *   如果 1 <sup>st</sup> 和 2 <sup>nd</sup> 索引处的字符被交换，那么字符串 S1 将修改为“1010”。现在，两个字符串的按位“或”是“1011”。
> *   如果 1 <sup>st</sup> 和 3 <sup>rd</sup> 索引处的字符被交换，那么字符串 S1 将修改为“1001”。现在，两个字符串的按位“或”是“1011”。
> 
> 完成上述步骤后，所有按位“或”都不同于原始字符串的按位“或”。因此，总数为 4。
> 
> **输入:**S1 =“01001”，S2 =“11011”
> T3】输出: 2

**方法:**给定的问题可以基于以下观察来解决:

*   如果在[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S1** 中交换了相同的字符，则不会影响[按位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。
*   如果在字符串**【S1】**中交换了不同的字符，比如说 **S1[i] = '0'** 和 **S2[j] = '1'** ，那么该值的[位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)将按照以下规则进行更改:
    *   如果 **S2[i] = '0'** 和 **S2[j] = '0'** 。
    *   如果 **S2[i] = '1'** 和 **S2[j] = '0'** 。
    *   如果 **S2[i] = '0'** 和 **S2[j] = '1'** 。

根据以上观察，按照以下步骤解决问题:

*   初始化四个变量，比如说 **t00** 、 **t10** 、 **t11** 、 **t01** 存储索引数量 **i** 使得 **S1[i] = '0'** 和 **S2[i] = '0'** 、 **S1[i] = '1'** 和 **S2[i] = '0'**
*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)**【S1】**和 **S2** ，按照以下步骤递增 **t00** 、 **t10** 、 **t11** 、 **t01** 的值:
    *   如果 **S1[i] = '0'** 和**S2[I]= ' 0 '**，则将 **t00** 的值增加 **1** 。
    *   如果 **S1[i] = '1'** 和 **S2[i] = '0'** ，那么将 **t10** 的值增加 **1** 。
    *   如果 **S1[i] = '1'** 和 **S2[i] = '1'** ，那么将 **t11** 的值增加 **1** 。
    *   如果 **S1[i] = '0'** 和 **S2[i] = '1'** ，那么将 **t01** 的值增加 **1** 。
*   完成上述步骤后，打印 **t00 * t10 + t01 * t10 + t00 * t11** 的值，作为与原始按位“或”不同的[按位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)所需交换的结果数量。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of ways
// to obtain different Bitwise OR
void differentBitwiseOR(string s1,
                        string s2)
{
    int n = s1.size();

    // Stores the count of pairs t00,
    // t10, t01, t11
    int t00 = 0, t10 = 0, t01 = 0, t11 = 0;

    // Traverse the characters of
    // the string S1 and S2
    for (int i = 0; i < n; i++) {

        // Count the pair (0, 0)
        if (s1[i] == '0'
            && s2[i] == '0') {
            t00++;
        }

        // Count the pair (1, 0)
        if (s1[i] == '1'
            && s2[i] == '0') {
            t10++;
        }

        // Count the pair (1, 1)
        if (s1[i] == '1'
            && s2[i] == '1') {
            t11++;
        }

        // Count the pair (0, 1)
        if (s1[i] == '0'
            && s2[i] == '1') {
            t01++;
        }
    }

    // Number of ways to calculate the
    // different bitwise OR
    int ans = t00 * t10 + t01 * t10
              + t00 * t11;

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    string S1 = "01001";
    string S2 = "11011";
    differentBitwiseOR(S1, S2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the number of ways
// to obtain different Bitwise OR
static void differentBitwiseOR(String s1, String s2)
{
    int n = s1.length();

    // Stores the count of pairs t00,
    // t10, t01, t11
    int t00 = 0, t10 = 0, t01 = 0, t11 = 0;

    // Traverse the characters of
    // the string S1 and S2
    for(int i = 0; i < n; i++)
    {

        // Count the pair (0, 0)
        if (s1.charAt(i) == '0' &&
            s2.charAt(i) == '0')
        {
            t00++;
        }

        // Count the pair (1, 0)
        if (s1.charAt(i) == '1' &&
            s2.charAt(i) == '0')
        {
            t10++;
        }

        // Count the pair (1, 1)
        if (s1.charAt(i) == '1' &&
            s2.charAt(i) == '1')
        {
            t11++;
        }

        // Count the pair (0, 1)
        if (s1.charAt(i) == '0' &&
            s2.charAt(i) == '1')
        {
            t01++;
        }
    }

    // Number of ways to calculate the
    // different bitwise OR
    int ans = t00 * t10 + t01 * t10 + t00 * t11;

    // Print the result
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
    String S1 = "01001";
    String S2 = "11011";

    differentBitwiseOR(S1, S2);
}
}

// This code is contributed by subhammahato348
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the number of ways
# to obtain different Bitwise OR
def differentBitwiseOR(s1, s2):
    n = len(s1)

    # Stores the count of pairs t00,
    # t10, t01, t11
    t00 = 0
    t10 = 0
    t01 = 0
    t11 = 0

    # Traverse the characters of
    # the string S1 and S2
    for i in range(n):

        # Count the pair (0, 0)
        if (s1[i] == '0'  and s2[i] == '0'):
            t00 += 1

        # Count the pair (1, 0)
        if (s1[i] == '1' and s2[i] == '0'):
                t10 += 1

        # Count the pair (1, 1)
        if (s1[i] == '1' and s2[i] == '1'):
                t11 += 1

        # Count the pair (0, 1)
        if (s1[i] == '0' and s2[i] == '1'):
                t01 += 1

    # Number of ways to calculate the
    # different bitwise OR
    ans = t00 * t10 + t01 * t10 + t00 * t11

    # Print the result
    print(ans)

# Driver Code
S1 = "01001"
S2 = "11011"
differentBitwiseOR(S1, S2)

# This code is contributed by _saurabh_jaiswal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the number of ways
// to obtain different Bitwise OR
static void differentBitwiseOR(String s1,
                               String s2)
{
    int n = s1.Length;

    // Stores the count of pairs t00,
    // t10, t01, t11
    int t00 = 0, t10 = 0, t01 = 0, t11 = 0;

    // Traverse the characters of
    // the string S1 and S2
    for(int i = 0; i < n; i++)
    {

        // Count the pair (0, 0)
        if (s1[i] == '0' && s2[i] == '0')
        {
            t00++;
        }

        // Count the pair (1, 0)
        if (s1[i] == '1' && s2[i] == '0')
        {
            t10++;
        }

        // Count the pair (1, 1)
        if (s1[i] == '1' && s2[i] == '1')
        {
            t11++;
        }

        // Count the pair (0, 1)
        if (s1[i] == '0' && s2[i] == '1')
        {
            t01++;
        }
    }

    // Number of ways to calculate the
    // different bitwise OR
    int ans = t00 * t10 + t01 * t10 + t00 * t11;

    // Print the result
    Console.Write(ans);
}

// Driver Code
public static void Main()
{
    String S1 = "01001";
    String S2 = "11011";

    differentBitwiseOR(S1, S2);
}
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to find the number of ways
        // to obtain different Bitwise OR
        function differentBitwiseOR(s1, s2) {
            let n = s1.length;

            // Stores the count of pairs t00,
            // t10, t01, t11
            let t00 = 0, t10 = 0, t01 = 0, t11 = 0;

            // Traverse the characters of
            // the string S1 and S2
            for (let i = 0; i < n; i++) {

                // Count the pair (0, 0)
                if (s1[i] == '0'
                    && s2[i] == '0') {
                    t00++;
                }

                // Count the pair (1, 0)
                if (s1[i] == '1'
                    && s2[i] == '0') {
                    t10++;
                }

                // Count the pair (1, 1)
                if (s1[i] == '1'
                    && s2[i] == '1') {
                    t11++;
                }

                // Count the pair (0, 1)
                if (s1[i] == '0'
                    && s2[i] == '1') {
                    t01++;
                }
            }

            // Number of ways to calculate the
            // different bitwise OR
            let ans = t00 * t10 + t01 * t10
                + t00 * t11;

            // Print the result
            document.write(ans);
        }

        // Driver Code
        let S1 = "01001";
        let S2 = "11011";
        differentBitwiseOR(S1, S2);

  // This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)