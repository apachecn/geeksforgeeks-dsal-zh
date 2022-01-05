# 计算给定长度的不同子串的数量

> 原文:[https://www . geeksforgeeks . org/count-给定长度的不同子字符串数/](https://www.geeksforgeeks.org/count-number-of-distinct-substrings-of-a-given-length/)

给定一个由小写英文字母和一个整数“l”组成的长度为 N 的字符串 S，求给定字符串的长度为“l”的不同子字符串的数量。

**示例:**

> **输入:**s =“abcbb”，l = 2
> **输出:** 4
> 长度为 2
> 的所有不同子串都将是{“ab”、“bc”、“cb”、“ba”}
> 因此，答案等于 4。
> **输入:** s =“亚的斯亚贝巴”，l = 2
> **输出:** 2

**天真方法:**
一个简单的方法是找到所有可能的子串，找到它们的哈希值，并找到不同子串的数量。
**时间复杂度:** O(l*N)

**高效方法:**
我们将使用**滚动哈希算法**来解决这个问题。

*   找到长度为“l”的第一个子字符串的哈希值。
    可评价为(s[0]-97)*x^(l-1)+(s[1]-97)*x^(l-2)……(s[l-1]-97)。让我们称之为'H₁'.
*   使用这个哈希值，我们将生成下一个哈希值为:
    h<sub>2</sub>=(h<sub>1</sub>-(s[0]-97)*x^(l-1)*x+(s[l]-97)。通过这种方式
    生成所有子串的散列，并将它们推入一个无序的集合中。
*   统计集合中不同值的数量。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
#define x 26
#define mod 3001
using namespace std;

// Function to find the required count
int CntSubstr(string s, int l)
{
    // Variable to the hash
    int hash = 0;

    // Finding hash of substring
    // (0, l-1) using random number x
    for (int i = 0; i < l; i++) {
        hash = (hash * x + (s[i] - 97)) % mod;
    }

    // Computing x^(l-1)
    int pow_l = 1;
    for (int i = 0; i < l - 1; i++)
        pow_l = (pow_l * x) % mod;

    // Unordered set to add hash values
    unordered_set<int> result;
    result.insert(hash);

    // Generating all possible hash values
    for (int i = l; i < s.size(); i++) {
        hash = ((hash - pow_l * (s[i - l] - 97)
              + 2 * mod) * x + (s[i] - 97)) % mod;
        result.insert(hash);
    }

    // Print the result
    cout << result.size() << endl;
}

// Driver Code
int main()
{
    string s = "abcba";

    int l = 2;

    CntSubstr(s, l);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG
{

    static int x = 26;
    static int mod = 3001;

    // Function to find the required count
    static void CntSubstr(char[] s, int l)
    {
        // Variable to the hash
        int hash = 0;

        // Finding hash of substring
        // (0, l-1) using random number x
        for (int i = 0; i < l; i++)
        {
            hash = (hash * x + (s[i] - 97)) % mod;
        }

        // Computing x^(l-1)
        int pow_l = 1;
        for (int i = 0; i < l - 1; i++)
        {
            pow_l = (pow_l * x) % mod;
        }

        // Unordered set to add hash values
        HashSet<Integer> result = new HashSet<Integer>();
        result.add(hash);

        // Generating all possible hash values
        for (int i = l; i < s.length; i++)
        {
            hash = ((hash - pow_l * (s[i - l] - 97)
                    + 2 * mod) * x + (s[i] - 97)) % mod;
            result.add(hash);
        }

        // Print the result
        System.out.println(result.size());
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "abcba";

        int l = 2;

        CntSubstr(s.toCharArray(), l);
    }
}

// This code contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    static int x = 26;
    static int mod = 3001;

    // Function to find the required count
    static void CntSubstr(char[] s, int l)
    {
        // Variable to the hash
        int hash = 0;

        // Finding hash of substring
        // (0, l-1) using random number x
        for (int i = 0; i < l; i++)
        {
            hash = (hash * x + (s[i] - 97)) % mod;
        }

        // Computing x^(l-1)
        int pow_l = 1;
        for (int i = 0; i < l - 1; i++)
        {
            pow_l = (pow_l * x) % mod;
        }

        // Unordered set to add hash values
        HashSet<int> result = new HashSet<int>();
        result.Add(hash);

        // Generating all possible hash values
        for (int i = l; i < s.Length; i++)
        {
            hash = ((hash - pow_l * (s[i - l] - 97)
                    + 2 * mod) * x + (s[i] - 97)) % mod;
            result.Add(hash);
        }

        // Print the result
        Console.WriteLine(result.Count);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String s = "abcba";

        int l = 2;

        CntSubstr(s.ToCharArray(), l);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of above approach
x = 26
mod = 3001

# Function to find the required count
def CntSubstr(s, l) :

    # Variable to the hash
    hash = 0;

    # Finding hash of substring
    # (0, l-1) using random number x
    for i in range(l) :
        hash = (hash * x + (ord(s[i]) - 97)) % mod;

    # Computing x^(l-1)
    pow_l = 1;
    for i in range(l-1) :
        pow_l = (pow_l * x) % mod;

    # Unordered set to add hash values
    result = set();
    result.add(hash);

    # Generating all possible hash values
    for i in range(l,len(s)) :
        hash = ((hash - pow_l * (ord(s[i - l]) - 97)
            + 2 * mod) * x + (ord(s[i]) - 97)) % mod;

        result.add(hash);

    # Print the result
    print(len(result)) ;

# Driver Code
if __name__ == "__main__" :

    s = "abcba";

    l = 2;

    CntSubstr(s, l);

# This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of above approach
var x = 26;
var mod = 3001;

// Function to find the required count
function CntSubstr(s, l)
{
    // Variable to the hash
    var hash = 0;

    // Finding hash of substring
    // (0, l-1) using random number x
    for (var i = 0; i < l; i++) {
        hash = (hash * x + (s[i].charCodeAt(0) - 97)) % mod;
    }

    // Computing x^(l-1)
    var pow_l = 1;
    for (var i = 0; i < l - 1; i++)
        pow_l = (pow_l * x) % mod;

    // Unordered set to add hash values
    var result = new Set();
    result.add(hash);

    // Generating all possible hash values
    for (var i = l; i < s.length; i++) {
        hash = ((hash - pow_l * (s[i - l].charCodeAt(0) - 97)
              + 2 * mod) * x + (s[i].charCodeAt(0) - 97)) % mod;
        result.add(hash);
    }

    // Print the result
    document.write( result.size );
}

// Driver Code
var s = "abcba";
var l = 2;
CntSubstr(s, l);

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N)