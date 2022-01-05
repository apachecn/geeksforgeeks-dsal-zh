# 在一串没有分隔符的数字中找到缺失的数字

> 原文:[https://www . geesforgeks . org/find-missing-number-string-numbers-no-separator/](https://www.geeksforgeeks.org/find-missing-number-string-numbers-no-separator/)

给定一个由一些数字组成的字符串，没有用任何分隔符分隔。这些数字都是正整数，除了缺少的数字之外，每个数字的序列都增加 1。任务是找到丢失的号码。数字不超过**六位**。如果输入序列无效，打印-1。

**示例:**

```
Input  : 89101113
Output : 12

Input  : 9899101102
Output : 100

Input  : 596597598600601602:
Output : 599

Input  : 909192939495969798100101
Output : 99

Input  : 11111211311411511
Output : -1
```

想法是尝试从 1 到 6 的所有长度。对于我们尝试的每个长度，我们检查当前长度是否满足所有连续数字和一个缺失的属性。一个有趣的事情是数字的数量可能会随着我们增加数字而变化。例如，当我们从 99 移动到 100 时。为了处理这种情况，我们使用对数基数 10 来计算位数。

下面是上述方法的实现:

## C++

```
// C++ program to find a missing number in a
// string of consecutive numbers without any
// separator.
#include<bits/stdc++.h>
using namespace std;
const int MAX_DIGITS = 6;

// gets the integer at position i with length m,
// returns it or -1, if none
int getValue(const string& str, int i, int m)
{
    if (i + m > str.length())
        return -1;

    // Find value at index i and length m.
    int value = 0;
    for (int j = 0; j < m; j++)
    {
        int c = str[i + j] - '0';
        if (c < 0 || c > 9)
            return -1;
        value = value * 10 + c;
    }
    return value;
}

// Returns value of missing number
int findMissingNumber(const string& str)
{
    // Try all lengths for first number
    for (int m=1; m<=MAX_DIGITS; ++m)
    {
        // Get value of first number with current
        // length/
        int n = getValue(str, 0, m);
        if (n == -1)
           break;

        // To store missing number of current length
        int missingNo = -1;

        // To indicate whether the sequence failed
        // anywhere for current length.
        bool fail = false;

        // Find subsequent numbers with previous number as n
        for (int i=m; i!=str.length(); i += 1 + log10l(n))
        {
            // If we haven't yet found the missing number
            // for current length. Next number is n+2\. Note
            // that we use Log10 as (n+2) may have more
            // length than n.
            if ((missingNo == -1) &&
                (getValue(str, i, 1+log10l(n+2)) == n+2))
            {
                missingNo = n + 1;
                n += 2;
            }

            // If next value is (n+1)
            else if (getValue(str, i, 1+log10l(n+1)) == n+1)
                n++;

            else
            {
                fail = true;
                break;
            }
        }

        if (!fail)
          return missingNo;
    }
    return -1; // not found or no missing number
}

// Driver code
int main()
{
    cout << findMissingNumber("99101102");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a missing number in a
// string of consecutive numbers without any
// separator.

class GFG {

    static final int MAX_DIGITS = 6;

// gets the integer at position i with length m,
// returns it or -1, if none
    static int getValue(String str, int i, int m) {
        if (i + m > str.length()) {
            return -1;
        }

        // Find value at index i and length m.
        int value = 0;
        for (int j = 0; j < m; j++) {
            int c = str.charAt(i + j) - '0';
            if (c < 0 || c > 9) {
                return -1;
            }
            value = value * 10 + c;
        }
        return value;
    }

// Returns value of missing number
    static int findMissingNumber(String str) {
        // Try all lengths for first number
        for (int m = 1; m <= MAX_DIGITS; ++m) {
            // Get value of first number with current
            // length/
            int n = getValue(str, 0, m);
            if (n == -1) {
                break;
            }

            // To store missing number of current length
            int missingNo = -1;

            // To indicate whether the sequence failed
            // anywhere for current length.
            boolean fail = false;

            // Find subsequent numbers with previous number as n
            for (int i = m; i != str.length(); i += 1 + Math.log10(n)) {
                // If we haven't yet found the missing number
                // for current length. Next number is n+2\. Note
                // that we use Log10 as (n+2) may have more
                // length than n.
                if ((missingNo == -1)
                        && (getValue(str, i, (int) (1 + Math.log10(n + 2))) == n + 2)) {
                    missingNo = n + 1;
                    n += 2;
                } // If next value is (n+1)
                else if (getValue(str, i, (int) (1 + Math.log10(n + 1))) == n + 1) {
                    n++;
                } else {
                    fail = true;
                    break;
                }
            }

            if (!fail) {
                return missingNo;
            }
        }
        return -1; // not found or no missing number
    }
// Driver code

    public static void main(String[] args) {
        System.out.println(findMissingNumber("99101102"));
    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find
# a missing number in a
# string of consecutive
# numbers without any
# separator.
import math
MAX_DIGITS = 6

# gets the integer at position
# i with length m, returns it
# or -1, if none
def getValue(Str, i, m):

    if(i + m > len(Str)):
        return -1

    # Find value at index
    # i and length m.
    value = 0

    for j in range(m):
        c = (ord(Str[i + j]) -
             ord('0'))
        if(c < 0 or c > 9):
            return -1
        value = value * 10 + c
    return value

# Returns value of missing
# number
def findMissingNumber(Str):

    # Try all lengths for
    #first number
    for m in range(1, MAX_DIGITS + 1):

        # Get value of first
        # number with current
        # length
        n = getValue(Str, 0, m)
        if(n == -1):
            break

        # To store missing number
        # of current length
        missingNo = -1

        # To indicate whether
        # the sequence failed
        # anywhere for current
        # length.
        fail = False

        # Find subsequent numbers
        # with previous number as n
        i = m
        while(i != len(Str)):

            # If we haven't yet found
            # the missing number for
            # current length. Next
            # number is n+2\. Note
            # that we use Log10 as
            # (n+2) may have more
            # length than n.
            if((missingNo == -1) and
               (getValue(Str, i, 1 +
                int(math.log10(n + 2))) ==
                               n + 2)):
                missingNo = n + 1
                n += 2

            # If next value is (n+1)
            elif((getValue(Str, i, 1 +
                  int(math.log10(n + 1))) ==
                                 n + 1)):
                n += 1
            else:
                fail = True
                break
            i += 1 + int(math.log10(n))

        if(not fail):
            return missingNo

    # not found or no
    # missing number
    return -1

# Driver code
print(findMissingNumber("99101102"))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to find a missing number in a
// string of consecutive numbers without any
// separator.
using System;
public class GFG {

    static readonly int MAX_DIGITS = 6;

// gets the integer at position i with length m,
// returns it or -1, if none
    static int getValue(String str, int i, int m) {
        if (i + m > str.Length) {
            return -1;
        }

        // Find value at index i and length m.
        int value = 0;
        for (int j = 0; j < m; j++) {
            int c = str[i + j] - '0';
            if (c < 0 || c > 9) {
                return -1;
            }
            value = value * 10 + c;
        }
        return value;
    }

// Returns value of missing number
    static int findMissingNumber(String str) {
        // Try all lengths for first number
        for (int m = 1; m <= MAX_DIGITS; ++m) {
            // Get value of first number with current
            // length/
            int n = getValue(str, 0, m);
            if (n == -1) {
                break;
            }

            // To store missing number of current length
            int missingNo = -1;

            // To indicate whether the sequence failed
            // anywhere for current length.
            bool fail = false;

            // Find subsequent numbers with previous number as n
            for (int i = m; i != str.Length; i += 1 + (int)Math.Log10(n)) {
                // If we haven't yet found the missing number
                // for current length. Next number is n+2\. Note
                // that we use Log10 as (n+2) may have more
                // length than n.
                if ((missingNo == -1)
                        && (getValue(str, i, (int) (1 + Math.Log10(n + 2))) == n + 2)) {
                    missingNo = n + 1;
                    n += 2;
                } // If next value is (n+1)
                else if (getValue(str, i, (int) (1 + Math.Log10(n + 1))) == n + 1) {
                    n++;
                } else {
                    fail = true;
                    break;
                }
            }

            if (!fail) {
                return missingNo;
            }
        }
        return -1; // not found or no missing number
    }
// Driver code

    public static void Main() {
        Console.WriteLine(findMissingNumber("99101102"));
    }
}
  //This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find a missing number
// in a string of consecutive numbers without any
// separator.
let MAX_DIGITS = 6;

// Gets the integer at position i
// with length m, returns it or -1,
// if none
function getValue(str, i, m)
{
    if (i + m > str.length)
    {
        return -1;
    }

    // Find value at index i and length m.
    let value = 0;
    for(let j = 0; j < m; j++)
    {
        let c = str[i + j].charCodeAt(0) -
                       '0'.charCodeAt(0);
        if (c < 0 || c > 9)
        {
            return -1;
        }
        value = value * 10 + c;
    }
    return value;
}

// Returns value of missing number
function findMissingNumber(str)
{

    // Try all lengths for first number
    for(let m = 1; m <= MAX_DIGITS; ++m)
    {

        // Get value of first number with
        // current length
        let n = getValue(str, 0, m);
        if (n == -1)
        {
            break;
        }

        // To store missing number of
        // current length
        let missingNo = -1;

        // To indicate whether the sequence
        // failed anywhere for current length.
        let fail = false;

        // Find subsequent numbers with
        // previous number as n
        for(let i = m;
                i != str.length;
                i += 1 + Math.floor(Math.log10(n)))
        {

            // If we haven't yet found the missing number
            // for current length. Next number is n+2\. Note
            // that we use Log10 as (n+2) may have more
            // length than n.
            if ((missingNo == -1) &&
                (getValue(str, i, Math.floor(1 + Math.log10(n + 2))) == n + 2)) {
                missingNo = n + 1;
                n += 2;
            }

            // If next value is (n+1)
            else if (getValue(str, i, Math.floor(
                1 + Math.log10(n + 1))) == n + 1)
            {
                n++;
            }
            else
            {
                fail = true;
                break;
            }
        }

        if (!fail)
        {
            return missingNo;
        }
    }

    // Not found or no missing number
    return -1;
}

// Driver code
document.write(findMissingNumber("99101102"));

// This code is contributed by ab2127

</script>
```

**输出:**

```
100
```

本文由 **Roshni Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。