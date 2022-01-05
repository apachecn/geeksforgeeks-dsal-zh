# 将 X 混排后发现 Y 中是否存在 X

> 原文:[https://www . geesforgeks . org/find-when-x-exists-in-y-after-jumbling-x/](https://www.geeksforgeeks.org/find-whether-x-exists-in-y-after-jumbling-x/)

给定两个包含小写字母的字符串 **X** 和 **Y** ，任务是检查字符串 **X** 的任何排列是否作为其子字符串存在于 **Y** 中。

**示例:**

> **输入:**X =“skege”，Y =“geeks forgeks”
> **输出:**是
> “geeks”是 X 的一个排列，
> 在 Y 中作为一个子串出现
> 
> **输入:**X =“AABB”，Y =“bbbbbbb”
> T3】输出:否

**方法:**这个问题可以使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)解决。

*   计算字符串 **X** 每个字符的频率计数，并将其存储在一个数组中，比如 **cnt_X[]** 。
*   现在对于子串**Y【I……(I+x . length()-1)】**，可以生成同频数组比如**CNT【】**。
*   使用步骤 2 中的数组，通过将**CNT[Y[I]–‘a’]**递减 **1** 并将**CNT[Y[I+x . length()]–‘a’]**递增 **1** ，可以在 O(1)时间内计算出下一个窗口的频率计数。
*   比较每个窗口的 **cnt[]** 和 **cnt_X[]** 。如果两者相等，那么找到了匹配。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 26;

// Function that returns true if both
// the arrays have equal values
bool areEqual(int* a, int* b)
{
    // Test the equality
    for (int i = 0; i < MAX; i++)
        if (a[i] != b[i])
            return false;
    return true;
}

// Function that returns true if any permutation
// of X exists as a substring in Y
bool xExistsInY(string x, string y)
{

    // Base case
    if (x.size() > y.size())
        return false;

    // To store cumulative frequency
    int cnt_x[MAX] = { 0 };
    int cnt[MAX] = { 0 };

    // Finding the frequency of
    // characters in X
    for (int i = 0; i < x.size(); i++)
        cnt_x[x[i] - 'a']++;

    // Finding the frequency of characters
    // in Y upto the length of X
    for (int i = 0; i < x.size(); i++)
        cnt[y[i] - 'a']++;

    // Equality check
    if (areEqual(cnt_x, cnt))
        return true;

    // Two pointer approach to generate the
    // entire cumulative frequency
    for (int i = 1; i < y.size() - x.size() + 1; i++) {

        // Remove the first character of
        // the previous window
        cnt[y[i - 1] - 'a']--;

        // Add the last character of
        // the current window
        cnt[y[i + x.size() - 1] - 'a']++;

        // Equality check
        if (areEqual(cnt, cnt_x))
            return true;
    }

    return false;
}

// Driver code
int main()
{
    string x = "skege";
    string y = "geeksforgeeks";

    if (xExistsInY(x, y))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int MAX = 26;

// Function that returns true if both
// the arrays have equal values
static boolean areEqual(int []a, int []b)
{
    // Test the equality
    for (int i = 0; i < MAX; i++)
        if (a[i] != b[i])
            return false;
    return true;
}

// Function that returns true if
// any permutation of X exists
// as a subString in Y
static boolean xExistsInY(String x, String y)
{

    // Base case
    if (x.length() > y.length())
        return false;

    // To store cumulative frequency
    int []cnt_x = new int[MAX];
    int []cnt = new int[MAX];

    // Finding the frequency of
    // characters in X
    for (int i = 0; i < x.length(); i++)
        cnt_x[x.charAt(i) - 'a']++;

    // Finding the frequency of characters
    // in Y upto the length of X
    for (int i = 0; i < x.length(); i++)
        cnt[y.charAt(i) - 'a']++;

    // Equality check
    if (areEqual(cnt_x, cnt))
        return true;

    // Two pointer approach to generate the
    // entire cumulative frequency
    for (int i = 1; i < y.length() -
                        x.length() + 1; i++)
    {

        // Remove the first character of
        // the previous window
        cnt[y.charAt(i - 1) - 'a']--;

        // Add the last character of
        // the current window
        cnt[y.charAt(i + x.length() - 1) - 'a']++;

        // Equality check
        if (areEqual(cnt, cnt_x))
            return true;
    }
    return false;
}

// Driver code
public static void main(String[] args)
{
    String x = "skege";
    String y = "geeksforgeeks";

    if (xExistsInY(x, y))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 26

# Function that returns true if both
# the arrays have equal values
def areEqual(a, b):

    # Test the equality
    for i in range(MAX):
        if (a[i] != b[i]):
            return False
    return True

# Function that returns true if any permutation
# of X exists as a sub in Y
def xExistsInY(x,y):

    # Base case
    if (len(x) > len(y)):
        return False

    # To store cumulative frequency
    cnt_x = [0] * MAX
    cnt = [0] * MAX

    # Finding the frequency of
    # characters in X
    for i in range(len(x)):
        cnt_x[ord(x[i]) - ord('a')] += 1;

    # Finding the frequency of characters
    # in Y upto the length of X
    for i in range(len(x)):
        cnt[ord(y[i]) - ord('a')] += 1

    # Equality check
    if (areEqual(cnt_x, cnt)):
        return True

    # Two pointer approach to generate the
    # entire cumulative frequency
    for i in range(1, len(y) - len(x) + 1):

        # Remove the first character of
        # the previous window
        cnt[ord(y[i - 1]) - ord('a')] -= 1

        # Add the last character of
        # the current window
        cnt[ord(y[i + len(x) - 1]) - ord('a')] += 1

        # Equality check
        if (areEqual(cnt, cnt_x)):
            return True

    return False

# Driver Code
if __name__ == '__main__':
    x = "skege"
    y = "geeksforgeeks"

    if (xExistsInY(x, y)):
        print("Yes")
    else:
        print("No")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int MAX = 26;

// Function that returns true if both
// the arrays have equal values
static bool areEqual(int []a,
                     int []b)
{
    // Test the equality
    for (int i = 0; i < MAX; i++)
        if (a[i] != b[i])
            return false;
    return true;
}

// Function that returns true if
// any permutation of X exists
// as a subString in Y
static bool xExistsInY(String x,
                       String y)
{

    // Base case
    if (x.Length > y.Length)
        return false;

    // To store cumulative frequency
    int []cnt_x = new int[MAX];
    int []cnt = new int[MAX];

    // Finding the frequency of
    // characters in X
    for (int i = 0; i < x.Length; i++)
        cnt_x[x[i] - 'a']++;

    // Finding the frequency of characters
    // in Y upto the length of X
    for (int i = 0; i < x.Length; i++)
        cnt[y[i] - 'a']++;

    // Equality check
    if (areEqual(cnt_x, cnt))
        return true;

    // Two pointer approach to generate the
    // entire cumulative frequency
    for (int i = 1; i < y.Length -
                        x.Length + 1; i++)
    {

        // Remove the first character of
        // the previous window
        cnt[y[i - 1] - 'a']--;

        // Add the last character of
        // the current window
        cnt[y[i + x.Length - 1] - 'a']++;

        // Equality check
        if (areEqual(cnt, cnt_x))
            return true;
    }
    return false;
}

// Driver code
public static void Main(String[] args)
{
    String x = "skege";
    String y = "geeksforgeeks";

    if (xExistsInY(x, y))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var MAX = 26;

// Function that returns true if both
// the arrays have equal values
function areEqual(a, b)
{
    // Test the equality
    for (var i = 0; i < MAX; i++)
        if (a[i] != b[i])
            return false;
    return true;
}

// Function that returns true if any permutation
// of X exists as a substring in Y
function xExistsInY(x, y)
{

    // Base case
    if (x.length > y.length)
        return false;

    // To store cumulative frequency
    var cnt_x = Array(MAX).fill(0);
    var cnt = Array(MAX).fill(0);

    // Finding the frequency of
    // characters in X
    for (var i = 0; i < x.length; i++)
        cnt_x[x[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

    // Finding the frequency of characters
    // in Y upto the length of X
    for (var i = 0; i < x.length; i++)
        cnt[y[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

    // Equality check
    if (areEqual(cnt_x, cnt))
        return true;

    // Two pointer approach to generate the
    // entire cumulative frequency
    for (var i = 1; i < y.length - x.length + 1; i++) {

        // Remove the first character of
        // the previous window
        cnt[y[i - 1].charCodeAt(0) - 'a'.charCodeAt(0)]--;

        // Add the last character of
        // the current window
        cnt[y[i + x.length - 1].charCodeAt(0) - 'a'.charCodeAt(0)]++;

        // Equality check
        if (areEqual(cnt, cnt_x))
            return true;
    }

    return false;
}

// Driver code
var x = "skege";
var y = "geeksforgeeks";
if (xExistsInY(x, y))
    document.write( "Yes");
else
    document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(xLen + yLen)，其中 xLen 和 yLen 分别是字符串 X 和 Y 的长度。