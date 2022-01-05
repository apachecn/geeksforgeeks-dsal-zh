# 检查一个数的二进制等价物是否以给定的字符串结尾

> 原文:[https://www . geeksforgeeks . org/check-数字的二进制等价形式是否以给定字符串结尾/](https://www.geeksforgeeks.org/check-whether-the-binary-equivalent-of-a-number-ends-with-given-string-or-not/)

给定一个正整数 **N** ，任务是检查该整数的二进制等价物是否以给定的字符串 **str** 结束。
如果以“str”结尾，则打印“是”。否则，打印“否”。
**示例**:

> **输入:** N = 23，str = "111"
> **输出:**是
> **解释:**
> 23 的二进制= 10111，以“111”结束
> 
> **输入:** N = 5，str = " 111 "
> T3】输出:否

**逼近**:思路是找到 N 的[二进制等价物，检查 str 是否是其二进制等价物的后缀。](https://www.geeksforgeeks.org/program-decimal-binary-conversion/)

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function returns true if
// s1 is suffix of s2
bool isSuffix(string s1, string s2)
{
    int n1 = s1.length();
    int n2 = s2.length();
    if (n1 > n2)
        return false;
    for (int i = 0; i < n1; i++)
        if (s1[n1 - i - 1] != s2[n2 - i - 1])
            return false;
    return true;
}

// Function to check if binary equivalent
// of a number ends in "111" or not
bool CheckBinaryEquivalent(int N, string str)
{

    // To store the binary
    // number
    int B_Number = 0;
    int cnt = 0;

    while (N != 0) {

        int rem = N % 2;
        int c = pow(10, cnt);
        B_Number += rem * c;
        N /= 2;

        // Count used to store
        // exponent value
        cnt++;
    }

    string bin = to_string(B_Number);
    return isSuffix(str, bin);
}

// Driver code
int main()
{

    int N = 23;
    string str = "111";
    if (CheckBinaryEquivalent(N, str))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
class GFG{

// Function returns true if
// s1 is suffix of s2
static boolean isSuffix(String s1, String s2)
{
    int n1 = s1.length(),
        n2 = s2.length();

    if (n1 > n2)
        return false;

    for(int i = 0; i < n1; i++)
        if (s1.charAt(n1 - i - 1) !=
            s2.charAt(n2 - i - 1))
        return false;

    return true;
}

// Function to check if binary equivalent
// of a number ends in "111" or not
static boolean CheckBinaryEquivalent(int N,
                                     String str)
{

    // To store the binary
    // number
    int B_Number = 0;
    int cnt = 0;

    while (N != 0)
    {
        int rem = N % 2;
        int c = (int)Math.pow(10, cnt);
        B_Number += rem * c;
        N /= 2;

        // Count used to store
        // exponent value
        cnt++;
    }

    String bin = Integer.toString(B_Number);
    return isSuffix(str, bin);
}

// Driver code
public static void main(String[] args)
{
    int N = 23;
    String str = "111";

    if (CheckBinaryEquivalent(N, str))
        System.out.print("Yes\n");
    else
        System.out.print("No\n");
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function returns true if
# s1 is suffix of s2
def isSuffix(s1, s2):

    n1 = len(s1)
    n2 = len(s2)

    if(n1 > n2):
        return False
    for i in range(n1):

        if (s1[n1 - i - 1] !=
            s2[n2 - i - 1]):
            return False;
    return True;

# Function to check if
# binary equivalent of a
# number ends in "111" or not
def CheckBinaryEquivalent(N, s):

    # To store the binary
    # number
    B_Number = 0;
    cnt = 0;

    while (N != 0):

        rem = N % 2;
        c = pow(10, cnt);
        B_Number += rem * c;
        N //= 2;

        # Count used to store
        # exponent value
        cnt += 1;   

    bin = str(B_Number);   
    return isSuffix(s, bin);

# Driver code   
if __name__ == "__main__":

    N = 23;
    s = "111";

    if (CheckBinaryEquivalent(N, s)):
        print("Yes")
    else:
        print("No")

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation of the 
// above approach 
using System;
using System.Collections;

class GFG{

// Function returns true if
// s1 is suffix of s2
static bool isSuffix(String s1, String s2)
{
    int n1 = s1.Length,
        n2 = s2.Length;

    if (n1 > n2)
        return false;

    for(int i = 0; i < n1; i++)
        if (s1[n1 - i - 1] !=
            s2[n2 - i - 1])
        return false;

    return true;
}

// Function to check if binary equivalent
// of a number ends in "111" or not
static bool CheckBinaryEquivalent(int N,
                                  String str)
{

    // To store the binary
    // number
    int B_Number = 0;
    int cnt = 0;

    while (N != 0)
    {
        int rem = N % 2;
        int c = (int)Math.Pow(10, cnt);
        B_Number += rem * c;
        N /= 2;

        // Count used to store
        // exponent value
        cnt++;
    }
    String bin = B_Number.ToString();
    return isSuffix(str, bin);
}

// Driver Code
public static void Main (String[] args)
{
    int N = 23;
    String str = "111";

    if (CheckBinaryEquivalent(N, str))
        Console.WriteLine("Yes\n");
    else
        Console.WriteLine("No\n");
}
}

// This code is contributed by jana_sayantan
```

## java 描述语言

```
<script>

// Javascript implementation of the
// above approach

// Function returns true if
// s1 is suffix of s2
function isSuffix(s1, s2)
{
    var n1 = s1.length;
    var n2 = s2.length;
    if (n1 > n2)
        return false;
    for (var i = 0; i < n1; i++)
        if (s1[n1 - i - 1] != s2[n2 - i - 1])
            return false;
    return true;
}

// Function to check if binary equivalent
// of a number ends in "111" or not
function CheckBinaryEquivalent(N, str)
{

    // To store the binary
    // number
    var B_Number = 0;
    var cnt = 0;

    while (N != 0) {

        var rem = N % 2;
        var c = Math.pow(10, cnt);
        B_Number += rem * c;
        N = parseInt(N/2);

        // Count used to store
        // exponent value
        cnt++;
    }

    var bin = B_Number.toString();
    return isSuffix(str, bin);
}

// Driver code
var N = 23;
var str = "111";
if (CheckBinaryEquivalent(N, str))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(|str)*

***辅助空间:** O(1)*