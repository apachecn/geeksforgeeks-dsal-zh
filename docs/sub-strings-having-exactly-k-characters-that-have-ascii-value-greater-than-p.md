# 【ASCII 值大于 p 的正好为 k 个字符的子字符串

> 原文:[https://www . geesforgeks . org/sub-strings-具有-恰好-k-字符-具有-ascii-value-大于-p/](https://www.geeksforgeeks.org/sub-strings-having-exactly-k-characters-that-have-ascii-value-greater-than-p/)

给定一个字符串“str”，两个整数“k”和“p”。任务是统计“str”的所有子字符串，这些子字符串包含 ASCII 值大于“p”的“k”字符。
**例:**

> **输入:** str = "abcd "，k=2，p=98
> **输出:** 3
> 只有字符‘c’和‘d’的 ASCII 值大于 98，
> 并且，包含它们的子字符串是“abcd”、“bcd”和“cd”。
> **输入:** str = "sabrcd "，k=5，p=80
> **输出:** 2

**方法:**我们只需要遍历所有索引，取所有可能长度的子串，然后只需检查子串是否正好有 ASCII 值大于‘p’的‘k’个字符。

> 将一个字符类型转换为 int 将给出它的 ASCII 值，即 int ascii = (int) char。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that checks if
// the string contain exactly
// K characters having ASCII
// value greater than p
bool isValidSubString(string r, int K, int p)
{
    int c = 0;

    for (int i = 0; i < r.length(); i++) {

        // if ASCII value is
        // greater than 'p'
        if ((int)r[i] > p)
            c++;
    }

    // if count of satisfying
    // characters is equal to 'K'
    // then return true
    if (c == K)
        return true;

    // otherwise return false
    else
        return false;
}

// function to count sub-strings
void countSubStrings(string s, int K, int p)
{
    // length of the string
    int l = s.length();

    // count of sub-strings
    int count = 0;

    // 'i' is the starting
    // index for the sub-string
    for (int i = 0; i < l; i++) {

        // 'j' is the no. of characters
        // to include in the sub-string
        for (int j = K; (i + j) <= l; j++) {
            string r = s.substr(i, j);

            // check if the sub-string
            // satisfies the condition
            if (isValidSubString(r, K, p))
                count++;
        }
    }

    cout << count << "\n";
}

// Driver code
int main()
{

    string s = "abepztydba";
    int K = 4;
    int p = 110;

    countSubStrings(s, K, p);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function that checks if
    // the String contain exactly
    // K characters having ASCII
    // value greater than p
    boolean isValidSubString(String r, int K, int p)
    {
        int c = 0;

        for (int i = 0; i < r.length(); i++) {

            // if ASCII value is
            // greater than 'p'
            if ((int)r.charAt(i) > p) {
                c++;
            }
        }

        // if count of satisfying
        // characters is equal to 'K'
        // then return true
        if (c == K) {
            return true;
        }

        // otherwise return false
        else {
            return false;
        }
    }

    // function to count sub-Strings
    void countSubStrings(String s, int K, int p)
    {
        // length of the String
        int l = s.length();

        // count of sub-Strings
        int count = 0;

        // 'i' is the starting
        // index for the sub-String
        for (int i = 0; i < l; i++) {

            // 'j' is the no. of characters
            // to include in the sub-String
            for (int j = K; (i + j) <= l; j++) {

                String r = s.substring(i, (i + j));

                // check if the sub-String
                // satisfies the condition
                if (isValidSubString(r, K, p)) {
                    count++;
                }
            }
        }
        System.out.println(count);
    }

    // Driver code
    public static void main(String args[])
    {
        GFG g = new GFG();
        String s = "abepztydba";
        int K = 4;
        int p = 110;

        g.countSubStrings(s, K, p);
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that checks if the string
# contain exactly K characters having
# ASCII value greater than p
def isValidSubString(r, K, p):

    c = 0
    for i in range(0, len(r)):

        # if ASCII value is
        # greater than 'p'
        if ord(r[i]) > p:
            c += 1

    # if count of satisfying
    # characters is equal to 'K'
    # then return true
    if c == K:
        return True

    # otherwise return false
    else:
        return False

# function to count sub-strings
def countSubStrings(s, K, p):

    # length of the string
    l = len(s)

    # count of sub-strings
    count = 0

    # 'i' is the starting
    # index for the sub-string
    for i in range(0, l):

        # 'j' is the no. of characters
        # to include in the sub-string
        for j in range(K, l - i + 1):
            r = s[i:i + j]

            # check if the sub-string
            # satisfies the condition
            if isValidSubString(r, K, p) == True:
                count += 1

    print(count)

# Driver code
if __name__ == "__main__":

    s = "abepztydba"
    K, p = 4, 110

    countSubStrings(s, K, p)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function that checks if
    // the String contain exactly
    // K characters having ASCII
    // value greater than p
    bool isValidSubString(String r, int K, int p)
    {
        int c = 0;

        for (int i = 0; i < r.Length; i++) {

            // if ASCII value is
            // greater than 'p'
            if ((int)r[i] > p) {
                c++;
            }
        }

        // if count of satisfying
        // characters is equal to 'K'
        // then return true
        if (c == K) {
            return true;
        }

        // otherwise return false
        else {
            return false;
        }
    }

    // function to count sub-Strings
    void countSubStrings(String s, int K, int p)
    {
        // length of the String
        int l = s.Length;

        // count of sub-Strings
        int count = 0;

        // 'i' is the starting
        // index for the sub-String
        for (int i = 0; i < l; i++) {

            // 'j' is the no. of characters
            // to include in the sub-String
            for (int j = K; (i + j) <= l; j++) {

                String r = s.Substring(i, j);

                // check if the sub-String
                // satisfies the condition
                if (isValidSubString(r, K, p)) {
                    count++;
                }
            }
        }
        Console.WriteLine(count);
    }

    // Driver code
    public static void Main(String[] args)
    {
        GFG g = new GFG();
        String s = "abepztydba";
        int K = 4;
        int p = 110;

        g.countSubStrings(s, K, p);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function that checks if
// the string contain exactly
// K characters having ASCII
// value greater than p
function isValidSubString(r, K, p)
{
    var c = 0;

    for (var i = 0; i < r.length; i++) {

        // if ASCII value is
        // greater than 'p'
        if (r.charCodeAt(i) > p)
            c++;
    }

    // if count of satisfying
    // characters is equal to 'K'
    // then return true
    if (c == K)
        return true;

    // otherwise return false
    else
        return false;
}

// function to count sub-strings
function countSubStrings(s, K, p)
{
    // length of the string
    var l = s.length;

    // count of sub-strings
    var count = 0;

    // 'i' is the starting
    // index for the sub-string
    for (var i = 0; i < l; i++) {

        // 'j' is the no. of characters
        // to include in the sub-string
        for (var j = K; (i + j) <= l; j++) {
            var r = s.substring(i, i+j);

            // check if the sub-string
            // satisfies the condition
            if (isValidSubString(r, K, p))
                count++;
        }
    }

    document.write( count + "<br>");
}

// Driver code
var s = "abepztydba";
var K = 4;
var p = 110;
countSubStrings(s, K, p);

</script>
```

**Output:** 

```
16
```