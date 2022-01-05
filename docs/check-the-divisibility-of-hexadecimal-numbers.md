# 检查十六进制数的可除性

> 原文:[https://www . geesforgeks . org/check-十六进制数的可除性/](https://www.geeksforgeeks.org/check-the-divisibility-of-hexadecimal-numbers/)

给定一个由一个大的十六进制数组成的字符串 **S** ，任务是用一个给定的十进制数 **M** 检查它的可除性。如果可分，则打印**是**否则打印**否**。
**举例:**

> **输入:**S =“10”，M = 4
> **输出:**是
> 10 是十进制 16 且(16 % 4) = 0
> **输入:**S =“10”，M = 5
> **输出:**否

**进场:**本[篇](https://www.geeksforgeeks.org/check-divisibility-binary-stream/)采用的一种进场方式将用于避免溢出。从背面迭代整个字符串。
如果子串**的剩余部分 S【0…I】**在与 **M** 的除法运算中已知。我们把这个余数叫做 **R** 。这可以用来在子串**S【0…I+1】**被除的时候得到余数。为此，首先将弦**S【0…I】**向左移动 **1** 。这相当于将字符串乘以 **16** 。然后，在此基础上添加 **S[i+1]** ，并使用 **M** 取其 mod。通过一点点模运算，它可以归结为

> S[0…I+1]% M =(S[0…I]* 16+S[I+1])% M =((S[0…I]% M * 16)+S[I+1])% M

因此，继续上述步骤，直到字符串结束。如果最后的余数是 **0** ，那么该字符串是可分的，否则它是不可分的。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const string CHARS = "0123456789ABCDEF";
const int DIGITS = 16;

// Function that returns true
// if s is divisible by m
bool isDivisible(string s, int m)
{
    // Map to map characters to real values
    unordered_map<char, int> mp;

    for (int i = 0; i < DIGITS; i++) {
        mp[CHARS[i]] = i;
    }

    // To store the remainder at any stage
    int r = 0;

    // Find the remainder
    for (int i = 0; i < s.size(); i++) {
        r = (r * 16 + mp[s[i]]) % m;
    }

    // Check the value of remainder
    if (!r)
        return true;
    return false;
}

// Driver code
int main()
{
    string s = "10";
    int m = 3;

    if (isDivisible(s, m))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static char []CHARS = "0123456789ABCDEF".toCharArray();
static int DIGITS = 16;

// Function that returns true
// if s is divisible by m
static boolean isDivisible(String s, int m)
{
    // Map to map characters to real values
    Map<Character, Integer> mp = new HashMap<>();

    for (int i = 0; i < DIGITS; i++)
    {        
        mp. put(CHARS[i], i);
    }

    // To store the remainder at any stage
    int r = 0;

    // Find the remainder
    for (int i = 0; i < s.length(); i++)
    {
        r = (r * 16 + mp.get(s.charAt(i))) % m;
    }

    // Check the value of remainder
    if (r == 0)
        return true;
    return false;
}

// Driver code
public static void main(String []args)
{
    String s = "10";
    int m = 3;

    if (isDivisible(s, m))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
CHARS = "0123456789ABCDEF";
DIGITS = 16;

# Function that returns true
# if s is divisible by m
def isDivisible(s, m) :

    # Map to map characters to real value
    mp = dict.fromkeys(CHARS, 0);

    for i in range( DIGITS) :
        mp[CHARS[i]] = i;

    # To store the remainder at any stage
    r = 0;

    # Find the remainder
    for i in range(len(s)) :
        r = (r * 16 + mp[s[i]]) % m;

    # Check the value of remainder
    if (not r) :
        return True;

    return False;

# Driver code
if __name__ == "__main__" :

    s = "10";
    m = 3;

    if (isDivisible(s, m)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

static char []CHARS = "0123456789ABCDEF".ToCharArray();
static int DIGITS = 16;

// Function that returns true
// if s is divisible by m
static bool isDivisible(String s, int m)
{
    // Map to map characters to real values
    Dictionary<char, int> mp = new Dictionary<char, int>();

    for (int i = 0; i < DIGITS; i++)
    {        
        if(mp.ContainsKey(CHARS[i]))
            mp[CHARS[i]] = i;
        else
            mp.Add(CHARS[i], i);
    }

    // To store the remainder at any stage
    int r = 0;

    // Find the remainder
    for (int i = 0; i < s.Length; i++)
    {
        r = (r * 16 + mp[s[i]]) % m;
    }

    // Check the value of remainder
    if (r == 0)
        return true;
    return false;
}

// Driver code
public static void Main(String []args)
{
    String s = "10";
    int m = 3;

    if (isDivisible(s, m))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var CHARS = "0123456789ABCDEF";
var DIGITS = 16;

// Function that returns true
// if s is divisible by m
function isDivisible(s, m)
{
    // Map to map characters to real values
    var mp = new Map();

    for (var i = 0; i < DIGITS; i++) {
        mp.set(CHARS[i], i);
    }

    // To store the remainder at any stage
    var r = 0;

    // Find the remainder
    for (var i = 0; i < s.length; i++) {
        r = (r * 16 + mp.get(s[i])) % m;
    }

    // Check the value of remainder
    if (!r)
        return true;
    return false;
}

// Driver code
var s = "10";
var m = 3;
if (isDivisible(s, m))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
No
```