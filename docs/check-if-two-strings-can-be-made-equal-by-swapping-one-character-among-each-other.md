# 通过相互交换一个字符来检查两个字符串是否相等

> 原文:[https://www . geeksforgeeks . org/check-if-two-string-可以通过相互交换一个字符来使其相等/](https://www.geeksforgeeks.org/check-if-two-strings-can-be-made-equal-by-swapping-one-character-among-each-other/)

给定两个长度为 **N** 的字符串 **A** 和 **B** ，任务是通过将 **A** 的任何字符与 **B** 的任何其他字符仅交换一次来检查这两个字符串是否可以相等。
**举例:**

> **输入:**A =“seeksforgeks”，B =“geesforgeek”
> **输出:**是
> “**S**eeksforgeks”和“geesforgeek**G**”
> 可以对调，使两个字符串相等。
> **输入:** A = "GEEKSFORGEEKS "，B = " supersperbsite "
> **输出:**否

**方法:**首先省略两个字符串中相同且索引相同的元素。然后，如果新字符串的长度为 2，并且每个字符串中的元素都相同，那么只有交换是可能的。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the string
// can be made equal after one swap
bool canBeEqual(string a, string b, int n)
{
    // A and B are new a and b
    // after we omit the same elements
    vector<char> A, B;

    // Take only the characters which are
    // different in both the strings
    // for every pair of indices
    for (int i = 0; i < n; i++)
    {

        // If the current characters differ
        if (a[i]!= b[i])
        {
            A.push_back(a[i]);
            B.push_back(b[i]);
        }
    }

    // The strings were already equal
    if (A.size() == B.size() and
        B.size() == 0)
        return true;

    // If the lengths of the
    // strings are two
    if (A.size() == B.size() and
        B.size() == 2)
    {

        // If swapping these characters
        // can make the strings equal
        if (A[0] == A[1] and B[0] == B[1])
            return true;
    }
    return false;
}

// Driver code
int main()
{
    string A = "SEEKSFORGEEKS";
    string B = "GEEKSFORGEEKG";

    if (canBeEqual(A, B, A.size()))
        printf("Yes");
    else
        printf("No");
}

// This code is contributed by Mohit Kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

// Function that returns true if the string
// can be made equal after one swap
static boolean canBeEqual(char []a,
                          char []b, int n)
{
    // A and B are new a and b
    // after we omit the same elements
    Vector<Character> A = new Vector<>();
    Vector<Character> B = new Vector<>();

    // Take only the characters which are
    // different in both the strings
    // for every pair of indices
    for (int i = 0; i < n; i++)
    {

        // If the current characters differ
        if (a[i] != b[i])
        {
            A.add(a[i]);
            B.add(b[i]);
        }
    }

    // The strings were already equal
    if (A.size() == B.size() &&
        B.size() == 0)
        return true;

    // If the lengths of the
    // strings are two
    if (A.size() == B.size() &&
        B.size() == 2)
    {

        // If swapping these characters
        // can make the strings equal
        if (A.get(0) == A.get(1) &&
            B.get(0) == B.get(1))
            return true;
    }
    return false;
}

// Driver code
public static void main(String[] args)
{
    char []A = "SEEKSFORGEEKS".toCharArray();
    char []B = "GEEKSFORGEEKG".toCharArray();

    if (canBeEqual(A, B, A.length))
        System.out.printf("Yes");
    else
        System.out.printf("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if the string
# can be made equal after one swap
def canBeEqual(a, b, n):
    # A and B are new a and b
    # after we omit the same elements
    A =[]
    B =[]

    # Take only the characters which are
    # different in both the strings
    # for every pair of indices
    for i in range(n):

        # If the current characters differ
        if a[i]!= b[i]:
            A.append(a[i])
            B.append(b[i])

    # The strings were already equal
    if len(A)== len(B)== 0:
        return True

    # If the lengths of the
    # strings are two
    if len(A)== len(B)== 2:

        # If swapping these characters
        # can make the strings equal
        if A[0]== A[1] and B[0]== B[1]:
            return True

    return False

# Driver code
A = 'SEEKSFORGEEKS'
B = 'GEEKSFORGEEKG'

if (canBeEqual(A, B, len(A))):
    print("Yes")
else:
    print("No")
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function that returns true if the string
// can be made equal after one swap
static Boolean canBeEqual(char []a,
                          char []b, int n)
{
    // A and B are new a and b
    // after we omit the same elements
    List<char> A = new List<char>();
    List<char> B = new List<char>();

    // Take only the characters which are
    // different in both the strings
    // for every pair of indices
    for (int i = 0; i < n; i++)
    {

        // If the current characters differ
        if (a[i] != b[i])
        {
            A.Add(a[i]);
            B.Add(b[i]);
        }
    }

    // The strings were already equal
    if (A.Count == B.Count &&
        B.Count == 0)
        return true;

    // If the lengths of the
    // strings are two
    if (A.Count == B.Count &&
        B.Count == 2)
    {

        // If swapping these characters
        // can make the strings equal
        if (A[0] == A[1] &&
            B[0] == B[1])
            return true;
    }
    return false;
}

// Driver code
public static void Main(String[] args)
{
    char []A = "SEEKSFORGEEKS".ToCharArray();
    char []B = "GEEKSFORGEEKG".ToCharArray();

    if (canBeEqual(A, B, A.Length))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function that returns true if the string
// can be made equal after one swap
function canBeEqual(a,b,n)
{
    // A and B are new a and b
    // after we omit the same elements
    let A = [];
    let B = [];

    // Take only the characters which are
    // different in both the strings
    // for every pair of indices
    for (let i = 0; i < n; i++)
    {

        // If the current characters differ
        if (a[i] != b[i])
        {
            A.push(a[i]);
            B.push(b[i]);
        }
    }

    // The strings were already equal
    if (A.length == B.length &&
        B.length == 0)
        return true;

    // If the lengths of the
    // strings are two
    if (A.length == B.length &&
        B.length == 2)
    {

        // If swapping these characters
        // can make the strings equal
        if (A[0] == A[1] &&
            B[0] == B[1])
            return true;
    }
    return false;
}
// Driver code
let A = "SEEKSFORGEEKS".split("");
let B = "GEEKSFORGEEKG".split("");

if (canBeEqual(A, B, A.length))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
Yes
```