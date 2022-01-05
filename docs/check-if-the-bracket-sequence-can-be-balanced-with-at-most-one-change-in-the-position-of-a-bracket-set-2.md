# 检查支架顺序是否可以通过最多一次支架位置变化来平衡|设置 2

> 原文:[https://www . geeksforgeeks . org/check-if-the-bracket-sequence-最多可以用一个括号-set-2 的位置变化来平衡/](https://www.geeksforgeeks.org/check-if-the-bracket-sequence-can-be-balanced-with-at-most-one-change-in-the-position-of-a-bracket-set-2/)

给定一个括号序列作为字符串 **str** ，任务是找出给定的字符串是否可以通过最多将一个括号从序列中的原始位置移动到任何其他位置来平衡。
**例:**

> **输入:**str =(()”
> **输出:**是
> As 通过将 s[0]移动到最后将使其有效。
> "()"
> **输入:**str = "())(()"
> **输出:**否

**方法:**这个问题可以使用[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)来解决，如[这篇](https://www.geeksforgeeks.org/check-if-the-bracket-sequence-can-be-balanced-with-at-most-one-change-in-the-position-of-a-bracket/)帖子中所讨论的。在本文中，将讨论一种不使用额外空间的方法。
如果“(”的频率小于“)”的频率。如果上述差值大于 1，则序列不能被平衡，否则如果总差值为零，它可以被平衡。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if
// the string can be balanced
bool canBeBalanced(string s, int n)
{

    // Count to check the difference between
    // the frequencies of '(' and ')' and
    // count_1 is to find the minimum value
    // of freq('(') - freq(')')
    int count = 0, count_1 = 0;

    // Traverse the given string
    for (int i = 0; i < n; i++) {

        // Increase the count
        if (s[i] == '(')
            count++;

        // Decrease the count
        else
            count--;

        // Find the minimum value
        // of freq('(') - freq(')')
        count_1 = min(count_1, count);
    }

    // If the minimum difference is greater
    // than or equal to -1 and the overall
    // difference is zero
    if (count_1 >= -1 && count == 0)
        return true;

    return false;
}

// Driver code
int main()
{
    string s = "())()(";
    int n = s.length();

    if (canBeBalanced(s, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to toggle K-th bit of a number N
class GFG
{

// Function that returns true if
// the string can be balanced
static boolean canBeBalanced(String s, int n)
{

    // Count to check the difference between
    // the frequencies of '(' and ')' and
    // count_1 is to find the minimum value
    // of freq('(') - freq(')')
    int count = 0, count_1 = 0;

    // Traverse the given string
    for (int i = 0; i < n; i++)
    {

        // Increase the count
        if (s.charAt(i) == '(')
            count++;

        // Decrease the count
        else
            count--;

        // Find the minimum value
        // of freq('(') - freq(')')
        count_1 = Math.min(count_1, count);
    }

    // If the minimum difference is greater
    // than or equal to -1 and the overall
    // difference is zero
    if (count_1 >= -1 && count == 0)
        return true;

    return false;
}

// Driver code
public static void main(String []args)
{
    String s = "())()(";
    int n = s.length();

    if (canBeBalanced(s, n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if
# the can be balanced
def canBeBalanced(s, n):

    # Count to check the difference between
    # the frequencies of '(' and ')' and
    # count_1 is to find the minimum value
    # of freq('(') - freq(')')
    count = 0
    count_1 = 0

    # Traverse the given string
    for i in range(n):

        # Increase the count
        if (s[i] == '('):
            count += 1

        # Decrease the count
        else:
            count -= 1

        # Find the minimum value
        # of freq('(') - freq(')')
        count_1 = min(count_1, count)

    # If the minimum difference is greater
    # than or equal to -1 and the overall
    # difference is zero
    if (count_1 >= -1 and count == 0):
        return True

    return False

# Driver code
s = "())()("
n = len(s)

if (canBeBalanced(s, n)):
    print("Yes")
else:
    print("No")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to toggle K-th bit of a number N
using System;

class GFG
{

// Function that returns true if
// the string can be balanced
static Boolean canBeBalanced(String s, int n)
{

    // Count to check the difference between
    // the frequencies of '(' and ')' and
    // count_1 is to find the minimum value
    // of freq('(') - freq(')')
    int count = 0, count_1 = 0;

    // Traverse the given string
    for (int i = 0; i < n; i++)
    {

        // Increase the count
        if (s[i] == '(')
            count++;

        // Decrease the count
        else
            count--;

        // Find the minimum value
        // of freq('(') - freq(')')
        count_1 = Math.Min(count_1, count);
    }

    // If the minimum difference is greater
    // than or equal to -1 and the overall
    // difference is zero
    if (count_1 >= -1 && count == 0)
        return true;

    return false;
}

// Driver code
public static void Main(String []args)
{
    String s = "())()(";
    int n = s.Length;

    if (canBeBalanced(s, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find
// next greater number than N

// Function that returns true if
// the string can be balanced
function canBeBalanced( s, n)
{

    // Count to check the difference between
    // the frequencies of '(' and ')' and
    // count_1 is to find the minimum value
    // of freq('(') - freq(')')
    var count = 0, count_1 = 0;

    // Traverse the given string
    for (var i=0; i < n; i++) {

        // Increase the count
        if (s[i] == '(')
            count++;

        // Decrease the count
        else
            count--;

        // Find the minimum value
        // of freq('(') - freq(')')
        count_1 = Math.min(count_1, count);
    }

    // If the minimum difference is greater
    // than or equal to -1 and the overall
    // difference is zero
    if (count_1 >= -1 && count == 0)
        return true;

    return false;
}

var s = "())()(";
    var n = s.length;

    if (canBeBalanced(s, n))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed bby SoumikMondal

</script>
```

**Output:** 

```
Yes
```