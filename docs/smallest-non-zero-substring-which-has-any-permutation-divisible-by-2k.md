# 具有可被 2^K 整除的任意排列的最小非零子串

> 原文:[https://www . geeksforgeeks . org/minist-非零-substring-哪个有-2k 整除-任意排列/](https://www.geeksforgeeks.org/smallest-non-zero-substring-which-has-any-permutation-divisible-by-2k/)

给定一个长度为 **N** 的二进制字符串 **S** 和一个整数 **K** ，任务是找到 **S** 的最小非零子串，该子串可以被混在一起生成一个可被 **2 <sup>K</sup>** 整除的二进制字符串。如果不存在这样的子字符串，则打印 **-1** 。**注意**注意 **K** 始终大于 **0** 。
**例:**

> **输入:**S =“100”，k = 1
> **输出:** 2
> 可乱码的最小子串为“10”。
> 于是，答案是 2。
> **输入:** S = "1111 "，k = 2
> **输出:** -1

**方法:**我们来看看字符串的排列被**2<sup>K</sup>T5】整除的条件。** 

1.  该字符串必须至少有 **0s** 的 **K** 号。
2.  绳子必须至少有一个 **1** 。

这可以使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)来实现。对于每个索引 **i** ，尝试找到最小的索引 **j** ，使得子串**S【I…j-1】**满足上述两个条件。
假设左指针指向索引 **i** ，右指针指向 **j** ， **ans** 存储最小所需子串的长度。
如果条件不满足，则增加 **j** ，否则增加 **i** 。
迭代时，找到满足上述两个条件的最小值**(j–I)**，将答案更新为 **ans = min(ans，j–I)**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the length of the
// smallest substring divisible by 2^k
int findLength(string s, int k)
{
    // To store the final answer
    int ans = INT_MAX;

    // Left pointer
    int l = 0;

    // Right pointer
    int r = 0;

    // Count of the number of zeros and
    // ones in the current substring
    int cnt_zero = 0, cnt_one = 0;

    // Loop for two pointers
    while (l < s.size() and r <= s.size()) {

        // Condition satisfied
        if (cnt_zero >= k and cnt_one >= 1) {

            // Updated the answer
            ans = min(ans, r - l);

            // Update the pointer and count
            l++;
            if (s[l - 1] == '0')
                cnt_zero--;
            else
                cnt_one--;
        }

        else {

            // Update the pointer and count
            if (r == s.size())
                break;
            if (s[r] == '0')
                cnt_zero++;
            else
                cnt_one++;
            r++;
        }
    }

    if (ans == INT_MAX)
        return -1;
    return ans;
}

// Driver code
int main()
{
    string s = "100";
    int k = 2;

    cout << findLength(s, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    static final int INT_MAX = Integer.MAX_VALUE;

    // Function to return the length of the
    // smallest substring divisible by 2^k
    static int findLength(String s, int k)
    {
        // To store the final answer
        int ans = INT_MAX;

        // Left pointer
        int l = 0;

        // Right pointer
        int r = 0;

        // Count of the number of zeros and
        // ones in the current substring
        int cnt_zero = 0, cnt_one = 0;

        // Loop for two pointers
        while (l < s.length() && r <= s.length())
        {

            // Condition satisfied
            if (cnt_zero >= k && cnt_one >= 1)
            {

                // Updated the answer
                ans = Math.min(ans, r - l);

                // Update the pointer and count
                l++;
                if (s.charAt(l - 1) == '0')
                    cnt_zero--;
                else
                    cnt_one--;
            }
            else
            {

                // Update the pointer and count
                if (r == s.length())
                    break;
                if (s.charAt(r) == '0')
                    cnt_zero++;
                else
                    cnt_one++;
                r++;
            }
        }
        if (ans == INT_MAX)
            return -1;
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        String s = "100";
        int k = 2;

        System.out.println(findLength(s, k));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the length of the
# smallest subdivisible by 2^k
def findLength(s, k):

    # To store the final answer
    ans = 10**9

    # Left pointer
    l = 0

    # Right pointer
    r = 0

    # Count of the number of zeros and
    # ones in the current substring
    cnt_zero = 0
    cnt_one = 0

    # Loop for two pointers
    while (l < len(s) and r <= len(s)):

        # Condition satisfied
        if (cnt_zero >= k and cnt_one >= 1):

            # Updated the answer
            ans = min(ans, r - l)

            # Update the pointer and count
            l += 1
            if (s[l - 1] == '0'):
                cnt_zero -= 1
            else:
                cnt_one -= 1

        else:

            # Update the pointer and count
            if (r == len(s)):
                break
            if (s[r] == '0'):
                cnt_zero += 1
            else:
                cnt_one += 1
            r += 1

    if (ans == 10**9):
        return -1
    return ans

# Driver code
s = "100"
k = 2

print(findLength(s, k))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int INT_MAX = int.MaxValue;

    // Function to return the length of the
    // smallest substring divisible by 2^k
    static int findLength(string s, int k)
    {
        // To store the final answer
        int ans = INT_MAX;

        // Left pointer
        int l = 0;

        // Right pointer
        int r = 0;

        // Count of the number of zeros and
        // ones in the current substring
        int cnt_zero = 0, cnt_one = 0;

        // Loop for two pointers
        while (l < s.Length && r <= s.Length)
        {

            // Condition satisfied
            if (cnt_zero >= k && cnt_one >= 1)
            {

                // Updated the answer
                ans = Math.Min(ans, r - l);

                // Update the pointer and count
                l++;
                if (s[l - 1] == '0')
                    cnt_zero--;
                else
                    cnt_one--;
            }
            else
            {

                // Update the pointer and count
                if (r == s.Length)
                    break;

                if (s[r] == '0')
                    cnt_zero++;
                else
                    cnt_one++;
                r++;
            }
        }
        if (ans == INT_MAX)
            return -1;

        return ans;
    }

    // Driver code
    public static void Main ()
    {
        string s = "100";
        int k = 2;

        Console.WriteLine(findLength(s, k));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the length of the
// smallest substring divisible by 2^k
function findLength(s, k)
{
    // To store the final answer
    var ans = 1000000000;

    // Left pointer
    var l = 0;

    // Right pointer
    var r = 0;

    // Count of the number of zeros and
    // ones in the current substring
    var cnt_zero = 0, cnt_one = 0;

    // Loop for two pointers
    while (l < s.length && r <= s.length) {

        // Condition satisfied
        if (cnt_zero >= k && cnt_one >= 1) {

            // Updated the answer
            ans = Math.min(ans, r - l);

            // Update the pointer and count
            l++;
            if (s[l - 1] == '0')
                cnt_zero--;
            else
                cnt_one--;
        }

        else {

            // Update the pointer and count
            if (r == s.length)
                break;
            if (s[r] == '0')
                cnt_zero++;
            else
                cnt_one++;
            r++;
        }
    }

    if (ans == 1000000000)
        return -1;
    return ans;
}

// Driver code
var s = "100";
var k = 2;
document.write( findLength(s, k));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)