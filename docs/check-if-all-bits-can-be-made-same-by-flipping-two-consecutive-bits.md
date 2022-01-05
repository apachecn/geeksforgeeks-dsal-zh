# 通过翻转两个连续的位来检查是否所有的位都是相同的

> 原文:[https://www . geesforgeks . org/check-if-all-bits-可以通过翻转两个连续的位来制造相同的位/](https://www.geeksforgeeks.org/check-if-all-bits-can-be-made-same-by-flipping-two-consecutive-bits/)

给定一个二进制字符串，任务是通过将两个连续的位翻转任意多次来确定该字符串的所有数字是否相等，即 0 或 1。
**例:**

```
Input: 01011
Output: YES
Explanation:
Flip 2nd and 3rd bit -> 00111, 
again flipping 1'st and 2'nd bit -> 11111

Input: 100011
Output: NO
Explanation:
No number of moves can ever 
equalize all elements of the array.
```

**方法:**
仔细观察，第 I 位和第 j 位的切换可以通过从第 I 位开始切换来完成，比如(I，i+1)，(i+1，i+2) …。(j-1，j)这里，除了 I 和 j 之外，每个位都切换两次(如果位切换两次，则它到达初始值)，然后最终第 I 位和第 j 位切换。因此，可以说，当 1 和 0 的计数都是奇数时，不可能使二进制字符串中的所有数字相等。
以下是上述办法的实施:

## C++

```
// C++ program for the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if
// Binary string can be
// made equal
string canMake(string& s)
{

    int o = 0, z = 0;

    // Counting occurence of
    // zero and one in binary
    // string
    for (int i = 0; i < s.size(); i++) {
        if (s[i] - '0' == 1)
            o++;
        else
            z++;
    }

    // From above observation
    if (o % 2 == 1 && z % 2 == 1)
        return "NO";
    else
        return "YES";
}

// Driver code
int main()
{

    string s = "01011";
    cout << canMake(s) << '\n';
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

    // Function to check if
    // Binary string can be
    // made equal
    static String canMake(String s)
    {

        int o = 0, z = 0;

        // Counting occurence of
        // zero and one in binary
        // string
        for (int i = 0; i < s.length(); i++)
        {
            if (s.charAt(i) - '0' == 1)
                o++;
            else
                z++;
        }

        // From above observation
        if (o % 2 == 1 && z % 2 == 1)
            return "NO";
        else
            return "YES";
    }

    // Driver code
    public static void main (String[] args)
    {

        String s = "01011";
        System.out.println(canMake(s)) ;

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if
# Binary string can be
# made equal
def canMake(s) :

    o = 0; z = 0;

    # Counting occurence of
    # zero and one in binary
    # string
    for i in range(len(s)) :
        if (ord(s[i]) - ord('0') == 1) :
            o += 1;
        else :
            z += 1;

    # From above observation
    if (o % 2 == 1 and z % 2 == 1) :
        return "NO";
    else :
        return "YES";

# Driver code
if __name__ == "__main__" :

    s = "01011";
    print(canMake(s));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    // Function to check if
    // Binary string can be
    // made equal
    static string canMake(string s)
    {

        int o = 0, z = 0;

        // Counting occurence of
        // zero and one in binary
        // string
        for (int i = 0; i < s.Length; i++)
        {
            if (s[i] - '0' == 1)
                o++;
            else
                z++;
        }

        // From above observation
        if (o % 2 == 1 && z % 2 == 1)
            return "NO";
        else
            return "YES";
    }

    // Driver code
    public static void Main()
    {
        string s = "01011";
        Console.WriteLine(canMake(s)) ;
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to check if
// Binary string can be
// made equal
function canMake(s)
{

    var o = 0, z = 0;

    // Counting occurence of
    // zero and one in binary
    // string
    for (i = 0; i < s.length; i++)
    {
        if (s.charAt(i).charCodeAt(0) - '0'.charCodeAt(0) == 1)
            o++;
        else
            z++;
    }

    // From above observation
    if (o % 2 == 1 && z % 2 == 1)
        return "NO";
    else
        return "YES";
}

// Driver code
var s = "01011";
document.write(canMake(s)) ;

// This code is contributed by Rajput-Ji

</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(n)，其中 n 是给定二进制数的长度