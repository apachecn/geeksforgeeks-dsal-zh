# 检查二进制字符串是否包含长度为 k 的所有排列

> 原文:[https://www . geesforgeks . org/check-if-a-binary-string-contains-all-置换-length-k/](https://www.geeksforgeeks.org/check-if-a-binary-string-contains-all-permutations-of-length-k/)

给定一个二进制字符串和 k，检查它是否包含长度为 k 的所有排列。

示例:

```
Input : Binary string 11001
        k : 2
Output : Yes
11001 contains all possibilities of 
binary sequences with k = 2, 00, 01, 
10, 11

Input : Binary string: 1001
        k : 2
Output: No
1001 does not contain all possibilities of
binary sequences with k = 2\. Here 11 
sequence is missing
```

**方法 1:**
**解释:**
在这个例子中，一个长度为 k 的二进制序列没有被发现，它是 0110。
所以 k=4 的所有二进制序列都是 2 <sup>4</sup> =16。他们遵循
0000、0001、0010、0011、0100、0101、0110、0111、
1000、1001、1010、1011、1100、1101、1110、1111
都应该是给定二进制字符串的子字符串，然后打印是，否则打印否

**算法**
取二进制串和大小 k .在二进制串中我们检查二进制序列是否匹配。二进制序列是由大小为 k 的，正如我们知道的，在二进制中使用 0 和 1 位所以生成的二进制子集总数是 2 <sup>k</sup> 元素。它背后的主要思想是，将列表中的所有二进制值存储为字符串，然后将列表中的所有项目与给定的二进制字符串作为子集进行比较。如果所有都出现在二进制字符串中，则打印“是”，否则打印“否”。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Check a binary string
// contains all permutations of length k.

import java.util.*;
public class Checkbinary {

    // to check all Permutation in given String
    public static boolean tocheck(String s, int k)
    {
        List<String> list = BinarySubsets(k);

        // to check binary sequences are available
        // in string or not
        for (String b : list)
            if (s.indexOf(b) == -1)
                return false;       

        return true;
    }

    // to generate all binary subsets of given length k
    public static List<String> BinarySubsets(int k)
    {
        // Declare the list as String
        List<String> list = new ArrayList<>();

        // to define the format of binary of
        // given length k
        String format = "%0" + k + "d";

        // returns the string representation of the
        // unsigned integer value represented by
        // the argument in binary (base 2)  using
        // Integer.toBinaryString and convert it
        // into integer using Integer.valueOf.
        // Loop for 2<sup>k</sup> elements
        for (int i = 0; i < Math.pow(2, k); i++)
        {
            // To add in the list all possible
            // binary sequence of given length
            list.add(String.format(format,
                Integer.valueOf(Integer.toBinaryString(i))));

            /* To Show all binary sequence of given
               length k
            System.out.println(String.format(format,
            Integer.valueOf(Integer.toBinaryString(i))));*/
        }
        return list;
    }

    // drive main
    public static void main(String[] args)
    {
        String str = "11001";
        int num = 2;
        if (tocheck(str, num))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

**Output**

```
Yes
```

**方法二:**

**算法**
取二进制串和大小 k .在二进制串中我们检查二进制序列是否匹配。二进制序列是由大小为 k 的，正如我们知道的，在二进制中使用 0 和 1 位所以生成的二进制子集总数是 2 <sup>k</sup> 元素。其背后的主要思想是，将给定字符串的大小为 k 的所有子串存储到集合中，即存储大小为 k 的不同子串，如果集合的大小等于 2 <sup>k</sup> 则打印“是”，否则打印“否”。

## C++14

```
// C++ Program to Check If a
// String Contains All Binary
// Codes of Size K
#include <bits/stdc++.h>
using namespace std;
#define int long long

bool hasAllcodes(string s, int k)
{

    // Unordered map of type string
    unordered_set<string> us;

    for (int i = 0; i + k <= s.size(); i++)
    {
        us.insert(s.substr(i, k));
    }
    return us.size() == 1 << k;
}

// Driver Code
signed main()
{
    string s = "00110110";
    int k = 2;
    if (hasAllcodes)
    {
        cout << "YES\n";
    }
    else
    {
        cout << "NO\n";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Check If a
// String Contains All Binary
// Codes of Size K
import java.io.*;
import java.util.*;
class GFG
{
    static boolean hasAllcodes(String s, int k)
    {

        // Unordered map of type string
        Set<String> us= new HashSet<String>();
        for(int i = 0; i + k <= s.length(); i++)
        {
            us.add(s.substring(i, i + k));
        }
        return (us.size() == (1 << k));
    }

    // Driver code
    public static void main (String[] args)
    {
        String s = "00110110";
        int k = 2;
        if(hasAllcodes(s, k))
        {
            System.out.println("YES");
        }
        else
        {
            System.out.println("NO");
        }
    }
}

//  This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 Program to Check If a
# String Contains All Binary
# Codes of Size K
def hasAllcodes(s, k) :

    # Unordered map of type string
    us = set()
    for i in range(len(s) + 1) :   
        us.add(s[i : k])   
    return len(us) == 1 << k

# Driver code
s = "00110110"
k = 2
if (hasAllcodes) :
    print("YES")
else :
    print("NO")

    # This code is contributed by divyeshrabadiya07
```

## C#

```
// C# Program to Check If a
// String Contains All Binary
// Codes of Size K
using System;
using System.Collections.Generic;
class GFG {

  static bool hasAllcodes(string s, int k)
  {

    // Unordered map of type string
    HashSet<string> us = new HashSet<string>();

    for (int i = 0; i + k <= s.Length; i++)
    {
      us.Add(s.Substring(i, k));
    }

    return us.Count == 1 << k;
  }

  // Driver code
  static void Main()
  {
    string s = "00110110";
    int k = 2;
    if(hasAllcodes(s, k))
    {
      Console.WriteLine("YES");
    }
    else
    {
      Console.WriteLine("NO");
    }
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// Javascript program to Check If a
// String Contains All Binary
// Codes of Size K
function hasAllcodes(s,k)
{

    // Unordered map of type string
    let us = new Set();
    for(let i = 0; i + k <= s.length; i++)
    {
        us.add(s.substring(i, i + k));
    }
    return (us.size == (1 << k));
}

// Driver code
let s = "00110110";
let k = 2;   

if (hasAllcodes(s, k))
{
    document.write("YES");
}
else
{
    document.write("NO");
}

// This code is contributed by ab2127

</script>
```

**Output**

```
YES
```