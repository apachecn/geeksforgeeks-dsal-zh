# 两个没有共同字符的给定字符串的交错

> 原文:[https://www . geesforgeks . org/check-给定字符串是否是两个其他给定字符串的交错/](https://www.geeksforgeeks.org/check-whether-a-given-string-is-an-interleaving-of-two-other-given-strings/)

给定三个字符串 A、B 和 C，编写一个函数，检查 C 是否是 A 和 B 的交织，可以假设 A 和 B 之间没有共同的字符(请参见[这个](https://www.geeksforgeeks.org/find-if-a-string-is-interleaved-of-two-other-strings-dp-33/)也处理共同字符的扩展解决方案)，如果 C 包含 A 和 B 的所有字符，并且保留了单个字符串中所有字符的顺序，则称 C 是交织 A 和 B。示例见[上一帖](https://www.geeksforgeeks.org/print-all-interleavings-of-given-two-strings/)。
**解决方法:**
逐个挑选 C 的每个字符，与 a 中的第一个字符匹配，如果不匹配，则与 B 的第一个字符匹配，如果连 B 的第一个字符都不匹配，则返回 false。如果字符与 A 的第一个字符匹配，则从 C 的第二个字符、A 的第二个字符和 B 的第一个字符重复上述过程。如果 C 的第一个字符与 B 的第一个字符匹配(并且与 A 的第一个字符不匹配)，则从 C 的第二个字符重复上述过程。 A 的第一个字符和 B 的第二个字符。如果 C 的所有字符都与 A 的字符或 B 的字符匹配，并且 C 的长度是 A 和 B 的长度之和，则 C 是 A 和 B 的交错。

## C++

```
// C++ program to check if given string is
// an interleaving of the other two strings
#include <bits/stdc++.h>
using namespace std;

// Returns true if C is an interleaving of A and B,
// otherwise returns false
bool isInterleaved (char A[], char B[], char C[])
{
    // Iterate through all characters of C.
    while (*C != 0)
    {
        // Match first character of C with first character
        // of A. If matches them move A to next
        if (*A == *C)
            A++;

        // Else Match first character of C with first
        // character of B. If matches them move B to next
        else if (*B == *C)
            B++;

        // If doesn't match with either A or B, then return
        // false
        else
            return false;

        // Move C to next for next iteration
        C++;
    }

    // If A or B still have some characters, then length of
    // C is smaller than sum of lengths of A and B, so
    // return false
    if (*A || *B)
        return false;

    return true;
}

// Driver program to test above functions
int main()
{
    char A[] = "AB";
    char B[] = "CD";
    char C[] = "ACBG";
    if (isInterleaved(A, B, C) == true)
        cout << C << " is interleaved of " << A << " and " << B;
    else
        cout << C << " is not interleaved of " << A << " and " << B;

    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
// C program to check if given string is an interleaving
// of the other two strings
#include<stdio.h>

// Returns true if C is an interleaving of A and B,
// otherwise returns false
bool isInterleaved (char *A, char *B, char *C)
{
    // Iterate through all characters of C.
    while (*C != 0)
    {
        // Match first character of C with first character
        // of A. If matches them move A to next
        if (*A == *C)
            A++;

        // Else Match first character of C with first
        // character of B. If matches them move B to next
        else if (*B == *C)
            B++;

        // If doesn't match with either A or B, then return
        // false
        else
            return false;

        // Move C to next for next iteration
        C++;
    }

    // If A or B still have some characters, then length of
    // C  is smaller than sum of lengths of A and B, so
    // return false
    if (*A || *B)
        return false;

    return true;
}

// Driver program to test above functions
int main()
{
    char *A = "AB";
    char *B = "CD";
    char *C = "ACBG";
    if (isInterleaved(A, B, C) == true)
        printf("%s is interleaved of %s and %s", C, A, B);
    else
        printf("%s is not interleaved of %s and %s", C, A, B);

    return 0;
}

// This code is contributed by Venkat
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the given string is
// an interleaving of the other two strings
public class GfG{

    // Returns true if C is an interleaving
    // of A and B, otherwise returns false
    static boolean isInterleaved (String A, String B, String C)
    {
        int i = 0, j = 0, k = 0;

        // Iterate through all characters of C.
        while (k != C.length())
        {
            // Match first character of C with first character
            // of A. If matches them move A to next
            if (i<A.length()&&A.charAt(i) == C.charAt(k))
                i++;

            // Else Match first character of C with first
            // character of B. If matches them move B to next
            else if (j<B.length()&&B.charAt(j) == C.charAt(k))
                j++;

            // If doesn't match with either A or B, then return
            // false
            else
                return false;

            // Move C to next for next iteration
            k++;
        }

        // If A or B still have some characters,
        // then length of C is smaller than sum
        // of lengths of A and B, so return false
        if (i < A.length() || j < B.length())
            return false;

        return true;
    }

    public static void main(String []args){

        String A = "AB";
        String B = "CD";
        String C = "ACBG";
        if (isInterleaved(A, B, C) == true)
            System.out.printf("%s is interleaved of %s and %s", C, A, B);
        else
            System.out.printf("%s is not interleaved of %s and %s", C, A, B);
    }
}

// This code is contributed by Rituraj Jain
```

## 计算机编程语言

```
# Python program to check if given string is an interleaving of
# the other two strings

# Returns true if C is an interleaving of A and B, otherwise
# returns false
def isInterleaved(A, B, C):

    # Utility variables
    i = 0
    j = 0
    k = 0

    # Iterate through all characters of C.
    while k != len(C)-1:

        # Match first character of C with first character of A,
        # If matches them move A to next
        if i<len(A) and A[i] == C[k]:
            i+=1

        # Else Match first character of C with first character
        # of B. If matches them move B to next
        elif j< len(B) and B[j] == C[k]:
            j+=1

        # If doesn't match with either A or B, then return false
        else:
            return 0

        # Move C to next for next iteration
        k+=1

    # If A or B still have some characters, then length of C is
    # smaller than sum of lengths of A and B, so return false
    if A[i-1] or B[j-1]:
        return 0

    return 1

# Driver program to test the above function
A = "AB"
B = "CD"
C = "ACBG"
if isInterleaved(A, B, C) == 1:
    print C + " is interleaved of " + A + " and " + B
else:
    print C + " is not interleaved of " + A + " and " + B

# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to check if the given string is
// an interleaving of the other two strings
using System;

class GfG
{

    // Returns true if C is an interleaving
    // of A and B, otherwise returns false
    static bool isInterleaved (String A, String B, String C)
    {
        int i = 0, j = 0, k = 0;

        // Iterate through all characters of C.
        while (k != C.Length - 1)
        {
            // Match first character of C with first character
            // of A. If matches them move A to next
            if (A[i] == C[k])
                i++;

            // Else Match first character of C with first
            // character of B. If matches them move B to next
            else if (B[j] == C[k])
                j++;

            // If doesn't match with either A or B, then return
            // false
            else
                return false;

            // Move C to next for next iteration
            k++;
        }

        // If A or B still have some characters,
        // then length of C is smaller than sum
        // of lengths of A and B, so return false
        if (i < A.Length || j < B.Length)
            return false;

        return true;
    }

    // Driver code
    public static void Main(String []args)
    {

        String A = "AB";
        String B = "CD";
        String C = "ACBG";
        if (isInterleaved(A, B, C) == true)
            Console.WriteLine("{0} is interleaved of {1} and {2}", C, A, B);
        else
            Console.WriteLine("{0} is not interleaved of {1} and {2}", C, A, B);
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if given string
// is an interleaving of the other two strings

// Returns true if C is an interleaving
// of A and B, otherwise returns false
function isInterleaved ($A, $B, $C)
{
    // Iterate through all characters of C.
    while ($C != 0)
    {
        // Match first character of C with
        // first character of A. If matches
        // them move A to next
        if ($A == $C)
            $A++;

        // Else Match first character of C
        // with first character of B. If
        // matches them move B to next
        else if ($B == $C)
            $B++;

        // If doesn't match with either
        // A or B, then return false
        else
            return false;

        // Move C to next for next iteration
        $C++;
    }

    // If A or B still have some characters,
    // then length of C is smaller than sum
    // of lengths of A and B, so return false
    if ($A || $B)
        return false;

    return true;
}

// Driver Code
$A = "AB";
$B = "CD";
$C = "ACBG";
if (isInterleaved($A, $B, $C) == true)
    echo $C . " is interleaved of " .
         $A . " and " . $B;
else
    echo $C . " is not interleaved of " .
         $A . " and " . $B;

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript program to check if the given string is 
// an interleaving of the other two strings     

    // Returns true if C is an interleaving 
    // of A and B, otherwise returns false 
    function isInterleaved (A,B,C)
    {
        let i = 0, j = 0, k = 0;

        // Iterate through all characters of C. 
        while (k != C.length)
        {

            // Match first character of C with first character 
            // of A. If matches them move A to next 
            if (i<A.length && A[i] == C[k])
            {
                i++;
            }

            // Else Match first character of C with first 
            // character of B. If matches them move B to next
            else if (j < B.length && B[j] == C[k])
            {
                j++; 
            }

            // If doesn't match with either A or B, then return 
            // false 
            else
            {
                return false;
            }

            // Move C to next for next iteration
            k++;
        }

        // If A or B still have some characters, 
        // then length of C is smaller than sum 
        // of lengths of A and B, so return false
        if (i < A.length || j < B.length)
        {
            return false;
        }
        return true; 
    }

    let A = "AB";
    let B = "CD"; 
    let C = "ACBG";
    if (isInterleaved(A, B, C) == true)
    {
        document.write(C+ " is interleaved of "+ A+" and ", B); 
    }
    else
    {
        document.write(C + " is not interleaved of "+ A +" and ", B);
    }

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
  ACBG is not interleaved of AB and CD
```

**时间复杂度:** O(m+n)，其中 m 和 n 分别是字符串 A 和 B 的长度。
注意，如果 A 和 B 有一些共同的特征，上述方法就不起作用了。例如，如果字符串 A =“AAB”，字符串 B =“AAC”和字符串 C =“AACAAB”，那么上述方法将返回 false。我们已经在这里讨论了[一个处理普通字符](https://www.geeksforgeeks.org/check-whether-a-given-string-is-an-interleaving-of-two-other-given-strings-set-2/)的扩展解决方案。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。