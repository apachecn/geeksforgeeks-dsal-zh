# 异或两个不等长的二进制字符串

> 原文:[https://www . geeksforgeeks . org/xor-二进制不等长字符串/](https://www.geeksforgeeks.org/xor-two-binary-strings-of-unequal-lengths/)

给定两个不等长的二进制串 **A** 和 **B** ，任务是打印二进制串，该二进制串是 **A** 和 **B** 的异或。
**示例:**

> **输入:** A = "11001 "，B = " 11111 "
> **输出:** 100110
> **输入:** A = "11111 "，B = "0"
> **输出:** 11111

**做法:**思路是先使两个字符串长度相等，然后对每个字符逐一进行 XOR 运算，存储到结果字符串中。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to insert n 0s in the
// beginning of the given string
void addZeros(string& str, int n)
{
    for (int i = 0; i < n; i++) {
        str = "0" + str;
    }
}

// Function to return the XOR
// of the given strings
string getXOR(string a, string b)
{

    // Lengths of the given strings
    int aLen = a.length();
    int bLen = b.length();

    // Make both the strings of equal lengths
    // by inserting 0s in the beginning
    if (aLen > bLen) {
        addZeros(b, aLen - bLen);
    }
    else if (bLen > aLen) {
        addZeros(a, bLen - aLen);
    }

    // Updated length
    int len = max(aLen, bLen);

    // To store the resultant XOR
    string res = "";
    for (int i = 0; i < len; i++) {
        if (a[i] == b[i])
            res += "0";
        else
            res += "1";
    }

    return res;
}

// Driver code
int main()
{
    string a = "11001", b = "111111";

    cout << getXOR(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to insert n 0s in the
    // beginning of the given string
    static String addZeros(String str, int n)
    {
        for (int i = 0; i < n; i++)
        {
            str = "0" + str;
        }
        return str;
    }

    // Function to return the XOR
    // of the given strings
    static String getXOR(String a, String b)
    {

        // Lengths of the given strings
        int aLen = a.length();
        int bLen = b.length();

        // Make both the strings of equal lengths
        // by inserting 0s in the beginning
        if (aLen > bLen)
        {
            a = addZeros(b, aLen - bLen);
        }
        else if (bLen > aLen)
        {
            a = addZeros(a, bLen - aLen);
        }

        // Updated length
        int len = Math.max(aLen, bLen);

        // To store the resultant XOR
        String res = "";

        for (int i = 0; i < len; i++)
        {
            if (a.charAt(i) == b.charAt(i))
                res += "0";
            else
                res += "1";
        }
        return res;
    }

    // Driver code
    public static void main (String[] args)
    {
        String a = "11001", b = "111111";

        System.out.println(getXOR(a, b));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to insert n 0s in the
# beginning of the given string
def addZeros(strr, n):
    for i in range(n):
        strr = "0" + strr
    return strr

# Function to return the XOR
# of the given strings
def getXOR(a, b):

    # Lengths of the given strings
    aLen = len(a)
    bLen = len(b)

    # Make both the strings of equal lengths
    # by inserting 0s in the beginning
    if (aLen > bLen):
        b = addZeros(b, aLen - bLen)
    elif (bLen > aLen):
        a = addZeros(a, bLen - aLen)

    # Updated length
    lenn = max(aLen, bLen);

    # To store the resultant XOR
    res = ""
    for i in range(lenn):
        if (a[i] == b[i]):
            res += "0"
        else:
            res += "1"

    return res

# Driver code
a = "11001"
b = "111111"

print(getXOR(a, b))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to insert n 0s in the
    // beginning of the given string
    static String addZeros(String str, int n)
    {
        for (int i = 0; i < n; i++)
        {
            str = "0" + str;
        }
        return str;
    }

    // Function to return the XOR
    // of the given strings
    static String getXOR(String a, String b)
    {

        // Lengths of the given strings
        int aLen = a.Length;
        int bLen = b.Length;

        // Make both the strings of equal lengths
        // by inserting 0s in the beginning
        if (aLen > bLen)
        {
            a = addZeros(b, aLen - bLen);
        }
        else if (bLen > aLen)
        {
            a = addZeros(a, bLen - aLen);
        }

        // Updated length
        int len = Math.Max(aLen, bLen);

        // To store the resultant XOR
        String res = "";

        for (int i = 0; i < len; i++)
        {
            if (a[i] == b[i])
                res += "0";
            else
                res += "1";
        }
        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String a = "11001", b = "111111";

        Console.WriteLine(getXOR(a, b));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to insert n 0s in the
    // beginning of the given string
    function addZeros(str, n)
    {
        for (let i = 0; i < n; i++)
        {
            str = "0" + str;
        }
        return str;
    }

    // Function to return the XOR
    // of the given strings
    function getXOR(a, b)
    {

        // Lengths of the given strings
        let aLen = a.length;
        let bLen = b.length;

        // Make both the strings of equal lengths
        // by inserting 0s in the beginning
        if (aLen > bLen)
        {
            a = addZeros(b, aLen - bLen);
        }
        else if (bLen > aLen)
        {
            a = addZeros(a, bLen - aLen);
        }

        // Updated length
        let len = Math.max(aLen, bLen);

        // To store the resultant XOR
        let res = "";

        for (let i = 0; i < len; i++)
        {
            if (a[i] == b[i])
                res += "0";
            else
                res += "1";
        }
        return res;
    }

    let a = "11001", b = "111111";

      document.write(getXOR(a, b));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
100110
```

**时间复杂度:** O(len)，len=Max(长度 a，长度 b)

**辅助空间:** O(镜头)