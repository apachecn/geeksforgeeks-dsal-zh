# 检查字符串是否由 K 个交替字符组成

> 原文:[https://www . geesforgeks . org/check-if-a-string-is-由 k 个交替字符组成/](https://www.geeksforgeeks.org/check-if-a-string-is-made-up-of-k-alternating-characters/)

给定一个字符串 **str** 和一个整数 **K** ，任务是检查它是否由 **K** 交替字符组成。
**举例:**

> **输入:** str = "acdeac "，K = 4
> **输出:**是
> **输入:**str = " abcdab "，K = 2
> **输出:**否

**方法:**为了使字符串由 K 个交替字符组成，它必须满足以下条件:

1.  **(i + mK)** 索引处的所有字符必须相同，其中 **i** 是当前索引， **mK** 代表 K 的 m <sup>次</sup>次倍数，这意味着每 K 个索引后，字符必须重复。
2.  相邻字符不能相同。这是因为如果字符串是“AAAAA”类型的，其中单个字符重复任何次数，上述条件将得到匹配，但在这种情况下，答案必须是“否”。
    下面的代码是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a string
// is made up of k alternating characters
bool isKAlternating(string s, int k)
{
    if (s.length() < k)
        return false;

    int checker = 0;

    // Check if all the characters at
    // indices 0 to K-1 are different
    for (int i = 0; i < k; i++) {

        int bitAtIndex = s[i] - 'a';

        // If that bit is already set in
        // checker, return false
        if ((checker & (1 << bitAtIndex)) > 0) {
            return false;
        }

        // Otherwise update and continue by
        // setting that bit in the checker
        checker = checker | (1 << bitAtIndex);
    }

    for (int i = k; i < s.length(); i++)
        if (s[i - k] != s[i])
            return false;

    return true;
}

// Driver code
int main()
{
    string str = "acdeac";
    int K = 4;

    if (isKAlternating(str, K))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG{

// Function to check if a String
// is made up of k alternating characters
static boolean isKAlternating(String s, int k)
{
    if (s.length() < k)
        return false;

    int checker = 0;

    // Check if all the characters at
    // indices 0 to K-1 are different
    for (int i = 0; i < k; i++) {

        int bitAtIndex = s.charAt(i) - 'a';

        // If that bit is already set in
        // checker, return false
        if ((checker & (1 << bitAtIndex)) > 0) {
            return false;
        }

        // Otherwise update and continue by
        // setting that bit in the checker
        checker = checker | (1 << bitAtIndex);
    }

    for (int i = k; i < s.length(); i++)
        if (s.charAt(i - k) != s.charAt(i) )
            return false;

    return true;
}

// Driver code
public static void main(String[] args)
{
    String str = "acdeac";
    int K = 4;

    if (isKAlternating(str, K))
        System.out.print("Yes" +"\n");
    else
        System.out.print("No" +"\n");
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to check if a string
# is made up of k alternating characters
def isKAlternating( s, k):
    if (len(s) < k):
        return False

    checker = 0

    # Check if all the characters at
    # indices 0 to K-1 are different
    for i in range( k):

        bitAtIndex = ord(s[i]) - ord('a')

        # If that bit is already set in
        # checker, return false
        if ((checker & (1 << bitAtIndex)) > 0):
            return False

        # Otherwise update and continue by
        # setting that bit in the checker
        checker = checker | (1 << bitAtIndex)

    for i in range(k,len(s)):
        if (s[i - k] != s[i]):
            return False

    return True

# Driver code
if __name__ =="__main__":

    st = "acdeac"
    K = 4

    if (isKAlternating(st, K)):
        print ("Yes")
    else:
        print ("No")

# This code is contributed by chitranayal  
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Function to check if a String
// is made up of k alternating characters
static bool isKAlternating(String s, int k)
{
    if (s.Length < k)
        return false;

    int checker = 0;

    // Check if all the characters at
    // indices 0 to K-1 are different
    for (int i = 0; i < k; i++) {

        int bitAtIndex = s[i] - 'a';

        // If that bit is already set in
        // checker, return false
        if ((checker & (1 << bitAtIndex)) > 0) {
            return false;
        }

        // Otherwise update and continue by
        // setting that bit in the checker
        checker = checker | (1 << bitAtIndex);
    }

    for (int i = k; i < s.Length; i++)
        if (s[i - k] != s[i] )
            return false;

    return true;
}

// Driver code
public static void Main()
{
    String str = "acdeac";
    int K = 4;

    if (isKAlternating(str, K))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This article contributed by AbhiThakur
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to check if a string
// is made up of k alternating characters
function isKAlternating(s, k)
{
    if (s.length < k)
        return false;

    var checker = 0;

    // Check if all the characters at
    // indices 0 to K-1 are different
    for (var i = 0; i < k; i++) {

        var bitAtIndex = s[i].charCodeAt(0) - 'a'.charCodeAt(0);

        // If that bit is already set in
        // checker, return false
        if ((checker & (1 << bitAtIndex)) > 0) {
            return false;
        }

        // Otherwise update and continue by
        // setting that bit in the checker
        checker = checker | (1 << bitAtIndex);
    }

    for (var i = k; i < s.length; i++)
        if (s[i - k] != s[i])
            return false;

    return true;
}

// Driver code
var str = "acdeac";
var K = 4;
if (isKAlternating(str, K))
    document.write( "Yes" );
else
    document.write( "No" );

// This code is contributed by importantly.
</script>
```

**Output:** 

```
Yes
```

1.  ***时间复杂度:**O(N)*T4】