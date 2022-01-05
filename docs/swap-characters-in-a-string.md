# 交换字符串中的字符

> 原文:[https://www.geeksforgeeks.org/swap-characters-in-a-string/](https://www.geeksforgeeks.org/swap-characters-in-a-string/)

给定一个长度为 **N** 的字符串 **S** ，两个整数 **B** 和 **C** ，任务是从头开始遍历字符，将一个字符与它的 C 位后的字符交换，即在位置 **i** 和 **(i + C)%N** 交换字符。重复此过程 **B** 次，一次前进一个位置。你的任务是找到 **B** 互换后的最终字符串。

**示例:**

```
Input : S = "ABCDEFGH", B = 4, C = 3;
Output:  DEFGBCAH
Explanation:
         after 1st swap: DBCAEFGH
         after 2nd swap: DECABFGH
         after 3rd swap: DEFABCGH
         after 4th swap: DEFGBCAH

Input : S = "ABCDE", B = 10, C = 6;
Output : ADEBC
Explanation:
         after 1st swap: BACDE
         after 2nd swap: BCADE
         after 3rd swap: BCDAE
         after 4th swap: BCDEA
         after 5th swap: ACDEB
         after 6th swap: CADEB
         after 7th swap: CDAEB
         after 8th swap: CDEAB
         after 9th swap: CDEBA
         after 10th swap: ADEBC
```

**天真的方法**:

*   对于 **B** 的大值，循环 **B** 次的幼稚做法，每次用 **(i + C)%N 次**字符交换字符都会导致高 CPU 时间。
*   解决这个问题的诀窍是在每次 **N** 迭代后观察得到的字符串，其中 **N** 是字符串 **S** 的长度。
*   同样，如果 **C** 大于或等于 **N** ，它实际上等于 **C** 除以 **N** 的余数。
*   在这里，让我们考虑一下 **C** 小于 **N** 。

**有效方法:**

*   如果我们观察每 **N** 次连续迭代和交换后形成的字符串(我们称之为一次完整迭代)，我们可以开始得到一个模式。
*   我们可以发现字符串分为两部分:长度的第一部分 **C** 由 **S** 的第一个 **C** 字符组成，第二部分由其余字符组成。
*   这两个部分旋转了一些地方。每一次完整的迭代，第一部分向右旋转 **(N % C)** 个位置。
*   第二部分在每次完整迭代中向左旋转 **C** 个位置。
*   我们可以通过将 **B** 除以 **N** 来计算完整迭代的次数 **f** 。
*   因此，第一部分将向左旋转 **( N % C ) * f** 。这个值可以超越 **C** 所以，实际上就是 **( ( N % C ) * f ) % C** ，也就是第一个零件会被**旋转((N % C ) * f ) % C** 个位置剩下。
*   第二部分将向左旋转 **C * f** 个位置。由于该值可以超出第二部分**(N–C)**的长度，因此实际上是**((C * f)%(N–C))**，即第二部分将旋转**((C * f)%(N–C))**位。
*   在 **f** 完整迭代之后，可能还剩下一些迭代来完成 **B** 迭代。该值为 **B % N** ，小于 **N** 。在 **f** 完整迭代之后，我们可以在这些剩余的迭代中遵循天真的方法来获得结果字符串。

> **例:**
> s = ABCDEFGHIJK；c = 4；
> 零件:1 次全迭代后的 ABCD EFGHIJK
> 2 次全迭代后的 DABC IJKEFGH
> CDAB FGHIJKE
> 3 次全迭代后的 BCDA jkeghi
> 4 次全迭代后的 ABCD GHIJKEF
> 5 次全迭代后的 DABC KEFGHIJ
> 6 次全迭代后的 CDAB HIJKEFG
> 7 次全迭代后的 BCDA EFGHIJK
> 8 次全迭代后的 ABCD IJKEFGH

以下是该方法的实施情况:

## C++

```
// C++ program to find new after swapping
// characters at position i and i + c
// b times, each time advancing one
// position ahead
#include <bits/stdc++.h>
using namespace std;

string rotateLeft(string s, int p)
{

    // Rotating a string p times left is
    // effectively cutting the first p
    // characters and placing them at the end
    return s.substr(p) + s.substr(0, p);
}

// Method to find the required string
string swapChars(string s, int c, int b)
{

    // Get string length
    int n = s.size();

    // If c is larger or equal to the length of
    // the string is effectively the remainder of
    // c divided by the length of the string
    c = c % n;

    if (c == 0)
    {

        // No change will happen
        return s;
    }
    int f = b / n;
    int r = b % n;

    // Rotate first c characters by (n % c)
    // places f times
    string p1 = rotateLeft(s.substr(0, c),
                  ((n % c) * f) % c);

    // Rotate remaining character by
    // (n * f) places
    string p2 = rotateLeft(s.substr(c),
                  ((c * f) % (n - c)));

    // Concatenate the two parts and convert the
    // resultant string formed after f full
    // iterations to a string array
    // (for final swaps)
    string a = p1 + p2;

    // Remaining swaps
    for(int i = 0; i < r; i++)
    {

        // Swap ith character with
        // (i + c)th character
        char temp = a[i];
        a[i] = a[(i + c) % n];
        a[(i + c) % n] = temp;
    }

    // Return final string
    return a;
}

// Driver code
int main()
{

    // Given values
    string s1 = "ABCDEFGHIJK";
    int b = 1000;
    int c = 3;

    // Get final string print final string
    cout << swapChars(s1, c, b) << endl;
}

// This code is contributed by rag2127
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find new after swapping
// characters at position i and i + c
// b times, each time advancing one
// position ahead

class GFG {
    // Method to find the required string

    String swapChars(String s, int c, int b)
    {
        // Get string length
        int n = s.length();

        // if c is larger or equal to the length of
        // the string is effectively the remainder of
        // c divided by the length of the string
        c = c % n;

        if (c == 0) {
            // No change will happen
            return s;
        }

        int f = b / n;
        int r = b % n;

        // Rotate first c characters by (n % c)
        // places f times
        String p1 = rotateLeft(s.substring(0, c),
                               ((n % c) * f) % c);

        // Rotate remaining character by
        // (n * f) places
        String p2 = rotateLeft(s.substring(c),
                               ((c * f) % (n - c)));

        // Concatenate the two parts and convert the
        // resultant string formed after f full
        // iterations to a character array
        // (for final swaps)
        char a[] = (p1 + p2).toCharArray();

        // Remaining swaps
        for (int i = 0; i < r; i++) {

            // Swap ith character with
            // (i + c)th character
            char temp = a[i];
            a[i] = a[(i + c) % n];
            a[(i + c) % n] = temp;
        }

        // Return final string
        return new String(a);
    }

    String rotateLeft(String s, int p)
    {
        // Rotating a string p times left is
        // effectively cutting the first p
        // characters and placing them at the end
        return s.substring(p) + s.substring(0, p);
    }

    // Driver code
    public static void main(String args[])
    {
        // Given values
        String s1 = "ABCDEFGHIJK";
        int b = 1000;
        int c = 3;

        // get final string
        String s2 = new GFG().swapChars(s1, c, b);

        // print final string
        System.out.println(s2);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find new after swapping
# characters at position i and i + c
# b times, each time advancing one
# position ahead

# Method to find the required string
def swapChars(s, c, b):

    # Get string length
    n = len(s)

    # If c is larger or equal to the length of
    # the string is effectively the remainder of
    # c divided by the length of the string
    c = c % n

    if (c == 0):

        # No change will happen
        return s

    f = int(b / n)
    r = b % n

    # Rotate first c characters by (n % c)
    # places f times
    p1 = rotateLeft(s[0 : c], ((c * f) % (n - c)))

    # Rotate remaining character by
    # (n * f) places
    p2 = rotateLeft(s[c:], ((c * f) % (n - c)))

    # Concatenate the two parts and convert the
    # resultant string formed after f full
    # iterations to a character array
    # (for final swaps)
    a = p1 + p2
    a = list(a)

    # Remaining swaps
    for i in range(r):

        # Swap ith character with
        # (i + c)th character
        temp = a[i]
        a[i] = a[(i + c) % n]
        a[(i + c) % n] = temp

    # Return final string
    return str("".join(a))

def rotateLeft(s, p):

    # Rotating a string p times left is
    # effectively cutting the first p
    # characters and placing them at the end
    return s[p:] + s[0 : p]

# Driver code

# Given values
s1 = "ABCDEFGHIJK"
b = 1000
c = 3

# Get final string
s2 = swapChars(s1, c, b)

# Print final string
print(s2)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# Program to find new after swapping
// characters at position i and i + c
// b times, each time advancing one
// position ahead
using System;

class GFG
{
    // Method to find the required string
    String swapChars(String s, int c, int b)
    {
        // Get string length
        int n = s.Length;

        // if c is larger or equal to the length of
        // the string is effectively the remainder of
        // c divided by the length of the string
        c = c % n;

        if (c == 0)
        {
            // No change will happen
            return s;
        }

        int f = b / n;
        int r = b % n;

        // Rotate first c characters by (n % c)
        // places f times
        String p1 = rotateLeft(s.Substring(0, c),
                            ((n % c) * f) % c);

        // Rotate remaining character by
        // (n * f) places
        String p2 = rotateLeft(s.Substring(c),
                            ((c * f) % (n - c)));

        // Concatenate the two parts and convert the
        // resultant string formed after f full
        // iterations to a character array
        // (for readonly swaps)
        char []a = (p1 + p2).ToCharArray();

        // Remaining swaps
        for (int i = 0; i < r; i++)
        {

            // Swap ith character with
            // (i + c)th character
            char temp = a[i];
            a[i] = a[(i + c) % n];
            a[(i + c) % n] = temp;
        }

        // Return readonly string
        return new String(a);
    }

    String rotateLeft(String s, int p)
    {

        // Rotating a string p times left is
        // effectively cutting the first p
        // characters and placing them at the end
        return s.Substring(p) + s.Substring(0, p);
    }

    // Driver code
    public static void Main(String []args)
    {
        // Given values
        String s1 = "ABCDEFGHIJK";
        int b = 1000;
        int c = 3;

        // get readonly string
        String s2 = new GFG().swapChars(s1, c, b);

        // print readonly string
        Console.WriteLine(s2);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript Program to find new after swapping
// characters at position i and i + c
// b times, each time advancing one
// position ahead

function swapChars(s, c, b)
{

    // Get string length
        let n = s.length;

        // if c is larger or equal to the length of
        // the string is effectively the remainder of
        // c divided by the length of the string
        c = c % n;

        if (c == 0) {
            // No change will happen
            return s;
        }

        let f = Math.floor(b / n);
        let r = b % n;

        // Rotate first c characters by (n % c)
        // places f times
        let p1 = rotateLeft(s.substring(0, c),
                               ((n % c) * f) % c);

        // Rotate remaining character by
        // (n * f) places
        let p2 = rotateLeft(s.substring(c),
                               ((c * f) % (n - c)));

        // Concatenate the two parts and convert the
        // resultant string formed after f full
        // iterations to a character array
        // (for final swaps)
        let a = (p1 + p2).split("");

        // Remaining swaps
        for (let i = 0; i < r; i++) {

            // Swap ith character with
            // (i + c)th character
            let temp = a[i];
            a[i] = a[(i + c) % n];
            a[(i + c) % n] = temp;
        }

        // Return final string
        return (a).join("");
}

function rotateLeft(s,p)
{
    // Rotating a string p times left is
        // effectively cutting the first p
        // characters and placing them at the end
        return s.substring(p) + s.substring(0, p);
}

 // Driver code
// Given values
let s1 = "ABCDEFGHIJK";
let b = 1000;
let c = 3;

// get final string
let s2 = swapChars(s1, c, b);

// print final string
document.write(s2);

// This code is contributed by ab2127
</script>
```

**Output:** 

```
CADEFGHIJKB
```

**时间复杂度**:O(n)
T3】空间复杂度 : O(n)