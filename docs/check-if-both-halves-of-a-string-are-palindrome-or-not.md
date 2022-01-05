# 检查一个字符串的两半是否是回文

> 原文:[https://www . geeksforgeeks . org/check-如果字符串的两半都是回文或非回文/](https://www.geeksforgeeks.org/check-if-both-halves-of-a-string-are-palindrome-or-not/)

给定一个字符串 **str** ，任务是检查给定的字符串是否可以拆分成两半，每一半都是[回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。如果可能，打印**是**。否则，打印**否**。
**举例:**

> **输入:** str **=** 【馕】
> **输出:** No
> **说明:**
> 因为两半**【馕】****【an】**都不是回文。
> **输入:**mommad
> **输出:** Yes
> **解释:**
> 既然两个半**“妈”**和**“爸”**都是回文。

**进场:**
按照以下步骤解决问题:

*   迭代字符串的第一个**((N/2)/2–1)**索引。
*   通过以下两种情况同时检查两半是否回文:
    *   如果 **S[i]** 与**S[N/2–1–I]**的*不相等，则前半部分不回文。*
    *   如果**S【N/2+I】**不等于*T3**S【N–1–I】**，则后半部分不回文。*
*   如果上述条件在迭代过程中没有一个得到满足，那么这两部分都是回文。打印**是**。
*   否则，打印**否**。

以下是上述方法的实现:

## C++

```
// C++ Program to check whether
// both halves of a string is
// Palindrome or not
#include <bits/stdc++.h>
using namespace std;

// Function to check if both halves
// of a string are palindrome or not
void checkPalindrome(string S)
{
    // Length of string
    int N = S.size();

    // Initialize both part as true
    bool first_half = true;
    bool second_half = true;

    int cnt = (N / 2) - 1;

    for (int i = 0; i < ((N / 2) / 2); i++) {

        // If first half is not palindrome
        if (S[i] != S[cnt]) {
            first_half = false;
            break;
        }

        // If second half is not palindrome
        if (S[N / 2 + i] != S[N / 2 + cnt]) {
            second_half - false;
            break;
        }

        cnt--;
    }

    // If both halves are Palindrome
    if (first_half && second_half) {
        cout << "Yes" << endl;
    }
    else {
        cout << "No" << endl;
    }
}

int main()
{
    string S = "momdad";

    checkPalindrome(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check whether
// both halves of a string is
// Palindrome or not
public class Main {

    // Function to check and return if
    // both halves of a string are
    // palindromic or not
    public static void checkPalindrome(
        String S)
    {
        // Length of string
        int N = S.length();

        // Initialize both part as true
        boolean first_half = true;
        boolean second_half = true;

        int cnt = (N / 2) - 1;

        for (int i = 0; i < (N / 2); i++) {

            // If first half is not palindrome
            if (S.charAt(i) != S.charAt(cnt)) {
                first_half = false;
                break;
            }

            // If second half is not palindrome
            if (S.charAt(N / 2 + i)
                != S.charAt(N / 2 + cnt)) {
                second_half = false;
                break;
            }

            cnt--;
        }

        // If both halves are Palindrome
        if (first_half && second_half) {
            System.out.println("Yes");
        }
        else {
            System.out.println("No");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        String S = "momdad";

        checkPalindrome(S);
    }
}
```

## 蟒蛇 3

```
# Python3 program to check whether
# both halves of a string is
# palindrome or not

# Function to check if both halves
# of a string are palindrome or not
def checkPalindrome(S):

    # Length of string
    n = len(S)

    # Initialize both part as true
    first_half = True
    second_half = True

    cnt = (n // 2) - 1

    for i in range(0, int((n / 2) / 2)):

        # If first half is not palindrome
        if (S[i] != S[cnt]):
            first_half = False
            break

        # If second half is not palindrome
        if (S[n // 2 + i] != S[n // 2 + cnt]):
            second_half = False
            break

        cnt -= 1

    # If both halves are palindrome
    if (first_half and second_half):
        print('Yes', end = '')
    else:
        print('No', end = '')

# Driver code
if __name__=='__main__':

    S = 'momdad'

    checkPalindrome(S)

# This code is contributed by virusbuddah_
```

## C#

```
// C# program to check whether
// both halves of a string is
// Palindrome or not
using System;

class GFG{

// Function to check and return if
// both halves of a string are
// palindromic or not
public static void checkPalindrome(String S)
{

    // Length of string
    int N = S.Length;

    // Initialize both part as true
    bool first_half = true;
    bool second_half = true;

    int cnt = (N / 2) - 1;

    for(int i = 0; i < (N / 2); i++)
    {

        // If first half is not palindrome
        if (S[i] != S[cnt])
        {
            first_half = false;
            break;
        }

        // If second half is not palindrome
        if (S[N / 2 + i] != S[N / 2 + cnt])
        {
            second_half = false;
            break;
        }
        cnt--;
    }

    // If both halves are Palindrome
    if (first_half && second_half)
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}

// Driver code
public static void Main()
{
    String S = "momdad";

    checkPalindrome(S);
}
}

// This code is contributed by grand_master
```

## java 描述语言

```
<script>

// JavaScript Program to check whether
// both halves of a string is
// Palindrome or not

    // Function to check and return if
    // both halves of a string are
    // palindromic or not
    function checkPalindrome( S) {

        // Length of string
        var N = S.length;

        // Initialize both part as true
        var first_half = true;
        var second_half = true;

        var cnt = parseInt((N / 2)) - 1;

        for (i = 0; i < (N / 2); i++) {

            // If first half is not palindrome
            if (S.charAt(i) != S.charAt(cnt)) {
                first_half = false;
                break;
            }

            // If second half is not palindrome
            if (S.charAt(N / 2 + i) != S.charAt(N / 2 + cnt)) {
                second_half = false;
                break;
            }

            cnt--;
        }

        // If both halves are Palindrome
        if (first_half && second_half) {
            document.write("Yes");
        } else {
            document.write("No");
        }
    }

    // Driver Code

        var S = "momdad";

        checkPalindrome(S);

// This code contributed by aashish1995

</script>
```

**Output:**

```
Yes
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*